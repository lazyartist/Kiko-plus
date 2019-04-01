---
layout: post
title: "Math - Collision Speed up"
description: ""
date: 2019-03-22 19:00:00+09:00
tags: [game, math, math]
comments: true
share: true
---

[TOC]



## 충돌 판정의 고속화

#### 평면의 앞뒤 확인

충돌을 앞으로만 한정하여 평면의 충돌 테스트 대상을 줄일 수 있다.

충돌 대상의 각 면의 법선 벡터와 충돌 방향을 내적하여 서로 마주보고 있다면(각도가 90~180 사이) 충돌 테스트 대상으로 선정한다.

#### 충돌 영역의 간략화

실제 게임에서 충돌 영역이 미세하지 않아도 게임 플레이에 지정을 주지 않는 경우가 많다. 

이럴 때 충돌 영역을 구와 같이 간단한 형태로 만들어 충돌 검출에 필요한 계산을 줄일 수 있다.



## 바운딩 볼륨

실제 충돌 테스트할 대상을 충돌체로 감싸고 이 충돌체가 충돌했을 때 실제 대상과 충돌 테스트를 하는 방법으로 실제 충돌 대상의 복잡한 충돌 테스트를 필요할 때만 할 수 있다.

감싸는 충돌체는 충돌 판정을 쉽게 할 수 있는 구, 박스 형태가 사용된다.



#### 바운딩 스피어

구 형태의 바운딩 볼륨이다.

구는 선분과 충돌 판정이 복잡하므로 구끼리 충돌 판정하는 것이 좋다.

충돌 판정이 쉽고 구조가 간단해서 메모리를 적게 사용하는 장점이 있지만 실제 객체를 감쌀 때 빈 공간이 생기기 쉽다.



#### 바운딩 박스

박스 형태의 바운딩 볼륨이다.

구보다 빈틈없이 객체를 감쌀 수 있다.



## 바운딩 볼륨 검출 방법



#### AABB(Axis-Aligned Bounding Box)

###### AABB 이론

x, y, z축에 평행한 변을 갖는 상자로 객체가 회전해도 상자는 회전하지 않는다.

두 점으로 상자를 만들고 선분과 충돌하는 영역을 계산한다.

선분과 충돌하는 영역은 x, y, z축으로 나누어 계산하고 이 영역들이 모두 겹치는 영역이 있을 경우 충돌로 판정한다.



<svg xmlns="http://www.w3.org/2000/svg" width="662" height="267.8000183105469" style="
        width:662px;
        height:267.8000183105469px;
        background: white;
        fill: none;
">
        <svg xmlns="http://www.w3.org/2000/svg"><g><defs><pattern id=".17961990918134596" width="10" height="10" patternUnits="userSpaceOnUse"><path d="M 10 0 L 0 0 0 10" fill="none" stroke="lightgray" stroke-width="0.5"/></pattern></defs><rect width="100%" height="100%" fill="url(#.17961990918134596)" stroke="lightgray" stroke-width="0.5"/></g></svg>
        <svg xmlns="http://www.w3.org/2000/svg" class="role-diagram-draw-area"><g class="shapes-region" style="stroke: black; fill: none;"><g class="composite-shape"><defs><!-- react-text: 63988 --> <!-- /react-text --><linearGradient id="_ivtt4wwbo" gradientTransform=" translate(0,0) rotate(90 0.5 0.5)" x1="0" y1="0.5" x2="1" y2="0.5"><!-- react-text: 63990 --> <!-- /react-text --><stop offset="0" style="stop-color: rgba(173, 235, 110, 0.5);"/><stop offset="1" style="stop-color: rgba(255, 255, 255, 0.5);"/></linearGradient></defs><path class="real" d=" M244,97 L584,97 L584,177 L244,177 Z" style="stroke-width: 1; stroke: none; fill: url(&quot;#_ivtt4wwbo&quot;);"/></g><g class="composite-shape"><defs><!-- react-text: 63996 --> <!-- /react-text --><linearGradient id="_6mvkd94d8" gradientTransform=" translate(0,0) rotate(90 0.5 0.5)" x1="0" y1="0.5" x2="1" y2="0.5"><!-- react-text: 63998 --> <!-- /react-text --><stop offset="0" style="stop-color: rgba(243, 197, 189, 0.5);"/><stop offset="1" style="stop-color: rgba(255, 255, 255, 0.5);"/></linearGradient></defs><path class="real" d=" M164,77 L434,77 L434,157 L164,157 Z" style="stroke-width: 1; stroke: none; fill: url(&quot;#_6mvkd94d8&quot;);"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M431,77 L164,77" style="stroke: rgb(208, 2, 27); stroke-width: 2; fill: none;"/><g stroke="rgba(208,2,27,1)" fill="rgba(208,2,27,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,164,77.00000000000001)" style="stroke: rgb(208, 2, 27); fill: rgb(208, 2, 27); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g><g stroke="none" fill="rgba(208,2,27,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,434,77)" style="stroke: none; fill: rgb(208, 2, 27); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M581,97 L244,97" style="stroke: rgb(126, 211, 33); stroke-width: 2; fill: none;"/><g stroke="rgba(126,211,33,1)" fill="rgba(126,211,33,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,244,97)" style="stroke: rgb(126, 211, 33); fill: rgb(126, 211, 33); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g><g stroke="none" fill="rgba(126,211,33,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,584,97.00000000000001)" style="stroke: none; fill: rgb(126, 211, 33); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M631,207 L114,207" style="stroke: rgb(245, 166, 35); stroke-width: 2; fill: none;"/><g stroke="rgba(245,166,35,1)" fill="rgba(245,166,35,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,114,207)" style="stroke: rgb(245, 166, 35); fill: rgb(245, 166, 35); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g><g stroke="none" fill="rgba(245,166,35,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,634,206.99999999999997)" style="stroke: none; fill: rgb(245, 166, 35); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M164,77 L164,227" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M434,77 L434,227" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M194,127 L194,227" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M244,47 L244,227" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M584,97 L584,227" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="composite-shape"><defs><!-- react-text: 64043 --> <!-- /react-text --><pattern id="_ggngjvy4k" x="0" y="0" width="14.142135623730951" height="14.142135623730951" patternTransform="rotate(-45,0,0)" patternUnits="userSpaceOnUse"><path d="M0,0 L0,14.142135623730951" style="stroke: rgb(137, 137, 137); stroke-width: 1; fill: none;"/><path d="M7.0710678118654755,0 L7.0710678118654755,14.142135623730951" style="stroke: rgb(137, 137, 137); stroke-width: 1; fill: none;"/><path d="M14.142135623730951,0 L14.142135623730951,14.142135623730951" style="stroke: rgb(137, 137, 137); stroke-width: 1; fill: none;"/></pattern></defs><path class="real" d=" M244,97 L434,97 L434,207 L244,207 Z" style="stroke-width: 1; stroke: none; fill: url(&quot;#_ggngjvy4k&quot;);"/></g><g class="composite-shape"><defs><!-- react-text: 64051 --> <!-- /react-text --><linearGradient id="_jso19pn1j" gradientTransform=" translate(0,0) rotate(90 0.5 0.5)" x1="0" y1="0.5" x2="1" y2="0.5"><!-- react-text: 64053 --> <!-- /react-text --><stop offset="0" style="stop-color: rgba(155, 155, 155, 0.2);"/><stop offset="1" style="stop-color: rgba(255, 255, 255, 0);"/></linearGradient></defs><path class="real" d=" M244,127 L314,127 L314,207 L244,207 Z" style="stroke-width: 1; stroke: none; fill: url(&quot;#_jso19pn1j&quot;);"/></g><g class="composite-shape"><defs><!-- react-text: 64059 --> <!-- /react-text --><linearGradient id="_od3ti5y7w" gradientTransform=" translate(0,0) rotate(90 0.5 0.5)" x1="0" y1="0.5" x2="1" y2="0.5"><!-- react-text: 64061 --> <!-- /react-text --><stop offset="0" style="stop-color: rgba(154, 193, 239, 0.5);"/><stop offset="1" style="stop-color: rgba(255, 255, 255, 0.5);"/></linearGradient></defs><path class="real" d=" M194,127 L314,127 L314,207 L194,207 Z" style="stroke-width: 1; stroke: none; fill: url(&quot;#_od3ti5y7w&quot;);"/></g><g class="composite-shape"><defs><!-- react-text: 64067 --> <!-- /react-text --><pattern id="_ikeloiiiz" x="0" y="0" width="14.142135623730951" height="14.142135623730951" patternTransform="rotate(45,0,0)" patternUnits="userSpaceOnUse"><path d="M0,0 L0,14.142135623730951" style="stroke: rgb(154, 154, 154); stroke-width: 1; fill: none;"/><path d="M7.0710678118654755,0 L7.0710678118654755,14.142135623730951" style="stroke: rgb(154, 154, 154); stroke-width: 1; fill: none;"/><path d="M14.142135623730951,0 L14.142135623730951,14.142135623730951" style="stroke: rgb(154, 154, 154); stroke-width: 1; fill: none;"/></pattern></defs><path class="real" d=" M244,127 L314,127 L314,207 L244,207 Z" style="stroke-width: 1; stroke: none; fill: url(&quot;#_ikeloiiiz&quot;);"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M311,127 L194,127" style="stroke: rgb(74, 144, 226); stroke-width: 2; fill: none;"/><g stroke="rgba(74,144,226,1)" fill="rgba(74,144,226,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,193.99999999999997,127)" style="stroke: rgb(74, 144, 226); fill: rgb(74, 144, 226); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g><g stroke="none" fill="rgba(74,144,226,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,314,126.99999999999999)" style="stroke: none; fill: rgb(74, 144, 226); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M311,227 L244,227" style="stroke: rgb(74, 74, 74); stroke-width: 2; fill: none;"/><g stroke="rgba(74,74,74,1)" fill="rgba(74,74,74,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,243.99999999999997,227.00000000000003)" style="stroke: rgb(74, 74, 74); fill: rgb(74, 74, 74); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g><g stroke="none" fill="rgba(74,74,74,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,314,227.00000000000003)" style="stroke: none; fill: rgb(74, 74, 74); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M114,207 L114,227" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M634,207 L634,227" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="6 6" d="  M244,47 L244,227" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="6 6" d="  M314,47 L314,227" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="intersections-group"><g style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g></g><g/><g/><!-- react-empty: 70368 --></svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="660" height="265.8000183105469" style="width:660px;height:265.8000183105469px;font-family:Asana-Math, Asana;background:white;"><g><g><text x="20.1624755859375" y="70.19999694824219" style="white-space:pre;stroke:none;fill:rgb(208, 2, 27);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(208, 2, 27);">x축의 충돌영역</text></g></g><g><g><text x="20.1624755859375" y="98.20001220703125" style="white-space:pre;stroke:none;fill:rgb(65, 117, 5);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(65, 117, 5);">y축의 충돌영역</text></g></g><g><g><text x="20.1624755859375" y="128.20001220703125" style="white-space:pre;stroke:none;fill:rgb(74, 144, 226);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 144, 226);">z축의 충돌영역</text></g></g><g><g><text x="35.9124755859375" y="199.20001220703125" style="white-space:pre;stroke:none;fill:rgb(245, 166, 35);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(245, 166, 35);">선분 전체</text></g></g><g><g><text x="195.7437744140625" y="239.20001220703125" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">모든 축과 충돌하는 영역</text></g></g><g><g><text x="197.15625" y="217.20001220703125" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">t_min</text></g></g><g><g><text x="323.07501220703125" y="219.20001220703125" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">t_max</text></g></g><g><g><text x="106.36248779296875" y="227.20001220703125" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">t=0</text></g></g><g><g><text x="626.3624877929688" y="227.20001220703125" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">t=1</text></g></g><g><g><text x="151.9937744140625" y="11" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:18px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">선분과 박스의 모든 축에 대한 충돌 영역 겹칩</text></g></g><g><g><text x="141.90625" y="50.19999694824219" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">tx_min</text></g></g><g><g><text x="412.32501220703125" y="50.19999694824219" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">tx_max</text></g></g><g><g><text x="191.90625" y="90.20001220703125" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">ty_min</text></g></g><g><g><text x="592.3250122070312" y="90.20001220703125" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">ty_max</text></g></g><g><g><text x="141.90625" y="120.20001220703125" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">tz_min</text></g></g><g><g><text x="319.32501220703125" y="122.20001220703125" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">tz_max</text></g></g></svg>
