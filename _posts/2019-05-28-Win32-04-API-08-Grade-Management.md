---
layout: post
title: "Win32 - API - Grade Management"
description: ""
date: 2019-05-28 00:04:08
tags: [win32]
comments: true
share: true
---

[TOC]

## 요구사항

- 관리자 로그인
- 관리자 정보 수정
- 학생 정보, 성적 정보 파일로 저장



![](https://raw.githubusercontent.com/lazyartist/blog/master/images/GradeManagement.gif)



## 소스코드

### common.h

- 프로그램 전역에서 공통으로 사용하는 구조체와 함수 및 매크로를 정의

```cpp
#pragma once

#include <iostream> // sprintf_s()
#include "Windows.h"
//#include <vector>

using namespace std;


// ===== define =====
#define Max_Account_Text 10 + 1

#define Max_Student_Id 6 + 1
#define Max_Student_Name 10 + 1
#define Max_Student_Info_Line (Max_Student_Id + 1 + Max_Student_Name)

#define Max_Score_Text 9 + 1
#define Max_Score_Info_Line (Max_Student_Id + 1 + Max_Score_Text + 1 + Max_Score_Text + 1 + Max_Score_Text)

#define Max_Semester 4

#define Str_ScoreFile_Path_Format "scores/%s_%d.txt"

// ===== define ===== end


// ===== enum =====
enum LoginResultType
{
	Success, Fail
};
// ===== enum =====  end


// ===== struct =====
typedef struct _Student {
	char Id[Max_Student_Id];
	char Name[Max_Student_Name];
} Student, *PStudent;

typedef struct _Score {
	char Course[Max_Score_Text];
	char Point[Max_Score_Text];

	_Score(const char *course, const char *point) {
		strcpy_s(Course, course);
		strcpy_s(Point, point);
	}
} Score, *PScore;
// ===== struct ===== end


// ===== function =====
inline void log(LPCSTR lpStr) {
	OutputDebugString(lpStr);
	OutputDebugString("\n");
};

inline void log(LPCSTR lpStr, LPCSTR lpStr2) {
	OutputDebugString(lpStr);
	OutputDebugString(", ");
	OutputDebugString(lpStr2);
	OutputDebugString("\n");
};

inline void log(LPCSTR lpStr, LPCSTR lpStr2, LPCSTR lpStr3) {
	OutputDebugString(lpStr);
	OutputDebugString(", ");
	OutputDebugString(lpStr2);
	OutputDebugString(", ");
	OutputDebugString(lpStr3);
	OutputDebugString("\n");
};

inline void log(int i) {
	char buffer[99];
	sprintf_s(buffer, 99, "%d", i);
	OutputDebugString(buffer);
	OutputDebugString("\n");
};
// ===== function ===== end

```



### File.cpp

- 파일 스트림 관리를 용이하게 하기 위한 기능 제공

```cpp
#pragma once 

#include "File.h"

File::File(const char *fileName, const char *mode)
{
	fopen_s(&_pFile, "account.txt", mode);
}

File::~File()
{
	close();
}

void File::getLine(char *buffer, size_t bufferSize) {
	if (_pFile != nullptr) {
		fgets(buffer, bufferSize, _pFile);

		// \n은 줄바꿈을 지정하는 문자이므로 순수 문자만 얻기 위해 제거한다.
		buffer[strcspn(buffer, "\n")] = 0; // strcspn()으로 "\n"의 위치를 찾고 그 위치에 0을 넣어준다.
	}
}

void File::writeLine(const char *buffer, size_t bufferSize) {
	if (_pFile != nullptr) {
		fputs(buffer, _pFile);
	}
}

void File::close() {
	if (_pFile != nullptr) {
		fclose(_pFile);
	}
}
```



### 0700-GradeManagement.cpp

- 메인 함수가 있는 파일
- 윈도우와 관련된 모든 행동, 프로시저를 정의한다.

```cpp
#include "Windows.h"
#include "resource.h"
#include "common.h"
#include "File.h"
#include <vector>
#include "Commctrl.h"
#include "StudentList.h"
#include "ScoreList.h"

HINSTANCE g_hInstance;

char g_strLoginId[Max_Account_Text];

// 학생
StudentList g_studentList;
UINT g_nSelectedStudentIndex = -1;
Student g_selectedStudent;
// 학기
UINT g_nSelectedSemesterIndex = -1;
int g_semesterRadioIds[Max_Semester] = { IDC_RADIO1 , IDC_RADIO2 , IDC_RADIO3 , IDC_RADIO4 };
// 점수
UINT g_nSelectedScoreIndex = -1;
ScoreList g_scoreList;

// 윈도우 프로시저
INT_PTR CALLBACK LoginDlgProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam);
INT_PTR CALLBACK LoginInfoChangeDlgProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam);
INT_PTR CALLBACK MainDlgProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam);

void UpdateLoginInfo(HWND hWnd);
void UpdateStudentsListView(HWND hWnd);
void UpdateScoreListView(HWND hWnd);
void UpdateSelectedStudentInfo(HWND hWnd);

void UpdateStudentDeleteButtonState(HWND hWnd);
void UpdateScoreDeleteButtonState(HWND hWnd);

void SelectSemester(HWND hWnd, UINT index);
int GetSemesterIndexById(UINT id);

void SetWindowPositionToCenter(HWND hWnd);

int APIENTRY WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow)
{
	g_hInstance = hInstance;

	LoginResultType loginResult = (LoginResultType)DialogBox(hInstance, MAKEINTRESOURCE(IDD_DIALOG1), nullptr, LoginDlgProc);
	//LoginResultType loginResult = LoginResultType::Success;
	if (loginResult == LoginResultType::Success) {
		log("login success!!");

		// 메인창 띄움
		DialogBox(hInstance, MAKEINTRESOURCE(IDD_DIALOG2), nullptr, MainDlgProc);
	}
	else {
		log("login Failed!!");
	}

	return 0;
}

// 메인 윈도우 프로시저
INT_PTR CALLBACK MainDlgProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam)
{
	switch (message)
	{
	case WM_INITDIALOG:
	{
		UpdateLoginInfo(hWnd);
		UpdateStudentDeleteButtonState(hWnd);

		// 스크린 가운데 출력
		SetWindowPositionToCenter(hWnd);

		// 학생리스트 설정
		{
			// 컬럼 추가
			HWND hListView = GetDlgItem(hWnd, IDC_LIST1);
			char colText0[] = "학번";
			char colText1[] = "이름";
			LVCOLUMN col = {};
			col.mask = LVCF_FMT | LVCF_WIDTH | LVCF_TEXT | LVCF_SUBITEM;
			col.fmt = LVCFMT_LEFT;
			col.cx = 60;
			col.pszText = colText0;
			ListView_InsertColumn(hListView, 0, &col); // 컬럼 추가0
			col.pszText = colText1;
			ListView_InsertColumn(hListView, 1, &col); // 컬럼 추가1

			// 리스트 아이템 전체가 선택되도록 설정
			ListView_SetExtendedListViewStyle(
				GetDlgItem(hWnd, IDC_LIST1),
				LVS_EX_FULLROWSELECT // 아이템 전체가 클릭되도록 한다.
				| LVS_EX_GRIDLINES // 서브아이템 사이에 그리드 라인을 넣는다.
			);
		}


		// 점수리스트 설정
		{
			// 컬럼 추가
			HWND hListView = GetDlgItem(hWnd, IDC_LIST2);
			char colText0[] = "과목";
			char colText1[] = "점수";
			LVCOLUMN col = {};
			col.mask = LVCF_FMT | LVCF_WIDTH | LVCF_TEXT | LVCF_SUBITEM;
			col.fmt = LVCFMT_LEFT;
			col.cx = 60;
			col.pszText = colText0;
			ListView_InsertColumn(hListView, 0, &col); // 컬럼 추가0
			col.pszText = colText1;
			ListView_InsertColumn(hListView, 1, &col); // 컬럼 추가1

			// 리스트 아이템 전체가 선택되도록 설정
			ListView_SetExtendedListViewStyle(
				GetDlgItem(hWnd, IDC_LIST2),
				LVS_EX_FULLROWSELECT // 아이템 전체가 클릭되도록 한다.
				| LVS_EX_GRIDLINES // 서브아이템 사이에 그리드 라인을 넣는다.
			);
		}

		// 파일에서 학생정보 읽기
		g_studentList.LoadStudents("students.txt");
		UpdateStudentsListView(hWnd);
		// 1학기 선택
		SelectSemester(hWnd, 0);
		// 점수 리스트 갱신
		UpdateScoreListView(hWnd);
	}
	break;

	case WM_NOTIFY: // 공통 컨트롤러의 메시지 통지
	{
		switch (wParam)
		{
		case IDC_LIST1: // 학생 리스트
		{
			NMTTDISPINFO *nmttdispinfo = (NMTTDISPINFO*)lParam;
			if (nmttdispinfo->hdr.code == LVN_ITEMCHANGED) {
				g_nSelectedStudentIndex = ListView_GetNextItem(
					nmttdispinfo->hdr.hwndFrom, // 윈도우 핸들
					-1, // 검색을 시작할 인덱스
					LVNI_SELECTED // 검색 조건
				);
				if (g_nSelectedStudentIndex == -1) {
					// 
				}
				else {
					ListView_GetItemText(nmttdispinfo->hdr.hwndFrom, g_nSelectedStudentIndex, 0, g_selectedStudent.Id, Max_Student_Id);
					ListView_GetItemText(nmttdispinfo->hdr.hwndFrom, g_nSelectedStudentIndex, 1, g_selectedStudent.Name, Max_Student_Name);
					log(g_selectedStudent.Id, g_selectedStudent.Name);
				}

				UpdateSelectedStudentInfo(hWnd);
				UpdateStudentDeleteButtonState(hWnd);

				SelectSemester(hWnd, 0);

				UpdateScoreListView(hWnd);
			}
		}
		break;

		case IDC_LIST2: // 성적 리스트
		{
			NMTTDISPINFO *nmttdispinfo = (NMTTDISPINFO*)lParam;
			if (nmttdispinfo->hdr.code == LVN_ITEMCHANGED) {
				g_nSelectedScoreIndex = ListView_GetNextItem(
					nmttdispinfo->hdr.hwndFrom, // 윈도우 핸들
					-1, // 검색을 시작할 인덱스
					LVNI_SELECTED // 검색 조건
				);
				if (g_nSelectedScoreIndex == -1) {
					// 
				}
				else {
					char course[Max_Account_Text];
					ListView_GetItemText(nmttdispinfo->hdr.hwndFrom, g_nSelectedScoreIndex, 0, course, Max_Account_Text);
					log(course);
				}

				UpdateScoreDeleteButtonState(hWnd);
			}
		}
		break;

		default:
			break;
		}
	}
	break;

	case WM_COMMAND:
	{
		switch (LOWORD(wParam))
		{
		case IDOK:
		{
			File f("account.txt", "rt");
			char id[Max_Account_Text] = {};
			char pw[Max_Account_Text] = {};
			f.getLine(id, Max_Account_Text); // 한줄씩 읽는다.
			f.getLine(pw, Max_Account_Text); // 한줄씩 읽는다.

			char editId[Max_Account_Text] = {};
			char editPw[Max_Account_Text] = {};
			GetDlgItemText(hWnd, IDC_EDIT1, editId, Max_Account_Text);
			GetDlgItemText(hWnd, IDC_EDIT2, editPw, Max_Account_Text);

			int resId = strcmp(id, editId);
			int resPw = strcmp(pw, editPw);

			LoginResultType loginResult = LoginResultType::Fail;
			if (resId == 0 && resPw == 0) {
				// 파일에 저장된 Id, Pw와 입력한 Id, Pw가 같으므로 로그인 성공
				loginResult = LoginResultType::Success;
			}

			EndDialog(hWnd, (INT_PTR)loginResult);
		}
		break;

		case IDC_BUTTON1: // 로그인 정보 변경 버튼
		{
			DialogBox(g_hInstance, MAKEINTRESOURCE(IDD_DIALOG3), hWnd, LoginInfoChangeDlgProc);
		}
		break;

		case IDC_BUTTON2: // 학생 삭제 버튼
		{
			g_studentList.RemoveStudent(g_nSelectedStudentIndex);

			g_nSelectedStudentIndex = -1;
			UpdateStudentsListView(hWnd);
			UpdateStudentDeleteButtonState(hWnd);
		}
		break;

		case IDC_BUTTON4: // 학생 파일저장 버튼
		{
			g_studentList.SaveStudents();
		}
		break;

		case IDC_BUTTON3: // 학생 추가 버튼
		{
			LRESULT rId = SendMessage(GetDlgItem(hWnd, IDC_EDIT1), WM_GETTEXTLENGTH, 0, 0);
			LRESULT rName = SendMessage(GetDlgItem(hWnd, IDC_EDIT2), WM_GETTEXTLENGTH, 0, 0);

			if (rId == 0 || rName == 0) {
				MessageBox(hWnd, "input id or name", "input", MB_OK);
			}
			else {
				char id[Max_Account_Text];
				char name[Max_Account_Text];
				GetDlgItemText(hWnd, IDC_EDIT1, id, Max_Account_Text);
				GetDlgItemText(hWnd, IDC_EDIT2, name, Max_Account_Text);
				g_studentList.AddStudent(id, name);

				UpdateStudentsListView(hWnd);

				SetDlgItemText(hWnd, IDC_EDIT1, "");
				SetDlgItemText(hWnd, IDC_EDIT2, "");
			}

		}
		break;

		case IDC_RADIO1: // 학기 라디오 버튼
		case IDC_RADIO2:
		case IDC_RADIO3:
		case IDC_RADIO4:
		{
			int radioIndex = GetSemesterIndexById(LOWORD(wParam));

			SelectSemester(hWnd, radioIndex);

			g_nSelectedScoreIndex = -1;
			UpdateScoreListView(hWnd);
			UpdateScoreDeleteButtonState(hWnd);
		}
		break;

		case IDC_BUTTON5: // 성적 추가 버튼
		{
			LRESULT rCourse = SendMessage(GetDlgItem(hWnd, IDC_EDIT6), WM_GETTEXTLENGTH, 0, 0);
			LRESULT rPoint = SendMessage(GetDlgItem(hWnd, IDC_EDIT7), WM_GETTEXTLENGTH, 0, 0);

			if (rCourse == 0 || rPoint == 0) {
				MessageBox(hWnd, "input course or point", "input", MB_OK);
			}
			else {
				char course[Max_Account_Text];
				char point[Max_Account_Text];
				GetDlgItemText(hWnd, IDC_EDIT6, course, Max_Account_Text);
				GetDlgItemText(hWnd, IDC_EDIT7, point, Max_Account_Text);

				Score score = { course, point };
				g_scoreList.AddScore(&score);

				UpdateScoreListView(hWnd);

				SetDlgItemText(hWnd, IDC_EDIT6, "");
				SetDlgItemText(hWnd, IDC_EDIT7, "");
			}

		}
		break;

		case IDC_BUTTON6: // 성적 삭제 버튼
		{
			g_scoreList.RemoveScore(g_nSelectedScoreIndex);

			g_nSelectedScoreIndex = -1;
			UpdateScoreListView(hWnd);
			UpdateScoreDeleteButtonState(hWnd);
		}
		break;

		case IDC_BUTTON7: // 성적 저장 버튼
		{
			// 학생 선택 확인
			if (g_nSelectedSemesterIndex == -1) {
				break;
			}

			// 학생 Id, 학기 정보로 현재 성적 리스트 파일로 저장
			g_scoreList.SaveScores(g_selectedStudent.Id, g_nSelectedSemesterIndex);
		}
		break;

		case IDCANCEL:
			EndDialog(hWnd, (INT_PTR)LoginResultType::Fail);
			break;

		default:
			break;

		}
		break;
	}

	default:
		break;
	}

	return false;
}

void CheckLogin() {

}

// 로그인 다이얼로그 프로시저
INT_PTR CALLBACK LoginDlgProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam)
{
	switch (message)
	{
	case WM_INITDIALOG:
		SetWindowPositionToCenter(hWnd);
		break;
	case WM_COMMAND:
	{
		switch (LOWORD(wParam))
		{
		case IDOK:
		{
			File f("account.txt", "rt");
			char id[Max_Account_Text] = {};
			char pw[Max_Account_Text] = {};
			f.getLine(id, Max_Account_Text); // 한줄씩 읽는다.
			f.getLine(pw, Max_Account_Text); // 한줄씩 읽는다.

			char editId[Max_Account_Text] = {};
			char editPw[Max_Account_Text] = {};
			GetDlgItemText(hWnd, IDC_EDIT1, editId, Max_Account_Text);
			GetDlgItemText(hWnd, IDC_EDIT2, editPw, Max_Account_Text);

			int resId = strcmp(id, editId);
			int resPw = strcmp(pw, editPw);

			LoginResultType loginResult = LoginResultType::Fail;
			if (resId == 0 && resPw == 0) {
				// 파일에 저장된 Id, Pw와 입력한 Id, Pw가 같으므로 로그인 성공
				strcpy_s(g_strLoginId, id);
				loginResult = LoginResultType::Success;
				EndDialog(hWnd, (INT_PTR)loginResult);
			}
			else {
				// 로그인 실패
				MessageBox(hWnd, "로그인 실패!!", "로그인", MB_OK);
			}
		}
		break;

		case IDCANCEL:
			EndDialog(hWnd, (INT_PTR)LoginResultType::Fail);
			break;

		default:
			break;

		}
		break;
	}

	default:
		break;
	}

	return false;
}

// 로그인정보 수정 다이얼로그 프로시저
INT_PTR CALLBACK LoginInfoChangeDlgProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam)
{
	switch (message)
	{
	case WM_INITDIALOG:
	{
		SetFocus(GetDlgItem(hWnd, IDC_EDIT1));
	}
	break;

	case WM_COMMAND:
	{
		switch (LOWORD(wParam))
		{
		case IDOK:
		{
			File readAccountFile("account.txt", "rt");
			char id[Max_Account_Text] = {};
			char pw[Max_Account_Text] = {};
			readAccountFile.getLine(id, Max_Account_Text); // 한줄씩 읽는다.
			readAccountFile.getLine(pw, Max_Account_Text); // 한줄씩 읽는다.
			readAccountFile.close();

			char editCurId[Max_Account_Text] = {};
			char editPw[Max_Account_Text] = {};
			GetDlgItemText(hWnd, IDC_EDIT1, editCurId, Max_Account_Text);
			GetDlgItemText(hWnd, IDC_EDIT2, editPw, Max_Account_Text);

			int resId = strcmp(id, editCurId);
			int resPw = strcmp(pw, editPw);

			// 파일에 저장된 Id, Pw와 입력한 Id, Pw가 같다.
			if (resId == 0 && resPw == 0) {
				char editChangeId[Max_Account_Text] = {};
				char editChangePw[Max_Account_Text] = {};

				// 새로운 로그인 정보
				GetDlgItemText(hWnd, IDC_EDIT3, editChangeId, Max_Account_Text);
				GetDlgItemText(hWnd, IDC_EDIT4, editChangePw, Max_Account_Text);

				File writeAccountFile("account.txt", "wt");
				writeAccountFile.writeLine(editChangeId, Max_Account_Text);
				writeAccountFile.writeLine("\n", Max_Account_Text);
				writeAccountFile.writeLine(editChangePw, Max_Account_Text);
				writeAccountFile.close();

				EndDialog(hWnd, 0);
				MessageBox(hWnd, "성공!!", "로그인 정보 변경", MB_OK);
			}
		}
		break;
		case IDCANCEL:
			EndDialog(hWnd, 0);
			return 0;
			break;
		default:
			break;
		}
	}
	break;

	default:
		break;
	}

	return 0;
}

// 윈도우의 위치를 스크린 가운데로 옮김
void SetWindowPositionToCenter(HWND hWnd) {
	int screenX = GetSystemMetrics(SM_CXFULLSCREEN);
	int screenY = GetSystemMetrics(SM_CYFULLSCREEN);

	RECT rectClient;
	GetWindowRect(hWnd, &rectClient);
	UINT clientW = rectClient.right - rectClient.left;
	UINT clientH = rectClient.bottom - rectClient.top;

	MoveWindow(hWnd, (screenX / 2) - (clientW / 2), (screenY / 2) - (clientH / 2), clientW, clientH, false);
}

void UpdateLoginInfo(HWND hWnd) {
	SetDlgItemText(hWnd, IDC_EDIT4, g_strLoginId);
}

void UpdateStudentsListView(HWND hWnd)
{
	HWND hListView = GetDlgItem(hWnd, IDC_LIST1);

	ListView_DeleteAllItems(hListView);

	// 아이템 추가
	LVITEM item = {};
	item.mask = LVIF_TEXT;
	item.iSubItem = 0; // 아이템을 처음 추가하므로 0번째 서브아이템을 선택한다.
	item.state;
	item.stateMask;
	int itemCount = 0;

	auto students = g_studentList.GetStudents();
	vector<Student>::iterator it = students->begin();
	while (it != students->end())
	{
		itemCount = ListView_GetItemCount(hListView);

		item.iItem = itemCount;
		item.pszText = it->Id;
		ListView_InsertItem(hListView, &item); // 아이템 추가0
		ListView_SetItemText(hListView, itemCount/*item idx*/, 1/*subitem idx*/, it->Name); // 서브아이템 추가0

		++it;
	}
}

void UpdateStudentDeleteButtonState(HWND hWnd) {
	EnableWindow(GetDlgItem(hWnd, IDC_BUTTON2), g_nSelectedStudentIndex != -1);
}

void UpdateSelectedStudentInfo(HWND hWnd) {
	SetDlgItemText(hWnd, IDC_EDIT8, g_selectedStudent.Id);
	SetDlgItemText(hWnd, IDC_EDIT9, g_selectedStudent.Name);

	SelectSemester(hWnd, 0);
}

void UpdateScoreDeleteButtonState(HWND hWnd) {
	EnableWindow(GetDlgItem(hWnd, IDC_BUTTON6), g_nSelectedScoreIndex != -1);
}

void SelectSemester(HWND hWnd, UINT index)
{
	CheckDlgButton(hWnd,
		g_semesterRadioIds[index], // 컨트롤 ID
		BST_CHECKED // 상태
	);

	g_nSelectedSemesterIndex = index;

	// 학생과 학기가 선택됐다면 성적 파일을 읽어들임
	g_scoreList.LoadScore(g_selectedStudent.Id, g_nSelectedSemesterIndex);
}

int GetSemesterIndexById(UINT id)
{
	for (size_t i = 0; i < Max_Semester; i++)
	{
		if (g_semesterRadioIds[i] == id) {
			return i;
		}
	}
}

void UpdateScoreListView(HWND hWnd)
{
	HWND hListView = GetDlgItem(hWnd, IDC_LIST2);

	ListView_DeleteAllItems(hListView);

	// 아이템 추가
	LVITEM item = {};
	item.mask = LVIF_TEXT;
	item.iSubItem = 0; // 아이템을 처음 추가하므로 0번째 서브아이템을 선택한다.
	item.state;
	item.stateMask;
	int itemCount = 0;

	auto scores = g_scoreList.GetScores();
	vector<Score>::iterator it = scores->begin();
	while (it != scores->end())
	{
		itemCount = ListView_GetItemCount(hListView);

		item.iItem = itemCount;
		item.pszText = it->Course;
		ListView_InsertItem(hListView, &item); // 아이템 추가0
		ListView_SetItemText(hListView, itemCount/*item idx*/, 1/*subitem idx*/, it->Point); // 서브아이템 추가0

		++it;
	}
}
```



### StudentList.cpp

- 학생 리스트를 관리한다.

```cpp
#include "StudentList.h"


StudentList::StudentList()
{
}

StudentList::StudentList(const char * filePath)
{
	LoadStudents(filePath);
}


StudentList::~StudentList()
{
}

void StudentList::LoadStudents(const char * filePath)
{
	// 프로그램 내에서 파일을 여러번 열고 닫을 경우 fopen_s는 두번째부터 에러(13)가 나기 때문에 
		// _fsopen()을 사용한다.
		//fopen_s(&file, "students.txt", "rt");
	FILE *file;
	file = _fsopen(filePath, "rt", _SH_DENYNO/*Permits read and write access.*/);

	char studentsFileInfo[Max_Student_Info_Line] = {};
	fgets(studentsFileInfo, Max_Student_Info_Line, file);
	int studentsCount = atoi(studentsFileInfo);

	char studentInfoLine[Max_Student_Info_Line] = {};
	char id[Max_Student_Id];
	char name[Max_Student_Name];
	char *token;
	char *nextToken;

	_vStudents.clear();
	_vStudents.reserve(studentsCount); // 메모리 미리 할당

	for (size_t i = 0; i < studentsCount; i++)
	{
		fgets(studentInfoLine, Max_Student_Info_Line, file);

		token = strtok_s(studentInfoLine, "\t", &nextToken);
		strcpy_s(id, token);
		token = strtok_s(NULL, "\t", &nextToken);
		strcpy_s(name, token);

		// \n을 제거
		id[strcspn(id, "\n")] = 0;
		name[strcspn(name, "\n")] = 0;

		AddStudent(id, name);
	}
}

void StudentList::SaveStudents()
{
	// 파일 열기
	FILE *file;
	file = _fsopen("students.txt", "wt", _SH_DENYNO/*Permits read and write access.*/);

	if (file != nullptr) {
		char buffer[Max_Student_Info_Line];

		// 학생 수 기록
		int itemCount = _vStudents.size();
		sprintf_s(buffer, Max_Student_Info_Line, "%d\n", itemCount);
		fputs(buffer, file);

		// 학생 정보 기록
		auto it = _vStudents.begin();
		while (it != _vStudents.end())
		{
			sprintf_s(buffer, Max_Student_Info_Line, "%s\t%s\n", it->Id, it->Name);
			fputs(buffer, file);

			++it;
		}
	}

	if (file) {
		fclose(file);
		log("SaveStudents success!");
	}
}

void StudentList::ClearStudents()
{
	_vStudents.clear();
}

void StudentList::AddStudent(char *id, char *name)
{
	Student student = {};
	strcpy_s(student.Id, id);
	strcpy_s(student.Name, name);

	_vStudents.push_back(student);
}

void StudentList::RemoveStudent(int index)
{
	if (index != -1) {
		auto itBegin = _vStudents.begin();
		auto itTarget = itBegin + index;
		_vStudents.erase(itTarget);
	}
}

vector<Student>* StudentList::GetStudents()
{
	return &_vStudents;
}

```



### ScoreList.cpp

- 점수 리스트를 관리한다.

```cpp
#include "ScoreList.h"

ScoreList::ScoreList()
{
}

ScoreList::~ScoreList()
{
}

void ScoreList::LoadScore(const char * id, unsigned int semester)
{
	_vScores.clear();

	// 프로그램 내에서 파일을 여러번 열고 닫을 경우 fopen_s는 두번째부터 에러(13)가 나기 때문에 _fsopen()을 사용한다.
	//fopen_s(&file, "students.txt", "rt");
	char filePath[MAX_PATH];
	sprintf_s(filePath, Str_ScoreFile_Path_Format, id, semester);

	FILE *file;
	file = _fsopen(filePath, "rt", _SH_DENYNO/*Permits read and write access.*/);

	IsExistScore = file != nullptr;
	if (IsExistScore) {
		char strLineCount[Max_Score_Info_Line] = {};
		fgets(strLineCount, Max_Score_Info_Line, file);
		int nLineCount = atoi(strLineCount);

		char strScoreInfoLine[Max_Score_Info_Line] = {};
		char id[Max_Student_Id];
		char semester[Max_Score_Text];
		char course[Max_Score_Text];
		char point[Max_Score_Text];

		char *token;
		char *nextToken;

		_vScores.reserve(nLineCount); // 메모리 미리 할당

		for (size_t i = 0; i < nLineCount; i++)
		{
			memset(strScoreInfoLine, 0, Max_Score_Info_Line);
			fgets(strScoreInfoLine, Max_Score_Info_Line, file);

			token = strtok_s(strScoreInfoLine, "\t", &nextToken);
			strcpy_s(course, token);
			token = strtok_s(NULL, "\t", &nextToken);
			strcpy_s(point, token);

			// \n을 제거
			course[strcspn(course, "\n")] = 0;
			point[strcspn(point, "\n")] = 0;

			log(course);

			Score score(course, point);
			AddScore(&score);
		}
	}
}

void ScoreList::SaveScores(const char * id, unsigned int semesterIndex)
{
	// 파일 열기
	char filePath[MAX_PATH];
	sprintf_s(filePath, Str_ScoreFile_Path_Format, id, semesterIndex);

	FILE *file;
	file = _fsopen(filePath, "wt", _SH_DENYNO); // 경로에 폴더가 있다면 이미 존해해야함. 파일과 같이 생성하지 않음.

	if (file != nullptr) {
		char buffer[Max_Score_Info_Line];

		// 성적 수 기록
		int itemCount = _vScores.size();
		sprintf_s(buffer, Max_Score_Info_Line, "%d\n", itemCount);
		fputs(buffer, file);

		// 성적 정보 기록
		auto it = _vScores.begin();
		while (it != _vScores.end())
		{
			sprintf_s(buffer, Max_Score_Info_Line, "%s\t%s\n", it->Course, it->Point);
			fputs(buffer, file);

			++it;
		}
	}

	if (file) {
		fclose(file);
		log("SaveScores success!");
	}
}

void ScoreList::AddScore(Score *score)
{
	_vScores.push_back(*score);
}

void ScoreList::RemoveScore(int index)
{
	if (index != -1) {
		auto itBegin = _vScores.begin();
		auto itTarget = itBegin + index;
		_vScores.erase(itTarget);
	}
}

vector<Score>* ScoreList::GetScores()
{
	return &_vScores;
}

```