</svg>



1. 박스의 x축과 선분의 충돌 영역 tx_min, tx_max를 구하고 이 값이 0~1 사이에 있다면 이 값으로 t_min, t_max 값을 갱신한다.
2. y, x축에 대해서도 같은 과정을 거친다.
3. 최종적으로 모든 축과 겹치는 t_min, t_max 값이 나온다.
4. 이 값으로 다음 조건에 따라 충돌 판정을 내린다.



<svg xmlns="http://www.w3.org/2000/svg" width="662" height="712.2000122070312" style="
        width:662px;
        height:712.2000122070312px;
        background: white;
        fill: none;
">
        <svg xmlns="http://www.w3.org/2000/svg" class="role-diagram-draw-area"><g class="shapes-region" style="stroke: black; fill: none;"><g class="composite-shape"><path class="real" d=" M236.1,283.44 L248.2,295.54 L239.12,304.62 L248.2,313.7 L236.1,325.8 L227.02,316.72 L217.94,325.8 L205.84,313.7 L214.92,304.62 L205.84,295.54 L217.94,283.44 L227.02,292.52 Z" style="stroke-width: 1; stroke: none; fill: rgb(255, 185, 185);"/></g><g class="composite-shape"><path class="real" d=" M187.3,166.8 L264.7,166.8 L264.7,248.66 L187.3,248.66 Z" style="stroke-width: 2; stroke: rgb(74, 74, 74); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M294.7,237.2 L152.5,186.2" style="stroke: rgb(245, 166, 35); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M318.88,246.16 L286.85,234.36" style="stroke: rgb(245, 166, 35); stroke-width: 2; fill: none;"/><g stroke="rgba(245,166,35,1)" transform="matrix(-0.9383724337762651,-0.3456257738201955,0.3456257738201955,-0.9383724337762651,283.6999816894531,233.1999969482422)" style="stroke: rgb(245, 166, 35); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g><g stroke="none" fill="rgba(245,166,35,1)" transform="matrix(-0.9383724337762651,-0.3456257738201955,0.3456257738201955,-0.9383724337762651,321.6999816894531,247.1999969482422)" style="stroke: none; fill: rgb(245, 166, 35); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="composite-shape"><path class="real" d=" M384.3,166.8 L461.7,166.8 L461.7,248.66 L384.3,248.66 Z" style="stroke-width: 2; stroke: rgb(74, 74, 74); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M491.7,237.2 L349.5,186.2" style="stroke: rgb(245, 166, 35); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M417.44,210.57 L352.32,187.21" style="stroke: rgb(245, 166, 35); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(245,166,35,1)" transform="matrix(0.9412939131007876,0.3375881650167952,-0.3375881650167952,0.9412939131007876,349.5,186.1999969482422)" style="stroke: none; fill: rgb(245, 166, 35); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g><g stroke="rgba(245,166,35,1)" transform="matrix(-0.9412939131007878,-0.3375881650167945,0.3375881650167945,-0.9412939131007878,420.5999908447265,211.6999969482422)" style="stroke: rgb(245, 166, 35); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g></g><g class="composite-shape"><path class="real" d=" M543.3,165.8 L620.7,165.8 L620.7,247.66 L543.3,247.66 Z" style="stroke-width: 2; stroke: rgb(74, 74, 74); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M650.7,236.2 L508.5,185.2" style="stroke: rgb(245, 166, 35); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M590.32,214.84 L563.62,205.03" style="stroke: rgb(245, 166, 35); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(245,166,35,1)" transform="matrix(0.9386736918189149,0.3448067578906318,-0.3448067578906318,0.9386736918189149,560.7999979654948,204.0000025431315)" style="stroke: none; fill: rgb(245, 166, 35); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g><g stroke="rgba(245,166,35,1)" transform="matrix(-0.9386736918189144,-0.3448067578906332,0.3448067578906332,-0.9386736918189144,593.4666646321614,216.00000254313153)" style="stroke: rgb(245, 166, 35); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M189.7,260.2 L283.7,260.2" style="stroke: rgb(208, 2, 27); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(208,2,27,1)" transform="matrix(1,0,0,1,186.69998168945312,260.1999969482422)" style="stroke: none; fill: rgb(208, 2, 27); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M283.7,270.2 L267.7,270.2" style="stroke: rgb(74, 144, 226); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(74,144,226,1)" transform="matrix(1,-2.4492935982947064e-16,2.4492935982947064e-16,1,264.6999816894531,270.1999969482422)" style="stroke: none; fill: rgb(74, 144, 226); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M198.7,81.2 L113.86,81.2" style="stroke: rgb(245, 166, 35); stroke-width: 2; fill: none;"/><g stroke="rgba(245,166,35,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,110.49999999999999,81.1999969482422)" style="stroke: rgb(245, 166, 35); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g><g stroke="none" fill="rgba(245,166,35,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,201.69998168945312,81.19999694824219)" style="stroke: none; fill: rgb(245, 166, 35); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M387.7,259.2 L419.7,259.2" style="stroke: rgb(208, 2, 27); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(208,2,27,1)" transform="matrix(1,0,0,1,384.6999816894531,259.1999969482422)" style="stroke: none; fill: rgb(208, 2, 27); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M283.7,233.2 L283.7,281.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M349.5,186.2 L349.5,280.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M459.7,270.2 L419.7,270.2" style="stroke: rgb(74, 144, 226); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(74,144,226,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,462.69998168945307,270.19999694824224)" style="stroke: none; fill: rgb(74, 144, 226); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M593.47,216 L593.47,280" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M546.7,259.53 L593.47,259.53" style="stroke: rgb(208, 2, 27); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(208,2,27,1)" transform="matrix(1,0,0,1,543.6999816894531,259.5333302815755)" style="stroke: none; fill: rgb(208, 2, 27); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M593.47,270 L617.3,270" style="stroke: rgb(74, 144, 226); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(74,144,226,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,620.3000183105469,270.00000254313153)" style="stroke: none; fill: rgb(74, 144, 226); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M321.7,247.2 L321.7,281.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M420.6,211.7 L420.6,279.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M560.8,204 L560.8,280.67" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M330.7,81.2 L242.5,81.2" style="stroke: rgb(208, 2, 27); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(208,2,27,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,333.6999816894531,81.19999694824217)" style="stroke: none; fill: rgb(208, 2, 27); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M457.7,81.2 L369.5,81.2" style="stroke: rgb(74, 144, 226); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(74,144,226,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,460.6999816894531,81.19999694824219)" style="stroke: none; fill: rgb(74, 144, 226); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="composite-shape"><path class="real" d=" M187.3,348.8 L264.7,348.8 L264.7,430.66 L187.3,430.66 Z" style="stroke-width: 2; stroke: rgb(74, 74, 74); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M292.82,418.52 L152.5,368.2" style="stroke: rgb(245, 166, 35); stroke-width: 1; fill: none;"/><g stroke="none" fill="rgba(245,166,35,1)" transform="matrix(-0.9412939131007878,-0.3375881650167945,0.3375881650167945,-0.9412939131007878,294.6999816894531,419.19999694824224)" style="stroke: none; fill: rgb(245, 166, 35); stroke-width: 1;"><path d=" M8.93,-4.29 L0,0 L8.93,4.29 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M291.88,418.19 L226.76,394.83" style="stroke: rgb(245, 166, 35); stroke-width: 2; fill: none;"/><g stroke="rgba(245,166,35,1)" transform="matrix(-0.9412939131007878,-0.3375881650167945,0.3375881650167945,-0.9412939131007878,223.59999084472656,393.6999969482422)" style="stroke: rgb(245, 166, 35); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g><g stroke="none" fill="rgba(245,166,35,1)" transform="matrix(-0.9412939131007878,-0.3375881650167945,0.3375881650167945,-0.9412939131007878,294.6999816894531,419.19999694824224)" style="stroke: none; fill: rgb(245, 166, 35); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="composite-shape"><path class="real" d=" M384.3,348.8 L461.7,348.8 L461.7,430.66 L384.3,430.66 Z" style="stroke-width: 2; stroke: rgb(74, 74, 74); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M489.82,418.52 L349.5,368.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/><g stroke="none" fill="rgba(0,0,0,1)" transform="matrix(-0.9412939131007878,-0.3375881650167945,0.3375881650167945,-0.9412939131007878,491.6999816894531,419.1999969482422)" style="stroke: none; fill: rgb(0, 0, 0); stroke-width: 1;"><path d=" M8.93,-4.29 L0,0 L8.93,4.29 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M488.88,418.19 L352.66,369.33" style="stroke: rgb(245, 166, 35); stroke-width: 2; fill: none;"/><g stroke="rgba(245,166,35,1)" transform="matrix(-0.9412939131007878,-0.3375881650167945,0.3375881650167945,-0.9412939131007878,349.50000000000006,368.1999969482422)" style="stroke: rgb(245, 166, 35); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g><g stroke="none" fill="rgba(245,166,35,1)" transform="matrix(-0.9412939131007878,-0.3375881650167945,0.3375881650167945,-0.9412939131007878,491.6999816894531,419.1999969482422)" style="stroke: none; fill: rgb(245, 166, 35); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="composite-shape"><path class="real" d=" M543.3,347.8 L620.7,347.8 L620.7,429.66 L543.3,429.66 Z" style="stroke-width: 2; stroke: rgb(74, 74, 74); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M650.7,418.2 L508.5,367.2" style="stroke: rgb(245, 166, 35); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M647.54,417.07 L582.42,393.71" style="stroke: rgb(245, 166, 35); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(245,166,35,1)" transform="matrix(0.9412939131007876,0.3375881650167952,-0.3375881650167952,0.9412939131007876,579.5999908447266,392.6999969482422)" style="stroke: none; fill: rgb(245, 166, 35); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g><g stroke="rgba(245,166,35,1)" transform="matrix(-0.9412939131007878,-0.3375881650167945,0.3375881650167945,-0.9412939131007878,650.6999816894531,418.1999969482422)" style="stroke: rgb(245, 166, 35); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M189.7,442.2 L222.6,442.2" style="stroke: rgb(208, 2, 27); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(208,2,27,1)" transform="matrix(1,0,0,1,186.69998168945312,442.1999969482422)" style="stroke: none; fill: rgb(208, 2, 27); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M223,453 L262.7,452.26" style="stroke: rgb(74, 144, 226); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(74,144,226,1)" transform="matrix(-0.9998256268259461,0.01867393750937348,-0.01867393750937348,-0.9998256268259461,265.69998168945307,452.1999969482422)" style="stroke: none; fill: rgb(74, 144, 226); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M379.7,443.2 L349.5,443.2" style="stroke: rgb(208, 2, 27); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(208,2,27,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,382.69998168945307,443.19999694824224)" style="stroke: none; fill: rgb(208, 2, 27); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M223.6,393.7 L223.6,462.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M349.5,368.2 L349.5,462.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M349.5,452.2 L459.7,452.2" style="stroke: rgb(74, 144, 226); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(74,144,226,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,462.69998168945307,452.19999694824224)" style="stroke: none; fill: rgb(74, 144, 226); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M650.7,418.2 L650.7,461.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M546.7,442.2 L650.7,442.2" style="stroke: rgb(208, 2, 27); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(208,2,27,1)" transform="matrix(1,0,0,1,543.6999816894531,442.1999969482422)" style="stroke: none; fill: rgb(208, 2, 27); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M650.7,452.2 L622.7,452.2" style="stroke: rgb(74, 144, 226); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(74,144,226,1)" transform="matrix(1,-2.4492935982947064e-16,2.4492935982947064e-16,1,619.6999816894531,452.1999969482422)" style="stroke: none; fill: rgb(74, 144, 226); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M294.7,419.2 L294.7,462.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M491.7,419.2 L491.7,462.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M579.6,392.7 L579.6,462.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M186.3,151.2 L186.3,280.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M263.3,151.2 L263.3,280.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M383.3,153.2 L383.3,282.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M460.3,152.2 L460.3,281.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M542.3,152.2 L542.3,281.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M620.3,152.2 L620.3,281.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M187.3,334.2 L187.3,463.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M264.3,334.2 L264.3,463.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M384.3,336.2 L384.3,465.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M461.3,335.2 L461.3,464.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M543.3,335.2 L543.3,464.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M621.3,335.2 L621.3,464.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M30,100 L652.7,100" style="stroke: rgb(155, 155, 155); stroke-width: 1; fill: none;"/></g><g class="composite-shape"><path class="real" d=" M411.76,303.3 C411.76,298.42 415.72,294.46 420.6,294.46 C425.48,294.46 429.44,298.42 429.44,303.3 C429.44,308.18 425.48,312.14 420.6,312.14 C415.72,312.14 411.76,308.18 411.76,303.3 M398.5,303.3 C398.5,291.09 408.39,281.2 420.6,281.2 C432.81,281.2 442.7,291.09 442.7,303.3 C442.7,315.51 432.81,325.4 420.6,325.4 C408.39,325.4 398.5,315.51 398.5,303.3" style="stroke-width: 1; stroke: none; fill: rgb(176, 215, 255); fill-rule: evenodd;"/></g><g class="composite-shape"><path class="real" d=" M576.76,303.3 C576.76,298.42 580.72,294.46 585.6,294.46 C590.48,294.46 594.44,298.42 594.44,303.3 C594.44,308.18 590.48,312.14 585.6,312.14 C580.72,312.14 576.76,308.18 576.76,303.3 M563.5,303.3 C563.5,291.09 573.39,281.2 585.6,281.2 C597.81,281.2 607.7,291.09 607.7,303.3 C607.7,315.51 597.81,325.4 585.6,325.4 C573.39,325.4 563.5,315.51 563.5,303.3" style="stroke-width: 1; stroke: none; fill: rgb(176, 215, 255); fill-rule: evenodd;"/></g><g class="composite-shape"><path class="real" d=" M411.76,487.3 C411.76,482.42 415.72,478.46 420.6,478.46 C425.48,478.46 429.44,482.42 429.44,487.3 C429.44,492.18 425.48,496.14 420.6,496.14 C415.72,496.14 411.76,492.18 411.76,487.3 M398.5,487.3 C398.5,475.09 408.39,465.2 420.6,465.2 C432.81,465.2 442.7,475.09 442.7,487.3 C442.7,499.51 432.81,509.4 420.6,509.4 C408.39,509.4 398.5,499.51 398.5,487.3" style="stroke-width: 1; stroke: none; fill: rgb(176, 215, 255); fill-rule: evenodd;"/></g><g class="composite-shape"><path class="real" d=" M576.76,487.3 C576.76,482.42 580.72,478.46 585.6,478.46 C590.48,478.46 594.44,482.42 594.44,487.3 C594.44,492.18 590.48,496.14 585.6,496.14 C580.72,496.14 576.76,492.18 576.76,487.3 M563.5,487.3 C563.5,475.09 573.39,465.2 585.6,465.2 C597.81,465.2 607.7,475.09 607.7,487.3 C607.7,499.51 597.81,509.4 585.6,509.4 C573.39,509.4 563.5,499.51 563.5,487.3" style="stroke-width: 1; stroke: none; fill: rgb(176, 215, 255); fill-rule: evenodd;"/></g><g class="composite-shape"><path class="real" d=" M214.76,486.3 C214.76,481.42 218.72,477.46 223.6,477.46 C228.48,477.46 232.44,481.42 232.44,486.3 C232.44,491.18 228.48,495.14 223.6,495.14 C218.72,495.14 214.76,491.18 214.76,486.3 M201.5,486.3 C201.5,474.09 211.39,464.2 223.6,464.2 C235.81,464.2 245.7,474.09 245.7,486.3 C245.7,498.51 235.81,508.4 223.6,508.4 C211.39,508.4 201.5,498.51 201.5,486.3" style="stroke-width: 1; stroke: none; fill: rgb(176, 215, 255); fill-rule: evenodd;"/></g><g class="composite-shape"><path class="real" d=" M187.3,529.8 L264.7,529.8 L264.7,611.66 L187.3,611.66 Z" style="stroke-width: 2; stroke: rgb(74, 74, 74); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M294.7,600.2 L152.5,549.2" style="stroke: rgb(245, 166, 35); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M247.5,582.87 L218.11,572.79" style="stroke: rgb(245, 166, 35); stroke-width: 2; fill: none;"/><g stroke="rgba(245,166,35,1)" transform="matrix(-0.9459156263843979,-0.3244127429091098,0.3244127429091098,-0.9459156263843979,214.93332417805988,571.6999969482422)" style="stroke: rgb(245, 166, 35); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g><g stroke="none" fill="rgba(245,166,35,1)" transform="matrix(-0.9459156263843979,-0.3244127429091098,0.3244127429091098,-0.9459156263843979,250.33333333333334,583.84375)" style="stroke: none; fill: rgb(245, 166, 35); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="composite-shape"><path class="real" d=" M384.3,529.8 L461.7,529.8 L461.7,611.66 L384.3,611.66 Z" style="stroke-width: 2; stroke: rgb(74, 74, 74); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M491.7,600.2 L349.5,549.2" style="stroke: rgb(245, 166, 35); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M429.84,577.51 L352.66,550.32" style="stroke: rgb(245, 166, 35); stroke-width: 2; fill: none;"/><g stroke="rgba(245,166,35,1)" transform="matrix(-0.9431646705278075,-0.33232575023337024,0.33232575023337024,-0.9431646705278075,349.5,549.1999969482422)" style="stroke: rgb(245, 166, 35); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g><g stroke="none" fill="rgba(245,166,35,1)" transform="matrix(-0.9431646705278075,-0.33232575023337024,0.33232575023337024,-0.9431646705278075,432.6666666666666,578.5104166666667)" style="stroke: none; fill: rgb(245, 166, 35); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="composite-shape"><path class="real" d=" M543.3,528.8 L620.7,528.8 L620.7,610.66 L543.3,610.66 Z" style="stroke-width: 2; stroke: rgb(74, 74, 74); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M650.7,599.2 L508.5,548.2" style="stroke: rgb(245, 166, 35); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M647.54,598.08 L632.83,592.85" style="stroke: rgb(245, 166, 35); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(245,166,35,1)" transform="matrix(0.9422914125695194,0.33479380788440466,-0.33479380788440466,0.9422914125695194,630,591.84375)" style="stroke: none; fill: rgb(245, 166, 35); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g><g stroke="rgba(245,166,35,1)" transform="matrix(-0.9422914125695191,-0.3347938078844056,0.3347938078844056,-0.9422914125695191,650.6999816894532,599.1999969482423)" style="stroke: rgb(245, 166, 35); stroke-width: 2;"><circle cx="0" cy="0" r="4.355"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M189.7,623.2 L216,623.2" style="stroke: rgb(208, 2, 27); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(208,2,27,1)" transform="matrix(1,0,0,1,186.69998168945312,623.1999969482422)" style="stroke: none; fill: rgb(208, 2, 27); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M215.33,633.2 L262.7,633.2" style="stroke: rgb(74, 144, 226); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(74,144,226,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,265.69998168945307,633.1999969482422)" style="stroke: none; fill: rgb(74, 144, 226); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M379.7,624.2 L349.5,624.2" style="stroke: rgb(208, 2, 27); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(208,2,27,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,382.69998168945307,624.1999969482422)" style="stroke: none; fill: rgb(208, 2, 27); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M214.93,571.7 L215.33,641.62" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M349.5,549.2 L349.5,643.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M349.5,633.2 L459.7,633.2" style="stroke: rgb(74, 144, 226); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(74,144,226,1)" transform="matrix(-1,1.2246467991473532e-16,-1.2246467991473532e-16,-1,462.69998168945307,633.1999969482422)" style="stroke: none; fill: rgb(74, 144, 226); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M650.7,599.2 L650.7,642.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M546.7,623.2 L650.7,623.2" style="stroke: rgb(208, 2, 27); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(208,2,27,1)" transform="matrix(1,0,0,1,543.6999816894531,623.1999969482422)" style="stroke: none; fill: rgb(208, 2, 27); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M650.7,633.2 L622.7,633.2" style="stroke: rgb(74, 144, 226); stroke-width: 2; fill: none;"/><g stroke="none" fill="rgba(74,144,226,1)" transform="matrix(1,-2.4492935982947064e-16,2.4492935982947064e-16,1,619.6999816894531,633.1999969482422)" style="stroke: none; fill: rgb(74, 144, 226); stroke-width: 2;"><path d=" M11.61,-5.58 L0,0 L11.61,5.58 Z"/></g></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M432.67,578.51 L432.67,643.18" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M630,591.84 L630,643.18" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M187.3,515.2 L187.3,644.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M264.3,515.2 L264.3,644.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M384.3,517.2 L384.3,646.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M461.3,516.2 L461.3,645.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M543.3,516.2 L543.3,645.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M621.3,516.2 L621.3,645.2" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="composite-shape"><path class="real" d=" M411.76,668.3 C411.76,663.42 415.72,659.46 420.6,659.46 C425.48,659.46 429.44,663.42 429.44,668.3 C429.44,673.18 425.48,677.14 420.6,677.14 C415.72,677.14 411.76,673.18 411.76,668.3 M398.5,668.3 C398.5,656.09 408.39,646.2 420.6,646.2 C432.81,646.2 442.7,656.09 442.7,668.3 C442.7,680.51 432.81,690.4 420.6,690.4 C408.39,690.4 398.5,680.51 398.5,668.3" style="stroke-width: 1; stroke: none; fill: rgb(176, 215, 255); fill-rule: evenodd;"/></g><g class="composite-shape"><path class="real" d=" M214.76,667.3 C214.76,662.42 218.72,658.46 223.6,658.46 C228.48,658.46 232.44,662.42 232.44,667.3 C232.44,672.18 228.48,676.14 223.6,676.14 C218.72,676.14 214.76,672.18 214.76,667.3 M201.5,667.3 C201.5,655.09 211.39,645.2 223.6,645.2 C235.81,645.2 245.7,655.09 245.7,667.3 C245.7,679.51 235.81,689.4 223.6,689.4 C211.39,689.4 201.5,679.51 201.5,667.3" style="stroke-width: 1; stroke: none; fill: rgb(176, 215, 255); fill-rule: evenodd;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M250.33,583.84 L250.33,642.51" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="composite-shape"><path class="real" d=" M594.68,647.12 L606.78,659.22 L597.7,668.3 L606.78,677.38 L594.68,689.48 L585.6,680.4 L576.52,689.48 L564.42,677.38 L573.5,668.3 L564.42,659.22 L576.52,647.12 L585.6,656.2 Z" style="stroke-width: 1; stroke: none; fill: rgb(255, 185, 185);"/></g><g class="composite-shape"><path class="real" d=" M569.8,73.9 C569.8,70.48 572.58,67.7 576,67.7 C579.42,67.7 582.2,70.48 582.2,73.9 C582.2,77.32 579.42,80.1 576,80.1 C572.58,80.1 569.8,77.32 569.8,73.9 M560.5,73.9 C560.5,65.34 567.44,58.4 576,58.4 C584.56,58.4 591.5,65.34 591.5,73.9 C591.5,82.46 584.56,89.4 576,89.4 C567.44,89.4 560.5,82.46 560.5,73.9" style="stroke-width: 1; stroke: none; fill: rgb(176, 215, 255); fill-rule: evenodd;"/></g><g class="composite-shape"><path class="real" d=" M623.35,58.76 L631.85,67.25 L625.48,73.62 L631.85,79.99 L623.35,88.48 L616.99,82.11 L610.62,88.48 L602.13,79.99 L608.5,73.62 L602.13,67.25 L610.62,58.76 L616.99,65.13 Z" style="stroke-width: 1; stroke: none; fill: rgb(255, 185, 185);"/></g><g class="intersections-group"><g style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"><g><g class="intersection-group"><g><circle cx="264.6999816894531" cy="226.44050189189733" r="5"/><circle cx="264.6999816894531" cy="226.44050189189733" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g><g><circle cx="187.30001831054688" cy="198.68101778067683" r="5"/><circle cx="187.30001831054688" cy="198.68101778067683" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g></g><g><g class="intersection-group"><g><circle cx="461.6999816894531" cy="226.44050189189733" r="5"/><circle cx="461.6999816894531" cy="226.44050189189733" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g><g><circle cx="384.3000183105469" cy="198.68101778067683" r="5"/><circle cx="384.3000183105469" cy="198.68101778067683" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g><g class="intersection-group"><g><circle cx="384.3000183105469" cy="198.68101778067683" r="5"/><circle cx="384.3000183105469" cy="198.68101778067683" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g></g><g><g class="intersection-group"><g><circle cx="620.6999816894531" cy="225.44050189189733" r="5"/><circle cx="620.6999816894531" cy="225.44050189189733" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g><g><circle cx="543.3000183105469" cy="197.68101778067683" r="5"/><circle cx="543.3000183105469" cy="197.68101778067683" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g></g><g><g class="intersection-group"><g><circle cx="264.6999816894531" cy="408.4405018918973" r="5"/><circle cx="264.6999816894531" cy="408.4405018918973" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g><g><circle cx="187.30001831054688" cy="380.6810177806768" r="5"/><circle cx="187.30001831054688" cy="380.6810177806768" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g><g class="intersection-group"><g><circle cx="264.6999816894531" cy="408.4405018918973" r="5"/><circle cx="264.6999816894531" cy="408.4405018918973" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g></g><g><g class="intersection-group"><g><circle cx="461.6999816894531" cy="408.4405018918973" r="5"/><circle cx="461.6999816894531" cy="408.4405018918973" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g><g><circle cx="384.3000183105469" cy="380.6810177806768" r="5"/><circle cx="384.3000183105469" cy="380.6810177806768" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g><g class="intersection-group"><g><circle cx="461.6999816894531" cy="408.4405018918973" r="5"/><circle cx="461.6999816894531" cy="408.4405018918973" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g><g><circle cx="384.3000183105469" cy="380.6810177806768" r="5"/><circle cx="384.3000183105469" cy="380.6810177806768" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g></g><g><g class="intersection-group"><g><circle cx="620.6999816894531" cy="407.4405018918973" r="5"/><circle cx="620.6999816894531" cy="407.4405018918973" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g><g><circle cx="543.3000183105469" cy="379.6810177806768" r="5"/><circle cx="543.3000183105469" cy="379.6810177806768" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g><g class="intersection-group"><g><circle cx="620.6999816894531" cy="407.4405018918973" r="5"/><circle cx="620.6999816894531" cy="407.4405018918973" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g></g><g><g class="intersection-group"><g><circle cx="264.6999816894531" cy="589.4405018918974" r="5"/><circle cx="264.6999816894531" cy="589.4405018918974" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g><g><circle cx="187.30001831054688" cy="561.6810177806768" r="5"/><circle cx="187.30001831054688" cy="561.6810177806768" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g></g><g><g class="intersection-group"><g><circle cx="461.6999816894531" cy="589.4405018918974" r="5"/><circle cx="461.6999816894531" cy="589.4405018918974" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g><g><circle cx="384.3000183105469" cy="561.6810177806768" r="5"/><circle cx="384.3000183105469" cy="561.6810177806768" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g><g class="intersection-group"><g><circle cx="384.3000183105469" cy="561.4645637966307" r="5"/><circle cx="384.3000183105469" cy="561.4645637966307" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g></g><g><g class="intersection-group"><g><circle cx="620.6999816894531" cy="588.4405018918974" r="5"/><circle cx="620.6999816894531" cy="588.4405018918974" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g><g><circle cx="543.3000183105469" cy="560.6810177806768" r="5"/><circle cx="543.3000183105469" cy="560.6810177806768" r="5" style="stroke: transparent; stroke-width: 6; fill: none;"/></g></g></g></g></g></g><g/><g/><!-- react-empty: 679 --></svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="660" height="710.2000122070312" style="width:660px;height:710.2000122070312px;font-family:Asana-Math, Asana;background:transparent;"><g><g><text x="172.32501220703125" y="111.60000610351562" style="white-space:pre;stroke:none;fill:rgb(208, 2, 27);font-size:25.92px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(208, 2, 27);">t_min &lt; 0</text></g></g><g><g><text x="33.7249755859375" y="199.60000610351562" style="white-space:pre;stroke:none;fill:rgb(74, 144, 226);font-size:25.92px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 144, 226);">t_max &lt; 0</text></g></g><g><g><text x="342.125" y="113.60000610351562" style="white-space:pre;stroke:none;fill:rgb(208, 2, 27);font-size:25.92px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(208, 2, 27);">0 ⩽ t_min ⩽ 1</text></g></g><g><g><text x="527.3250122070312" y="112.60000610351562" style="white-space:pre;stroke:none;fill:rgb(208, 2, 27);font-size:25.92px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(208, 2, 27);">1 &lt; t_min</text></g></g><g><g><text x="94.7437744140625" y="56" style="white-space:pre;stroke:none;fill:rgb(128, 128, 128);font-size:13.5px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(128, 128, 128);">Start</text></g></g><g><g><text x="181.98748779296875" y="56" style="white-space:pre;stroke:none;fill:rgb(128, 128, 128);font-size:13.5px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(128, 128, 128);">End</text></g></g><g><g><text x="267.65625" y="54.20001220703125" style="white-space:pre;stroke:none;fill:rgb(208, 2, 27);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(208, 2, 27);">t_min</text></g></g><g><g><text x="392.57501220703125" y="54.20001220703125" style="white-space:pre;stroke:none;fill:rgb(74, 144, 226);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 144, 226);">t_max</text></g></g><g><g><text x="7.524993896484375" y="381.6000061035156" style="white-space:pre;stroke:none;fill:rgb(74, 144, 226);font-size:25.92px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 144, 226);">0 ⩽ t_max ⩽ 1</text></g></g><g><g><text x="33.7249755859375" y="562.6000061035156" style="white-space:pre;stroke:none;fill:rgb(74, 144, 226);font-size:25.92px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 144, 226);">1 &lt; t_max</text></g></g><g><g><text x="35.98126220703125" y="71.20004272460938" style="white-space:pre;stroke:none;fill:rgb(245, 166, 35);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(245, 166, 35);">Segment</text></g></g><g><g><text x="491.6500244140625" y="65.20004272460938" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(0, 0, 0);">Collision</text></g></g><g><g><text x="124.9937744140625" y="21" style="white-space:pre;stroke:none;fill:rgb(74, 74, 74);font-size:18px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 74, 74);">선분의 충돌 영역 최소값과 최대값 t에 따른 충돌 판정</text></g></g></svg>
</svg>


###### AABB 구현



```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Segment_AABB_Collision : MonoBehaviour
{
    public Transform B0; // Box0
    public Transform B1; // Box1
    public Transform S0; // Segment0
    public Transform S1; // Segment1

    private void OnDrawGizmos()
    {
        Vector3 b0 = B0.position;
        Vector3 b1 = B1.position;
        Vector3 s0 = S0.position;
        Vector3 s1 = S1.position;
        Vector3 sv = s1 - s0;

        // 선분과 박스의 충돌하는 곳의 최대, 최소값.(직선의 매개변수 방정식의 t값)
        // x, y, z축의 충돌을 검사하며 점점 좁혀나간다.
        float t_min = 0f;
        float t_max = 1f;
        bool hit = false;

        // do while 반복문 영역은 반복을 위한 것이 아니라 조건에 안맞았을 시 바로 빠져나오기 위한 영역. 
        // while (false)이기 때문에 단 한번만 실행된다.
        do
        {
            // x
            float tx_min = 0f;
            float tx_max = 1f;
            if (sv.x == 0f)
            {
                // 선분이 x좌표로 이동하지 않는다는 뜻이므로 선분의 위치가 박스영역 안인지만 확인하면 된다.
                // 그리고 0으로 나누지 않기 위해서도 따로 처리한다.
                if (s0.x < b0.x || s0.x > b1.x) break;
            }
            else
            {
                // 선분과 박스 영역의 x값의 매개변수를 구한다.
                float tx0 = (b0.x - s0.x) / sv.x;
                float tx1 = (b1.x - s0.x) / sv.x;
                // x축의 최소값 최대값을 결정
                tx_min = Mathf.Min(tx0, tx1);
                tx_max = Mathf.Max(tx0, tx1);
                // 최소, 최대값이 영역을 벗어났는지 확인
                if (tx_max < 0f || tx_min > 1) break;

                Gizmos.color = Color.red;
                Gizmos.DrawWireSphere(s0 + (sv * tx0), 0.3f);
                Gizmos.DrawWireCube(s0 + (sv * tx1), Vector3.one * 0.55f);
            }
            // t_min이 x축의 최대(tx_max)보다 크다는 것은 다른축과 겹치는 영역이 없다는 것이기 때문에 종료한다.
            // t_max가 x축의 최소(tx_min)보다 작다는 것은 다른축과 겹치는 영역이 없다는 것이기 때문에 종료한다.
            if (t_min > tx_max || t_max < tx_min) break;

            // t_min, t_max 값을 tx_min, tx_max 값으로 갱신한다.
            // 현재 최소값보다 x축의 최소값이 크면 x축의 최소값으로 갱신한다.(겹치는 영역을 좁혀나간다.)
            t_min = Mathf.Max(t_min, tx_min);
            // 현재 최대값보다 x축의 최대값이 크면 x축의 최소값으로 갱신한다.(겹치는 영역을 좁혀나간다.)
            t_max = Mathf.Min(t_max, tx_max);
            // 여기서 t_min, t_max 값은 초기값이기 때문에 tx_min, tx_max 을 바로 넣어도 되지만 일관성을 위해 y, z와 똑같이 처리한다.

            // y
            // x와 똑같이 처리한다.
            float ty_min = 0f;
            float ty_max = 1f;
            if (sv.y == 0f)
            {
                if (s0.y < b0.y || s0.y > b1.y) break;
            }
            else
            {
                float ty0 = (b0.y - s0.y) / sv.y;
                float ty1 = (b1.y - s0.y) / sv.y;
                ty_min = Mathf.Min(ty0, ty1);
                ty_max = Mathf.Max(ty0, ty1);

                if (ty_max < 0f || ty_min > 1) break;

                Gizmos.color = Color.red;
                Gizmos.DrawWireSphere(s0 + (sv * ty0), 0.3f);
                Gizmos.DrawWireCube(s0 + (sv * ty1), Vector3.one * 0.55f);
            }
            if (t_max < ty_min || t_min > ty_max) break;
            t_min = Mathf.Max(t_min, ty_min);
            t_max = Mathf.Min(t_max, ty_max);

            // z
            // x와 똑같이 처리한다.
            float tz_min = 0f;
            float tz_max = 1f;
            if (sv.z == 0f)
            {
                if (s0.z < b0.z || s0.z > b1.z) break;
            }
            else
            {
                float tz0 = (b0.z - s0.z) / sv.z;
                float tz1 = (b1.z - s0.z) / sv.z;
                tz_min = Mathf.Min(tz0, tz1);
                tz_max = Mathf.Max(tz0, tz1);

                if (tz_max < 0f || tz_min > 1) break;

                Gizmos.color = Color.red;
                Gizmos.DrawWireSphere(s0 + (sv * tz0), 0.3f);
                Gizmos.DrawWireCube(s0 + (sv * tz1), Vector3.one * 0.55f);
            }
            if (t_max < tz_min || t_min > tz_max) break;
            t_min = Mathf.Max(t_min, tz_min);
            t_max = Mathf.Min(t_max, tz_max);

            // 최종 t값이 0~1 사이에 있는지 확인
            //hit = !(t_min > 1f || t_max < 0);
            hit = (t_min <= 1f && t_max >= 0);
        } while (false);

        // 선분 그리기
        Gizmos.color = Color.yellow;
        Gizmos.DrawLine(s0, s1);
        Gizmos.DrawLine(s0, s0 + Vector3.up);
        Gizmos.DrawLine(s1, s1 + Vector3.up);

        // 충돌 영역을 선분에 겹쳐 그린다.
        if (hit)
        {
            Gizmos.color = Color.white;
            Gizmos.DrawLine(s0 + (sv * t_min), s0 + (sv * t_max));
            Gizmos.DrawLine(s0 + (sv * t_min), s0 + (sv * t_min) + Vector3.up);
            Gizmos.DrawLine(s0 + (sv * t_max), s0 + (sv * t_max) + Vector3.up);
        }

        // 상자 그리기
        // 각 축별로 앞위왼 -> 뒤위오 순으로 그린다.
        // x축
        Gizmos.color = Color.red;
        Gizmos.DrawLine(new Vector3(b0.x, b1.y, b0.z), new Vector3(b1.x, b1.y, b0.z));
        Gizmos.DrawLine(b0, new Vector3(b1.x, b0.y, b0.z));
        Gizmos.DrawLine(new Vector3(b0.x, b1.y, b1.z), b1);
        Gizmos.DrawLine(new Vector3(b0.x, b0.y, b1.z), new Vector3(b1.x, b0.y, b1.z));

        // y축
        Gizmos.color = Color.green;
        Gizmos.DrawLine(new Vector3(b0.x, b1.y, b0.z), b0);
        Gizmos.DrawLine(new Vector3(b1.x, b1.y, b0.z), new Vector3(b1.x, b0.y, b0.z));
        Gizmos.DrawLine(new Vector3(b0.x, b1.y, b1.z), new Vector3(b0.x, b0.y, b1.z));
        Gizmos.DrawLine(b1, new Vector3(b1.x, b0.y, b1.z));

        // z축
        Gizmos.color = Color.blue;
        Gizmos.DrawLine(new Vector3(b0.x, b1.y, b0.z), new Vector3(b0.x, b1.y, b1.z));
        Gizmos.DrawLine(b0, new Vector3(b0.x, b0.y, b1.z));
        Gizmos.DrawLine(new Vector3(b1.x, b1.y, b0.z), b1);
        Gizmos.DrawLine(new Vector3(b1.x, b0.y, b0.z), new Vector3(b1.x, b0.y, b1.z));
    }
}

```



###### AABB 작동화면 캡쳐

![](https://raw.githubusercontent.com/lazyartist/blog/master/images/AABB.gif)







#### OBB(Oriented Bounding Box)

###### OBB 바운딩 박스의 정의

1. (0, 0) 위치에 있는 크기 1인 기본 상자
2. 이 상자의 크기, 회전, 위치를 조절한 변형된 상자가 최종 바운딩 박스
3. 데이터 구조는 다음 두 개의 매트릭스로 정의
   1. 크기, 회전, 위치를 변형시킬 행렬
   2. 기본 상자의 좌표계로 변형시킬 역행렬



###### OBB의 충돌 검출 이론

1. 바운딩 박스와 충돌 검출할 선분을 바운딩 박스의 원래 좌표계로 변형

   1. 이 때 바운딩 박스에 저장된 역행렬을 이용한다.
2. 변형된 선분과 기본 바운딩 박스의 충돌을 검출
   1. 충돌 검출에는 AABB 방식을 사용한다.


<svg xmlns="http://www.w3.org/2000/svg" width="662" height="208.1875" style="
        width:662px;
        height:208.1875px;
        background: white;
        fill: none;
">
        <svg xmlns="http://www.w3.org/2000/svg"><g><defs><pattern id=".27087992909080394" width="10" height="10" patternUnits="userSpaceOnUse"><path d="M 10 0 L 0 0 0 10" fill="none" stroke="lightgray" stroke-width="0.5"/></pattern></defs><rect width="100%" height="100%" fill="url(#.27087992909080394)" stroke="lightgray" stroke-width="0.5"/></g></svg>
        <svg xmlns="http://www.w3.org/2000/svg" class="role-diagram-draw-area"><g class="shapes-region" style="stroke: black; fill: none;"><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M100,110 L210,110 M111,20 L111,120"/><path d=" M203,105 L210,110 L203,115"/><path d=" M106,27 L111,20 L116,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M111,110 L71.43,148.6" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/><g stroke="#000" transform="matrix(0.7158146192652641,-0.6982903628478091,0.6982903628478091,0.7158146192652641,70,150)" style="stroke: rgb(0, 0, 0); stroke-width: 1;"><path d=" M10.93,-4.9 Q4.96,-1 0,0 Q4.96,1 10.93,4.9"/></g></g><g class="composite-shape"><path class="real" d=" M148.74,47.29 L173.38,49.12 L200,80 L152.5,120.94 L127.86,119.12 L101.24,88.23 Z" style="stroke-width: 1; stroke: rgb(0, 0, 0); fill: rgb(184, 233, 134);"/><path class="real" d=" M200,80 L175.36,78.17 L148.74,47.29" style="stroke-width: 1; stroke: rgb(0, 0, 0); fill: none;"/><path class="real" d=" M175.36,78.17 L127.86,119.12" style="stroke-width: 1; stroke: rgb(0, 0, 0); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M80,105 L140,80" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M180,65 L240,40" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M490,110 L590,110 M500,20 L500,120"/><path d=" M583,105 L590,110 L583,115"/><path d=" M495,27 L500,20 L505,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M503.6,107 L461.42,148.6" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/><g stroke="#000" transform="matrix(0.7120260459909961,-0.7021530529951628,0.7021530529951628,0.7120260459909961,460,150)" style="stroke: rgb(0, 0, 0); stroke-width: 1;"><path d=" M10.93,-4.9 Q4.96,-1 0,0 Q4.96,1 10.93,4.9"/></g></g><g class="composite-shape"><path class="real" d=" M486.78,81.84 L503.77,64.54 L544.15,64.54 L544.9,106.7 L527.9,124 L487.53,124 Z" style="stroke-width: 1; stroke: rgb(0, 0, 0); fill: rgb(184, 233, 134);"/><path class="real" d=" M544.15,64.54 L527.15,81.84 L486.78,81.84" style="stroke-width: 1; stroke: rgb(0, 0, 0); fill: none;"/><path class="real" d=" M527.15,81.84 L527.9,124" style="stroke-width: 1; stroke: rgb(0, 0, 0); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M493,104 L500.15,90.91" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M507.05,77.23 L520,50" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="composite-shape"><path class="real" d=" M280,22.86 L352,22.86 L352,5.71 L400,40 L352,74.29 L352,57.14 L280,57.14 Z" style="stroke-width: 1; stroke: rgb(255, 255, 255); fill: rgb(219, 235, 255);"/></g><g class="composite-shape"><path class="real" d=" M400,141.43 L328,141.43 L328,158.57 L280,124.29 L328,90 L328,107.14 L400,107.14 Z" style="stroke-width: 1; stroke: rgb(255, 255, 255); fill: rgb(255, 219, 219);"/></g><g class="intersections-group"><g style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g></g><g/><g/><!-- react-empty: 13397 --></svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="660" height="206.1875" style="width:660px;height:206.1875px;font-family:Asana-Math, Asana;background:white;"><g><g><text x="292.32501220703125" y="32.493743896484375" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(0, 0, 0);">역행렬(</text><g><g><g><g style="transform:matrix(1,0,0,1,342.3125,46.29376220703125);"><path d="M937 664L950 695C922 699 775 701 773 692L688 536L442 114L292 692C269 686 146 690 125 692L122 664L148 662C200 658 218 648 218 622C218 616 72 100 70 93C54 41 39 28 -16 23L-19 -3L20 -2C54 -1 79 0 93 0C107 0 133 -1 168 -2L203 -3L206 25L168 28C136 30 119 40 119 55C119 65 121 78 126 96L250 560L399 -18L422 -18L479 86L718 500L770 587L733 67C729 39 717 32 666 28L635 25L632 -3L679 -2C721 -1 751 0 766 0C782 0 812 -1 853 -2L899 -3L902 25L865 28C829 31 811 42 811 63L812 100L853 631C855 650 870 660 899 662Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g><g><g><g style="transform:matrix(1,0,0,1,358.51251220703125,39.80625);"><path d="M555 243L555 299L51 299L51 243ZM1023 -3L1023 27L971 30C916 33 906 44 906 96L906 700L665 598L672 548L822 614L822 96C822 44 811 33 757 30L701 27L701 -3C855 0 855 0 866 0C897 0 1007 -3 1023 -3Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.0119,0,0,-0.0119,0,0);"></path></g></g></g></g></g></g></g><text x="371.6624755859375" y="32.493743896484375" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(0, 0, 0);">)</text></g></g><g><g><text x="306.39373779296875" y="116.07501220703125" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(0, 0, 0);">행렬(</text><g><g><g><g style="transform:matrix(1,0,0,1,341.3812255859375,129.875);"><path d="M937 664L950 695C922 699 775 701 773 692L688 536L442 114L292 692C269 686 146 690 125 692L122 664L148 662C200 658 218 648 218 622C218 616 72 100 70 93C54 41 39 28 -16 23L-19 -3L20 -2C54 -1 79 0 93 0C107 0 133 -1 168 -2L203 -3L206 25L168 28C136 30 119 40 119 55C119 65 121 78 126 96L250 560L399 -18L422 -18L479 86L718 500L770 587L733 67C729 39 717 32 666 28L635 25L632 -3L679 -2C721 -1 751 0 766 0C782 0 812 -1 853 -2L899 -3L902 25L865 28C829 31 811 42 811 63L812 100L853 631C855 650 870 660 899 662Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g><text x="357.59375" y="116.07501220703125" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(0, 0, 0);">)</text></g></g><g><g><text x="422.1624755859375" y="162.20001220703125" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(0, 0, 0);">바운딩 박스의 변형 전 좌표계</text></g></g><g><g><text x="52.1624755859375" y="162.20001220703125" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(0, 0, 0);">바운딩 박스의 변형 후 좌표계</text></g></g></svg>
</svg>


###### OBB의 충돌 검출 구현

> Matrix4 클래스는 Math - Linear Transformation 포스트 참고

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Segment_OBB_Collision : MonoBehaviour
{
    public Transform BoxPosition;
    public Transform S0; // Segment0
    public Transform S1; // Segment1

    public float BoundingBoxSize; // Bounding Box Size
    public Vector3 Scale = new Vector3(1f, 1f, 1f);
    [Range(0, 360)]
    public float RotationX = 0f;
    [Range(0, 360)]
    public float RotationY = 0f;
    [Range(0, 360)]
    public float RotationZ = 0f;

    private void OnDrawGizmos()
    {
        Vector3 position = new Vector3(0f, 0f, 0f);
        float halfSize = BoundingBoxSize / 2;

        // 바운딩 박스의 버텍스를 생성한다.
        Vector3[] boxVertecis = new Vector3[]
        {
            new Vector3(position.x - halfSize, position.y- halfSize, position.z- halfSize),
            new Vector3(position.x + halfSize, position.y- halfSize, position.z- halfSize),
            new Vector3(position.x + halfSize, position.y + halfSize, position.z- halfSize),
            new Vector3(position.x- halfSize, position.y + halfSize, position.z- halfSize),

            new Vector3(position.x- halfSize, position.y- halfSize, position.z + halfSize),
            new Vector3(position.x + halfSize, position.y- halfSize, position.z + halfSize),
            new Vector3(position.x + halfSize, position.y+ halfSize, position.z + halfSize),
            new Vector3(position.x- halfSize, position.y + halfSize, position.z + halfSize),
        };

        // 바운딩 박스를 그린다.
        Color[] colors = new Color[] { Color.white, Color.green, Color.blue, Color.cyan };
        for (int i = 0; i < boxVertecis.Length; i++)
        {
            Gizmos.color = colors[(uint)i / 2];
            Gizmos.DrawWireSphere(boxVertecis[i], 0.1f);
        }

        // 크기 행렬
        Matrix4 sm = Matrix4.CreateScale(Scale.x, Scale.y, Scale.z);
        // 회전 행렬
        Matrix4 rm = Matrix4.CreateRotation(RotationX * Mathf.Deg2Rad, RotationY * Mathf.Deg2Rad, RotationZ * Mathf.Deg2Rad);
        // 이동 행렬
        Matrix4 tm = Matrix4.CreateTranslation(BoxPosition.position.x, BoxPosition.position.y, BoxPosition.position.z);

        // 크기, 회전, 이동 행렬을 조합하여 변환 행렬을 완성한다.
        Matrix4 tsr = tm * rm * sm;  // 변환 행렬의 적용 순서 반대로 곱해준다.
        // 변환 행렬의 역행렬을 구한다.
        Matrix4 tsr_inverse = tsr.Inverse();  // 역행렬

        // 바운딩 박스의 모든 버텍스에 변환행렬을 곱해준다.
        for (int i = 0; i < boxVertecis.Length; i++)
        {
            boxVertecis[i] = tsr * boxVertecis[i];
        }

        // 변환된 바운딩 박스를 그린다.
        for (int i = 0; i < boxVertecis.Length; i++)
        {
            Gizmos.color = colors[(uint)i / 2];
            Gizmos.DrawWireSphere(boxVertecis[i], 0.1f);
        }
        Gizmos.color = Color.white;
        Gizmos.DrawLine(boxVertecis[0], boxVertecis[1]);
        Gizmos.DrawLine(boxVertecis[1], boxVertecis[2]);
        Gizmos.DrawLine(boxVertecis[2], boxVertecis[3]);
        Gizmos.DrawLine(boxVertecis[3], boxVertecis[0]);
        Gizmos.DrawLine(boxVertecis[4], boxVertecis[5]);
        Gizmos.DrawLine(boxVertecis[5], boxVertecis[6]);
        Gizmos.DrawLine(boxVertecis[6], boxVertecis[7]);
        Gizmos.DrawLine(boxVertecis[7], boxVertecis[4]);
        Gizmos.DrawLine(boxVertecis[0], boxVertecis[4]);
        Gizmos.DrawLine(boxVertecis[1], boxVertecis[5]);
        Gizmos.DrawLine(boxVertecis[2], boxVertecis[6]);
        Gizmos.DrawLine(boxVertecis[3], boxVertecis[7]);

        // 바운딩 박스의 모든 버텍스에 변환행렬의 역행렬을 곱하여 원래 좌표계로 돌아가게 한다.
        for (int i = 0; i < boxVertecis.Length; i++)
        {
            boxVertecis[i] = tsr_inverse * boxVertecis[i];
        }

        // 바운딩 박스와 충돌 체크할 선분을 바운딩 박스의 원래 좌표계로 변형한다.
        Vector3 s0 = tsr_inverse * S0.position;
        Vector3 s1 = tsr_inverse *S1.position;

        // 원래 좌표계로 돌아간 바운딩 박스와 선분을 충돌 체크한다.
        bool hit = HitTest(boxVertecis[0], boxVertecis[6], s0, s1);
        
        // 충돌 체크 여부에 따라 선분의 색을 달리하여 그린다.
        Gizmos.color = hit ? Color.red : Color.yellow;
        Gizmos.DrawLine(S0.position, S1.position);
    }

    bool HitTest(Vector3 b0, Vector3 b1, Vector3 s0, Vector3 s1)
    {
        Vector3 sv = s1 - s0;

        // 선분과 박스의 충돌하는 곳의 최대, 최소값.(직선의 매개변수 방정식의 t값)
        // x, y, z축의 충돌을 검사하며 점점 좁혀나간다.
        float t_min = 0f;
        float t_max = 1f;
        bool hit = false;

        // do while 반복문 영역은 반복을 위한 것이 아니라 조건에 안맞았을 시 바로 빠져나오기 위한 영역. 
        // while (false)이기 때문에 단 한번만 실행된다.
        do
        {
            // x
            float tx_min = 0f;
            float tx_max = 1f;
            if (sv.x == 0f)
            {
                // 선분이 x좌표로 이동하지 않는다는 뜻이므로 선분의 위치가 박스영역 안인지만 확인하면 된다.
                // 그리고 0으로 나누지 않기 위해서도 따로 처리한다.
                if (s0.x < b0.x || s0.x > b1.x) break;
            }
            else
            {
                // 선분과 박스 영역의 x값의 매개변수를 구한다.
                float tx0 = (b0.x - s0.x) / sv.x;
                float tx1 = (b1.x - s0.x) / sv.x;
                // x축의 최소값 최대값을 결정
                tx_min = Mathf.Min(tx0, tx1);
                tx_max = Mathf.Max(tx0, tx1);
                // 최소, 최대값이 영역을 벗어났는지 확인
                if (tx_max < 0f || tx_min > 1) break;

                //Gizmos.color = Color.red;
                //Gizmos.DrawWireSphere(s0 + (sv * tx0), 0.3f);
                //Gizmos.DrawWireCube(s0 + (sv * tx1), Vector3.one * 0.55f);
            }
            // t_min이 x축의 최대(tx_max)보다 크다는 것은 다른축과 겹치는 영역이 없다는 것이기 때문에 종료한다.
            // t_max가 x축의 최소(tx_min)보다 작다는 것은 다른축과 겹치는 영역이 없다는 것이기 때문에 종료한다.
            if (t_min > tx_max || t_max < tx_min) break;

            // t_min, t_max 값을 tx_min, tx_max 값으로 갱신한다.
            // 현재 최소값보다 x축의 최소값이 크면 x축의 최소값으로 갱신한다.(겹치는 영역을 좁혀나간다.)
            t_min = Mathf.Max(t_min, tx_min);
            // 현재 최대값보다 x축의 최대값이 크면 x축의 최소값으로 갱신한다.(겹치는 영역을 좁혀나간다.)
            t_max = Mathf.Min(t_max, tx_max);
            // 여기서 t_min, t_max 값은 초기값이기 때문에 tx_min, tx_max 을 바로 넣어도 되지만 일관성을 위해 y, z와 똑같이 처리한다.

            // y
            // x와 똑같이 처리한다.
            float ty_min = 0f;
            float ty_max = 1f;
            if (sv.y == 0f)
            {
                if (s0.y < b0.y || s0.y > b1.y) break;
            }
            else
            {
                float ty0 = (b0.y - s0.y) / sv.y;
                float ty1 = (b1.y - s0.y) / sv.y;
                ty_min = Mathf.Min(ty0, ty1);
                ty_max = Mathf.Max(ty0, ty1);

                if (ty_max < 0f || ty_min > 1) break;

                //Gizmos.color = Color.red;
                //Gizmos.DrawWireSphere(s0 + (sv * ty0), 0.3f);
                //Gizmos.DrawWireCube(s0 + (sv * ty1), Vector3.one * 0.55f);
            }
            if (t_max < ty_min || t_min > ty_max) break;
            t_min = Mathf.Max(t_min, ty_min);
            t_max = Mathf.Min(t_max, ty_max);

            // z
            // x와 똑같이 처리한다.
            float tz_min = 0f;
            float tz_max = 1f;
            if (sv.z == 0f)
            {
                if (s0.z < b0.z || s0.z > b1.z) break;
            }
            else
            {
                float tz0 = (b0.z - s0.z) / sv.z;
                float tz1 = (b1.z - s0.z) / sv.z;
                tz_min = Mathf.Min(tz0, tz1);
                tz_max = Mathf.Max(tz0, tz1);

                if (tz_max < 0f || tz_min > 1) break;

                //Gizmos.color = Color.red;
                //Gizmos.DrawWireSphere(s0 + (sv * tz0), 0.3f);
                //Gizmos.DrawWireCube(s0 + (sv * tz1), Vector3.one * 0.55f);
            }
            if (t_max < tz_min || t_min > tz_max) break;
            t_min = Mathf.Max(t_min, tz_min);
            t_max = Mathf.Min(t_max, tz_max);

            // 최종 t값이 0~1 사이에 있는지 확인
            //hit = !(t_min > 1f || t_max < 0);
            hit = (t_min <= 1f && t_max >= 0);
        } while (false);

        // 선분 그리기
        Gizmos.color = Color.yellow;
        Gizmos.DrawLine(s0, s1);
        Gizmos.DrawLine(s0, s0 + Vector3.up);
        Gizmos.DrawLine(s1, s1 + Vector3.up);

        // 충돌 영역을 선분에 겹쳐 그린다.
        if (hit)
        {
            Gizmos.color = Color.white;
            Gizmos.DrawLine(s0 + (sv * t_min), s0 + (sv * t_max));
            Gizmos.DrawLine(s0 + (sv * t_min), s0 + (sv * t_min) + Vector3.up);
            Gizmos.DrawLine(s0 + (sv * t_max), s0 + (sv * t_max) + Vector3.up);
        }

        // 상자 그리기
        // 각 축별로 앞위왼 -> 뒤위오 순으로 그린다.
        // x축
        Gizmos.color = Color.red;
        Gizmos.DrawLine(new Vector3(b0.x, b1.y, b0.z), new Vector3(b1.x, b1.y, b0.z));
        Gizmos.DrawLine(b0, new Vector3(b1.x, b0.y, b0.z));
        Gizmos.DrawLine(new Vector3(b0.x, b1.y, b1.z), b1);
        Gizmos.DrawLine(new Vector3(b0.x, b0.y, b1.z), new Vector3(b1.x, b0.y, b1.z));

        // y축
        Gizmos.color = Color.green;
        Gizmos.DrawLine(new Vector3(b0.x, b1.y, b0.z), b0);
        Gizmos.DrawLine(new Vector3(b1.x, b1.y, b0.z), new Vector3(b1.x, b0.y, b0.z));
        Gizmos.DrawLine(new Vector3(b0.x, b1.y, b1.z), new Vector3(b0.x, b0.y, b1.z));
        Gizmos.DrawLine(b1, new Vector3(b1.x, b0.y, b1.z));

        // z축
        Gizmos.color = Color.blue;
        Gizmos.DrawLine(new Vector3(b0.x, b1.y, b0.z), new Vector3(b0.x, b1.y, b1.z));
        Gizmos.DrawLine(b0, new Vector3(b0.x, b0.y, b1.z));
        Gizmos.DrawLine(new Vector3(b1.x, b1.y, b0.z), b1);
        Gizmos.DrawLine(new Vector3(b1.x, b0.y, b0.z), new Vector3(b1.x, b0.y, b1.z));

        return hit;
    }
}

```



###### OBB 작동화면 캡쳐

![](https://raw.githubusercontent.com/lazyartist/blog/master/images/OBB.gif)