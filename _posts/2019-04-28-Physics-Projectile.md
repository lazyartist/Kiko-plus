---
layout: post
title: "Physics - Projectile"
description: ""
date: 2019-04-28 19:00:00+09:00
tags: [Physics, Projectile]
comments: true
share: true
---

[TOC]

## 등가속도



$$
\begin{gather*}
\begin{array}{ c c c }
t & : & 경과\ 시간\\
a & : & 가속도\\
v_{0} & : & 처음\ 속도\\
v & : & 나중\ 속도
\end{array}\\
a=\frac{v-v_{0}}{t}
\end{gather*}
$$



## 속도

$$
\begin{gather*}
\begin{array}{ c c c }
t & : & 경과\ 시간\\
a & : & 가속도\\
v_{0} & : & 처음\ 속도\\
v & : & 나중\ 속도
\end{array}\\
v=v_{0} +at
\end{gather*}
$$



## 물체의 변위(이동 거리)


<svg xmlns="http://www.w3.org/2000/svg" width="662" height="250.8125" style="
        width:662px;
        height:250.8125px;
        background: white;
        fill: none;
">
        <svg xmlns="http://www.w3.org/2000/svg"><g><defs><pattern id=".29422238962414315" width="10" height="10" patternUnits="userSpaceOnUse"><path d="M 10 0 L 0 0 0 10" fill="none" stroke="lightgray" stroke-width="0.5"/></pattern></defs><rect width="100%" height="100%" fill="url(#.29422238962414315)" stroke="lightgray" stroke-width="0.5"/></g></svg>
        <svg xmlns="http://www.w3.org/2000/svg" class="role-diagram-draw-area"><g class="shapes-region" style="stroke: black; fill: none;"><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M202,199.64 L388.1,199.64 M220.61,18 L220.61,219.82"/><path d=" M381.1,194.64 L388.1,199.64 L381.1,204.64"/><path d=" M215.61,25 L220.61,18 L225.61,25"/></g><g class="composite-shape"><path class="real" d=" M220.61,134.82 L370.1,134.82 L370.1,199.64 L220.61,199.64 Z" style="stroke-width: 1; stroke: rgb(0, 0, 0); fill: rgb(74, 144, 226); stroke-dasharray: 1.125, 3.35;"/></g><g class="shape"><polygon class="real" points=" 370.1,60.82 370.1,134.82 220.61,134.82" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: rgb(74, 144, 226); stroke-dasharray: 1.125, 3.35;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M221.1,61.82 L370.1,60.82" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="composite-shape"><path class="real" d=" M369.98,134.81 C370.19,134.82 370.4,134.83 370.6,134.83 C379.99,134.83 387.6,118.26 387.6,97.83 C387.6,77.39 379.99,60.82 370.6,60.82 C370.45,60.82 370.31,60.82 370.16,60.83 L370.6,97.83 Z" style="stroke-width: 1; stroke: none; fill: none; stroke-dasharray: 1.125, 3.35;"/><path class="real" d=" M369.98,134.81 C370.19,134.82 370.4,134.83 370.6,134.83 C379.99,134.83 387.6,118.26 387.6,97.83 C387.6,77.39 379.99,60.82 370.6,60.82 C370.45,60.82 370.31,60.82 370.16,60.83" style="stroke-width: 1; stroke: rgb(0, 0, 0); fill: none; stroke-dasharray: 1.125, 3.35;"/></g><g class="intersections-group"><g style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g></g><g/><g/><!-- react-empty: 503 --></svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="660" height="248.8125" style="width:660px;height:248.8125px;font-family:Asana-Math, Asana;background:white;"><g><g><text x="205.62503051757812" y="204.1999969482422" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(0, 0, 0);">0</text></g></g><g><g><text x="367.6250305175781" y="203.1999969482422" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(0, 0, 0);">t</text></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,201.78750610351562,140.15626525878906);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g><g><g><g style="transform:matrix(1,0,0,1,210.26254272460938,145.54375305175782);"><path d="M263 689C108 689 29 566 29 324C29 207 50 106 85 57C120 8 176 -20 238 -20C389 -20 465 110 465 366C465 585 400 689 263 689ZM245 654C342 654 381 556 381 316C381 103 343 15 251 15C154 15 113 116 113 360C113 571 150 654 245 654Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.0119,0,0,-0.0119,0,0);"></path></g></g></g></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,204.62503051757812,68.60000610351562);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,396.6312561035156,103.15626525878906);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,408.3062438964844,103.15626525878906);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,421.7812805175781,103.15626525878906);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g><g><g><g style="transform:matrix(1,0,0,1,430.2562561035156,108.54375305175782);"><path d="M263 689C108 689 29 566 29 324C29 207 50 106 85 57C120 8 176 -20 238 -20C389 -20 465 110 465 366C465 585 400 689 263 689ZM245 654C342 654 381 556 381 316C381 103 343 15 251 15C154 15 113 116 113 360C113 571 150 654 245 654Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.0119,0,0,-0.0119,0,0);"></path></g></g></g></g><g style="transform:matrix(1,0,0,1,440.9937438964844,103.15626525878906);"><path d="M604 347L604 406L65 406L65 347ZM604 134L604 193L65 193L65 134Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,457.1437683105469,103.15626525878906);"><path d="M271 204L242 77C238 60 236 42 236 26C236 4 245 -9 260 -9C283 -9 324 17 406 85L399 106C375 86 346 59 324 59C315 59 309 68 309 82C309 87 309 90 310 93L402 472L392 481L359 463C318 478 301 482 274 482C246 482 226 477 199 464C137 433 104 403 79 354C35 265 4 145 4 67C4 23 19 -11 38 -11C75 -11 155 41 271 204ZM319 414C297 305 278 253 244 201C187 117 126 59 94 59C82 59 76 72 76 99C76 163 104 280 139 360C163 415 186 433 234 433C257 433 275 429 319 414ZM568 390L512 107C511 99 499 61 499 31C499 6 510 -9 529 -9C564 -9 599 11 677 74L708 99L698 117L653 86C624 66 604 56 593 56C584 56 579 64 579 76C579 102 593 183 622 328L635 390L742 390L753 440C715 436 681 434 643 434C659 528 670 577 688 631L677 646C657 634 630 622 599 610L574 440C530 419 504 408 486 403L484 390Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,328.2000427246094,103.00001525878906);"><path d="M418 -3L418 27L366 30C311 33 301 44 301 96L301 700L60 598L67 548L217 614L217 96C217 44 206 33 152 30L96 27L96 -3C250 0 250 0 261 0C292 0 402 -3 418 -3Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g><g><g><g style="transform:matrix(1,0,0,1,328.2000427246094,128.00001525878906);"><path d="M16 23L16 -3C203 -3 203 0 239 0C275 0 275 -3 468 -3L468 82C353 77 307 81 122 77L304 270C401 373 431 428 431 503C431 618 353 689 226 689C154 689 105 669 56 619L39 483L68 483L81 529C97 587 133 612 200 612C286 612 341 558 341 473C341 398 299 324 186 204Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g><line style="fill:none;stroke-width:1px;stroke:rgb(0, 0, 0);" x1="328.2000427246094" y1="110.55000305175781" x2="336.68754291534424" y2="110.55000305175781"></line></g><g style="transform:matrix(1,0,0,1,338.3875427246094,115.00001525878906);"><path d="M271 204L242 77C238 60 236 42 236 26C236 4 245 -9 260 -9C283 -9 324 17 406 85L399 106C375 86 346 59 324 59C315 59 309 68 309 82C309 87 309 90 310 93L402 472L392 481L359 463C318 478 301 482 274 482C246 482 226 477 199 464C137 433 104 403 79 354C35 265 4 145 4 67C4 23 19 -11 38 -11C75 -11 155 41 271 204ZM319 414C297 305 278 253 244 201C187 117 126 59 94 59C82 59 76 72 76 99C76 163 104 280 139 360C163 415 186 433 234 433C257 433 275 429 319 414ZM568 390L512 107C511 99 499 61 499 31C499 6 510 -9 529 -9C564 -9 599 11 677 74L708 99L698 117L653 86C624 66 604 56 593 56C584 56 579 64 579 76C579 102 593 183 622 328L635 390L742 390L753 440C715 436 681 434 643 434C659 528 670 577 688 631L677 646C657 634 630 622 599 610L574 440C530 419 504 408 486 403L484 390Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g><g><g><g style="transform:matrix(1,0,0,1,351.5500183105469,107.71251525878907);"><path d="M16 23L16 -3C203 -3 203 0 239 0C275 0 275 -3 468 -3L468 82C353 77 307 81 122 77L304 270C401 373 431 428 431 503C431 618 353 689 226 689C154 689 105 669 56 619L39 483L68 483L81 529C97 587 133 612 200 612C286 612 341 558 341 473C341 398 299 324 186 204Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.0119,0,0,-0.0119,0,0);"></path></g></g></g></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,285.3125305175781,171.38124084472656);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g><g><g><g style="transform:matrix(1,0,0,1,293.7875061035156,176.76875915527344);"><path d="M263 689C108 689 29 566 29 324C29 207 50 106 85 57C120 8 176 -20 238 -20C389 -20 465 110 465 366C465 585 400 689 263 689ZM245 654C342 654 381 556 381 316C381 103 343 15 251 15C154 15 113 116 113 360C113 571 150 654 245 654Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.0119,0,0,-0.0119,0,0);"></path></g></g></g></g><g style="transform:matrix(1,0,0,1,299.7250061035156,171.38124084472656);"><path d="M125 390L69 107C68 99 56 61 56 31C56 6 67 -9 86 -9C121 -9 156 11 234 74L265 99L255 117L210 86C181 66 161 56 150 56C141 56 136 64 136 76C136 102 150 183 179 328L192 390L299 390L310 440C272 436 238 434 200 434C216 528 227 577 245 631L234 646C214 634 187 622 156 610L131 440C87 419 61 408 43 403L41 390Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g></svg>
</svg>

$$
\begin{gather*}
\begin{array}{ c c c }
s & : & 변위
\end{array}\\
s=v_{0} t+\frac{1}{2} at^{2}
\end{gather*}
$$



## 시간이 주어지지 않았을 때 물체의 변위

$$
\begin{gather*}
v=v_{0} +at를\ t로\ 정리\\
t=\frac{v-v_{0}}{a}\\
\\
물체의\ 변위식의\ t에\ 대입\\
\begin{array}{ c c c }
s & = & v_{0} t+\frac{1}{2} at^{2}\\
 & = & v_{0}\left(\frac{v-v_{0}}{a}\right) +\frac{1}{2} a\left(\frac{v-v_{0}}{a}\right)^{2}\\
 & = & \frac{vv_{0} -v^{2}_{0}}{a} +\frac{v^{2} -2vv_{0} +v^{2}_{0}}{2a}\\
 & = & \frac{2vv_{0} -2v^{2}_{0} +v^{2} -2vv_{0} +v^{2}_{0}}{2a}\\
 & = & \frac{v^{2} -v^{2}_{0}}{2a}
\end{array}\\
\\
\therefore 2as=v^{2} -v^{2}_{0}
\end{gather*}
$$



## 포물선 운동


<svg xmlns="http://www.w3.org/2000/svg" width="662" height="202.5" style="
        width:662px;
        height:202.5px;
        background: white;
        fill: none;
">
        <svg xmlns="http://www.w3.org/2000/svg"><g><defs><pattern id=".8079804738537064" width="10" height="10" patternUnits="userSpaceOnUse"><path d="M 10 0 L 0 0 0 10" fill="none" stroke="lightgray" stroke-width="0.5"/></pattern></defs><rect width="100%" height="100%" fill="url(#.8079804738537064)" stroke="lightgray" stroke-width="0.5"/></g></svg>
        <svg xmlns="http://www.w3.org/2000/svg" class="role-diagram-draw-area"><g class="shapes-region" style="stroke: black; fill: none;"><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M160,146 L500,146 M194,20 L194,160"/><path d=" M493,141 L500,146 L493,151"/><path d=" M189,27 L194,20 L199,27"/></g><g class="composite-shape"><path class="real" d=" M194.74,146.5 C198.43,114.15 254.88,88.28 324.07,88.03 C393.91,87.77 450.95,113.7 453.93,146.45 L324.3,149.5 Z" style="stroke-width: 1; stroke: none; fill: none;"/><path class="real" d=" M194.74,146.5 C198.43,114.15 254.88,88.28 324.07,88.03 C393.91,87.77 450.95,113.7 453.93,146.45" style="stroke-width: 1; stroke: rgb(0, 0, 0); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M209.34,101.89 L194,146" style="stroke: rgb(208, 2, 27); stroke-width: 1; fill: none;"/><g stroke="none" fill="rgba(208,2,27,1)" transform="matrix(-0.3285369771688027,0.9444911088161633,-0.9444911088161633,-0.3285369771688027,210,100)" style="stroke: none; fill: rgb(208, 2, 27); stroke-width: 1;"><path d=" M8.93,-4.29 L0,0 L8.93,4.29 Z"/></g></g><g class="composite-shape"><path class="real" d=" M194,100 L210,100 L210,146 L194,146 Z" style="stroke-width: 1; stroke: rgb(0, 0, 0); fill: none; stroke-dasharray: 1.125, 3.35;"/></g><g class="composite-shape"><path class="real" d=" M201.81,125.15 C211.62,125.55 219.42,134.4 219.34,145.2 C219.34,145.31 219.34,145.42 219.33,145.53 L201.1,145.06 Z" style="stroke-width: 1; stroke: none; fill: none;"/><path class="real" d=" M201.81,125.15 C211.62,125.55 219.42,134.4 219.34,145.2 C219.34,145.31 219.34,145.42 219.33,145.53" style="stroke-width: 1; stroke: rgb(74, 144, 226); fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M500,90 L194,89" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="1.125 3.35" d="  M453,64 L454,164" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="intersections-group"><g style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g></g><g/><g/><!-- react-empty: 1095 --></svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="660" height="200.5" style="width:660px;height:200.5px;font-family:Asana-Math, Asana;background:white;"><g><g><g><g><g><g style="transform:matrix(1,0,0,1,213.78750610351562,101.15625);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(208, 2, 27)" stroke-width="8" fill="rgb(208, 2, 27)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g><g><g><g style="transform:matrix(1,0,0,1,222.26254272460938,106.54373779296876);"><path d="M263 689C108 689 29 566 29 324C29 207 50 106 85 57C120 8 176 -20 238 -20C389 -20 465 110 465 366C465 585 400 689 263 689ZM245 654C342 654 381 556 381 316C381 103 343 15 251 15C154 15 113 116 113 360C113 571 150 654 245 654Z" stroke="rgb(208, 2, 27)" stroke-width="8" fill="rgb(208, 2, 27)" style="transform:matrix(0.0119,0,0,-0.0119,0,0);"></path></g></g></g></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,91.71249389648438,107.15625);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g><g><g><g style="transform:matrix(1,0,0,1,100.18753051757812,112.54373779296876);"><path d="M263 689C108 689 29 566 29 324C29 207 50 106 85 57C120 8 176 -20 238 -20C389 -20 465 110 465 366C465 585 400 689 263 689ZM245 654C342 654 381 556 381 316C381 103 343 15 251 15C154 15 113 116 113 360C113 571 150 654 245 654ZM492 -180C491 -187 491 -193 491 -198C491 -241 528 -276 573 -276C679 -276 789 -152 848 33L989 473L978 482C949 471 926 465 904 463L869 331C857 284 822 211 789 162C754 111 705 67 683 67C671 67 662 90 663 115L679 322C681 353 683 391 683 419C683 464 676 482 659 482C646 482 632 475 584 442L502 386L513 368L563 398C568 401 579 410 588 410C602 410 610 391 610 358C610 357 610 351 609 343L592 100L591 60C591 18 609 -11 634 -11C671 -11 755 74 830 187L781 16C730 -161 680 -234 610 -234C575 -234 548 -207 548 -172C548 -167 549 -159 550 -150L540 -146Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.0119,0,0,-0.0119,0,0);"></path></g></g></g></g><g style="transform:matrix(1,0,0,1,116.86251831054688,107.15625);"><path d="M604 347L604 406L65 406L65 347ZM604 134L604 193L65 193L65 134Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,133.01254272460938,107.15625);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g><g><g><g style="transform:matrix(1,0,0,1,141.48751831054688,112.54373779296876);"><path d="M263 689C108 689 29 566 29 324C29 207 50 106 85 57C120 8 176 -20 238 -20C389 -20 465 110 465 366C465 585 400 689 263 689ZM245 654C342 654 381 556 381 316C381 103 343 15 251 15C154 15 113 116 113 360C113 571 150 654 245 654Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.0119,0,0,-0.0119,0,0);"></path></g></g></g></g><g><g style="transform:matrix(1,0,0,1,150.82504272460938,107.15625);"><path d="M41 143C41 74 38 44 30 4C82 -13 121 -20 167 -20C298 -20 391 50 391 148C391 321 107 228 107 358C107 408 142 436 203 436C270 436 321 401 321 354L321 331L349 331C350 389 351 413 354 444C301 462 265 469 224 469C108 469 37 414 37 324C37 276 59 242 105 221C223 169 317 195 317 109C317 55 267 17 196 17C123 17 71 52 71 102L71 143ZM611 465L602 469C551 448 499 434 446 428L446 400L483 400C523 400 527 393 527 327L527 102C527 39 524 32 490 30L444 27L444 -3C544 0 544 0 569 0C594 0 594 0 694 -3L694 27L648 30C614 32 611 39 611 102ZM565 687C535 687 509 661 509 631C509 602 535 576 564 576C593 576 620 602 620 631C620 659 593 687 565 687ZM1123 -3C1184 0 1185 0 1202 0C1216 0 1216 0 1285 -3L1285 27L1244 30C1210 32 1207 38 1207 102L1207 295C1207 412 1152 469 1040 469C1003 469 982 462 961 444L885 378L885 465L876 469C825 448 773 434 720 428L720 400L757 400C797 400 801 393 801 327L801 102C801 39 798 32 764 30L719 27L719 -3C787 -1 814 0 843 0C872 0 899 -1 967 -3L967 27L922 30C888 32 885 39 885 102L885 314C885 359 951 408 1012 408C1079 408 1123 358 1123 281Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g><g style="transform:matrix(1,0,0,1,176.22500610351562,107.15625);"><path d="M237 -16C473 -16 572 316 576 504C578 618 546 702 419 702C159 702 72 412 69 199C67 80 101 -16 237 -16ZM401 676C536 676 506 491 485 381L169 381C194 485 272 676 401 676ZM253 13C102 13 147 261 163 349L479 349C454 237 396 13 253 13Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,210.71878051757812,171.15625);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g><g><g><g style="transform:matrix(1,0,0,1,219.19375610351562,176.54373779296876);"><path d="M263 689C108 689 29 566 29 324C29 207 50 106 85 57C120 8 176 -20 238 -20C389 -20 465 110 465 366C465 585 400 689 263 689ZM245 654C342 654 381 556 381 316C381 103 343 15 251 15C154 15 113 116 113 360C113 571 150 654 245 654ZM508 1C523 -7 539 -11 551 -11C584 -11 623 18 654 65L730 182L741 113C754 28 777 -11 813 -11C835 -11 867 6 899 35L948 79L939 98C903 68 878 53 862 53C847 53 834 63 824 83C815 102 804 139 799 168L781 269L816 318C863 383 890 406 921 406C937 406 949 398 954 383L968 387L983 472C971 479 962 482 953 482C913 482 873 446 811 354L774 299L768 347C756 446 729 482 670 482C644 482 622 474 613 461L555 378L572 368C602 402 622 416 641 416C674 416 696 375 713 277L724 215L684 153C641 86 607 54 579 54C564 54 553 58 551 63L540 91L520 88C520 53 512 27 508 1Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.0119,0,0,-0.0119,0,0);"></path></g></g></g></g><g style="transform:matrix(1,0,0,1,235.86874389648438,171.15625);"><path d="M604 347L604 406L65 406L65 347ZM604 134L604 193L65 193L65 134Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,252.01876831054688,171.15625);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g><g><g><g style="transform:matrix(1,0,0,1,260.4937438964844,176.54373779296876);"><path d="M263 689C108 689 29 566 29 324C29 207 50 106 85 57C120 8 176 -20 238 -20C389 -20 465 110 465 366C465 585 400 689 263 689ZM245 654C342 654 381 556 381 316C381 103 343 15 251 15C154 15 113 116 113 360C113 571 150 654 245 654Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.0119,0,0,-0.0119,0,0);"></path></g></g></g></g><g><g style="transform:matrix(1,0,0,1,269.8312683105469,171.15625);"><path d="M399 311C399 357 404 398 413 434C381 478 338 497 293 497C169 497 25 361 25 224C25 219 26 215 26 210C26 75 121 -20 255 -20C307 -20 382 -1 392 14L413 46L403 61C366 41 334 32 298 32C187 32 114 118 114 250C114 357 164 417 254 417C298 417 346 397 364 372L371 311ZM722 469C576 469 475 366 475 217C475 76 564 -20 693 -20C847 -20 957 87 957 237C957 372 859 469 722 469ZM704 436C796 436 864 336 864 200C864 85 813 13 732 13C634 13 568 109 568 251C568 371 616 436 704 436ZM1029 143C1029 74 1026 44 1018 4C1070 -13 1109 -20 1155 -20C1286 -20 1379 50 1379 148C1379 321 1095 228 1095 358C1095 408 1130 436 1191 436C1258 436 1309 401 1309 354L1309 331L1337 331C1338 389 1339 413 1342 444C1289 462 1253 469 1212 469C1096 469 1025 414 1025 324C1025 276 1047 242 1093 221C1211 169 1305 195 1305 109C1305 55 1255 17 1184 17C1111 17 1059 52 1059 102L1059 143Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g><g style="transform:matrix(1,0,0,1,297.2187805175781,171.15625);"><path d="M237 -16C473 -16 572 316 576 504C578 618 546 702 419 702C159 702 72 412 69 199C67 80 101 -16 237 -16ZM401 676C536 676 506 491 485 381L169 381C194 485 272 676 401 676ZM253 13C102 13 147 261 163 349L479 349C454 237 396 13 253 13Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,217.78750610351562,137.0999755859375);"><path d="M237 -16C473 -16 572 316 576 504C578 618 546 702 419 702C159 702 72 412 69 199C67 80 101 -16 237 -16ZM401 676C536 676 506 491 485 381L169 381C194 485 272 676 401 676ZM253 13C102 13 147 261 163 349L479 349C454 237 396 13 253 13Z" stroke="rgb(74, 144, 226)" stroke-width="8" fill="rgb(74, 144, 226)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,510.8812561035156,96.0999755859375);"><path d="M236 722L224 733C179 711 138 697 64 691L60 670L108 670C126 670 142 667 142 647C142 641 142 632 140 622L98 388C78 272 36 80 10 2L17 -9L86 7C94 64 108 164 148 236C193 317 296 414 338 414C349 414 360 407 360 393C360 375 355 342 345 303L294 107C288 85 281 55 281 31C281 6 291 -9 312 -9C344 -9 412 41 471 85L461 103L435 86C412 71 386 56 374 56C367 56 361 65 361 76C361 88 364 101 368 116L432 372C438 398 443 423 443 447C443 464 437 482 411 482C376 482 299 437 231 374C198 343 172 308 144 273L140 275Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,526.7937316894531,96.0999755859375);"><path d="M123 111C93 111 66 83 66 53C66 23 93 -5 122 -5C154 -5 182 22 182 53C182 83 154 111 123 111ZM123 456C93 456 66 428 66 398C66 368 93 340 122 340C154 340 182 367 182 397C182 428 154 456 123 456Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g><g style="transform:matrix(1,0,0,1,534.0813293457031,96.0999755859375);"><path d="" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><text x="538.0813293457031" y="96.26664225260417" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:17px;font-family:Asana-Math, Asana;font-weight:400;dominant-baseline:auto;text-decoration:none solid rgb(0, 0, 0);">최고점</text><g style="transform:matrix(1,0,0,1,589.2812805175781,96.0999755859375);"><path d="" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><text x="594.0813293457031" y="96.26664225260417" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:17px;font-family:Asana-Math, Asana;font-weight:400;dominant-baseline:auto;text-decoration:none solid rgb(0, 0, 0);">높이</text></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,401.7812805175781,186.0999755859375);"><path d="M368 365C371 403 376 435 384 476C373 481 369 482 364 482C333 482 302 458 266 407C227 351 188 291 172 256L204 408C208 425 210 438 210 450C210 470 202 482 187 482C166 482 128 461 54 408L26 388L33 368L65 389C93 407 104 412 113 412C123 412 130 403 130 390C130 332 87 126 47 -2L57 -9C72 -4 88 -1 111 4L124 6L150 126C168 209 191 262 235 319C269 363 296 384 318 384C333 384 343 379 354 365Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g><text x="408.3812561035156" y="172.29998779296875" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;dominant-baseline:text-before-edge;text-decoration:none solid rgb(0, 0, 0);"> : 수평 도달 거리</text></g></g></svg>
</svg>

$$
\begin{equation*}
\begin{array}{ c c c }
t & : & 경과\ 시간\\
a & : & 가속도\\
g & : & 중력\ 가속도\\
\theta  & : & 초기\ 각도\\
v_{x} & : & 나중\ x축\ 속도\\
v_{y} & : & 나중\ y축\ 속도\\
h & : & 최고점\ 높이\\
r & : & 수평\ 도달\ 거리
\end{array}
\end{equation*}
$$



## 포물선 - t초 후 속도

$$
\begin{equation*}
\begin{array}{ c c c }
v_{x} & = & v_{0}\cos \theta \ ( 수평은\ 등속운동)\\
v_{y} & = & v_{0}\sin \theta -gt
\end{array}
\end{equation*}
$$



## 포물선 - t초 후 위치

$$
\begin{equation*}
\begin{array}{ c c c }
x & = & v_{0}\cos \theta \times t\\
y & = & v_{0}\sin \theta \times t-\frac{1}{2} gt^{2}
\end{array}
\end{equation*}
$$



## 포물선 - 최고점 높이

$$
\begin{gather*}
최고점에서\ y속도가\ 0이\ 되는\ 것을\ 이용\\
\\
\begin{array}{ c c c c }
2as & = & v^{2} -v^{2}_{0} & \\
-2gs & = & 0-v^{2}_{0} & ( g는\ 반대방향이므로\ -,\ 최고점\ 속력은\ 0)\\
2gs & = & v^{2}_{0} & \\
2gs & = & v^{2}_{0y} & ( y의\ 변위를\ 구하므로\ v_{0y} 로\ 변경)\\
2gs & = & ( v_{0}\sin \theta )^{2} & \\
s & = & \frac{( v_{0}\sin \theta )^{2}}{2g} & \\
s & = & \frac{v^{2}_{0}\sin^{2} \theta }{2g} & 
\end{array}\\
\therefore h( 최고점\ 높이) =\frac{v^{2}_{0}\sin^{2} \theta }{2g}
\end{gather*}
$$



## 포물선 - 최고점 도달 시간

최고점에서 y속도는 0, 등가속도는 중력가속도 g를 시간을 구하는 공식에 대입

$$
\begin{gather*}
\begin{array}{ c c c c }
t & = & \frac{v-v_{0}}{a} & \\
 & = & \frac{0-v_{0}}{g} & \\
 & = & \frac{v_{0}\sin \theta }{g} & ( y축에\ 대한\ 식으로\ 변경)
\end{array}\\
\therefore h_{t}( 최고점\ 도달\ 시간) =\frac{v_{0}\sin \theta }{g}
\end{gather*}
$$


## 포물선 - 수평 도달 거리

이동 거리 공식에 최고점 도달시간 공식의 2배를 대입

(땅에 떨어질 때까지의 시간은 최고점 도달 시간의 2배)

$$
\begin{gather*}
\begin{array}{ c c c c }
s & = & vt & ( 이동거리\ 공식)\\
 & = & v_{0}\cos \theta \times t & ( x에\ 대한\ 식으로\ 변경)\\
 & = & v_{0}\cos \theta \times \left( 2\times \frac{v_{0}\sin \theta }{g}\right) & ( 최고점\ 도달시간\ 공식\ 대입)\\
 & = & \frac{v_{0}\cos \theta \times 2v_{0}\sin \theta }{g} & \\
 & = & \frac{v^{2}_{0} \times 2\cos \theta \sin \theta }{g} & \\
 & = & \frac{v^{2}_{0} \times \sin 2\theta }{g} & (\sin 2\theta =2\cos \theta \sin \theta )
\end{array}\\
\therefore r( 수평\ 도달\ 거리) =\frac{v^{2}_{0} \times \sin 2\theta }{g}
\end{gather*}
$$


## 포물선 - 경로 방정식

처음 속도와 발사 각도 및 x값을 아는 경우 y값을 계산할 수 있다.

x의 변위식을 y의 변위식에 대입하여 방정식 도출

$$
\begin{gather*}
\begin{array}{ c c c c }
s & = & v_{0} t-\frac{1}{2} gt^{2} & ( 거리\ 기본식)\\
x & = & v_{0}\cos \theta t & \\
y & = & v_{0}\sin \theta t-\frac{1}{2} gt^{2} & 
\end{array}\\
\\
x식을\ t에\ 대해\ 정리\ 후\ y식에\ 대입\\
\\
\begin{array}{ c c c c }
t & = & \frac{x}{v_{0}\cos \theta } & \\
y & = & v_{0}\sin \theta \frac{x}{v_{0}\cos \theta } -\frac{1}{2} g\left(\frac{x}{v_{0}\cos \theta }\right)^{2} & ( t를\ 대입)\\
 & = & \frac{v_{0}\sin \theta }{v_{0}\cos \theta } x-\frac{1}{2} g\frac{x^{2}}{v^{2}_{0}\cos^{2} \theta } & \\
 & = & \tan \theta x-\frac{g}{2v^{2}_{0}\cos^{2} \theta } x^{2} & \left(\frac{\sin \theta }{\cos \theta } =\tan \theta \right)
\end{array}
\end{gather*}
$$



```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ProjectileMotionTest : MonoBehaviour
{
    [Range(0, 360)]
    public float Angle;
    public float Velocity;
    public float Gravity = 9.8f;

    public float XRange = 10f;
    public float DrawLineResolution = 50;
    
    private void OnDrawGizmos()
    {
        // 각도와 속도 그리기
        float radian = Angle * Mathf.Deg2Rad;
        Gizmos.color = Color.blue;
        Gizmos.DrawLine(transform.position, transform.position + new Vector3(Velocity * Mathf.Cos(radian), Velocity * Mathf.Sin(radian), 0));

        // 포물선 그리기
        Gizmos.color = Color.red;
        float xUnit = XRange / DrawLineResolution;
        Vector3 prevPosition = transform.position;
        for (int i = 0; i < DrawLineResolution; i++)
        {
            float x = xUnit * i;
            float y = GetProjectileMotionY(x);
            Vector3 curPosition = transform.position + new Vector3(x, y, 0);

            Gizmos.DrawLine(prevPosition, curPosition);

            prevPosition = curPosition;
        }
    }

    private float GetProjectileMotionY(float x)
    {
        float radian = Angle * Mathf.Deg2Rad;
        float y = Mathf.Tan(radian) * x;
        y -= Gravity / (2 * Velocity * Velocity * Mathf.Cos(radian) * Mathf.Cos(radian)) * (x * x);
        return y;
    }
}

```




## 포물선 - (역)경로 방정식

최고점 높이(h), 최고점 도달 시간(ht), 마지막 위치(y) 및 경과 시간(t)을 아는 경우 y값을 계산할 수 있다.



#### 1. g(등가속도)값 구하기

최고점에서 지면으로 떨어질 때 최초 속도는 0이고 이동 거리(최고점 높이), 도달 시간을 알고 있으므로 기본공식을 이용하여 g값을 계산할 수 있다.

최고점에서 떨어지는 운동은 중력가속도에 의해 가속되는 운동이므로 등가속도값 빼지 않고 더해준다.

$$
\begin{equation*}
\begin{array}{ c c c c }
y & = & v_{0}\sin \theta \times t+\frac{1}{2} gt^{2} & \\
h & = & 0\times \sin \theta \times t+\frac{1}{2} gt^{2} & \\
 & = & \frac{1}{2} gt^{2} & \\
g & = & \frac{2h}{t^{2}} & 
\end{array}
\end{equation*}
$$



#### 2. y의 초기 속도(vy) 구하기

g값을 구했으니 최고점 높이 구하는 공식을 이용해 y의 초기 속도를 계산한다.

$$
\begin{equation*}
\begin{array}{ c c c }
h & = & \frac{v^{2}_{0}\sin^{2} \theta }{2g}\\
 & = & \frac{v^{2}_{y}}{2g}\\
v^{2}_{y} & = & 2hg\\
v_{y} & = & \sqrt{2hg}
\end{array}
\end{equation*}
$$



#### 3. 마지막 위치(y)까지 이동 시간(t) 구하기

기본 이동 공식에 알고 있는 값을 대입하면 미지수가 t만 남는데 이는 근의 공식을 사용하여 계산해 낸다.

$$
\begin{gather*}
y=v_{y} t-\frac{1}{2} gt^{2}\\
\begin{array}{ c c c }
-\frac{1}{2} gt^{2} +v_{y} t-y & = & 0\\
gt^{2} -2v_{y} t+2y & = & 0
\end{array}\\
\\
x=\frac{-b+\sqrt{b^{2} -4ac}}{2a}( 근의\ 공식)\\
\\
\begin{array}{ c c c }
a & = & g\\
b & = & -2v_{y}\\
c & = & 2y
\end{array}\\
\\
\therefore t=\frac{2v_{y} +\sqrt{( -2v_{y})^{2} -8gy}}{2g}
\end{gather*}
$$



#### 4. x의 초기속도(vx) 구하기

$$
\begin{gather*}
      x( 마지막\ 위치) =v_{x} \times t\\
      v_{x} =\frac{x}{t}
      \end{gather*}
$$



#### 5. 경과 시간값을 변화시키며 좌표얻기

t초 후 위치 계산 식에 t값을 변화시키며 좌표를 얻는다.

$$
\begin{equation*}
   \begin{array}{ c c c }
   x & = & v_{x} t\\
   y & = & v_{y} t-\frac{1}{2} gt^{2}
   \end{array}
   \end{equation*}
$$



```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.EventSystems;

public class ParabolaAlgorithm
{
    public float HeightLimit { get; private set; }
    public float TimeToTopmostHeight { get; private set; }
    public float TimeToEndPosition { get; private set; }

    private Vector3 _startPosition;
    private Vector3 _endPosition;

    private float _vx;
    private float _vy;
    private float _gravity;

    public Vector3 GetPosition(float elasedTime)
    {
        float x = _vx * elasedTime;
        float y = (_vy * elasedTime) - (0.5f * _gravity * elasedTime * elasedTime);

        return new Vector3(_startPosition.x + x, _startPosition.y + y, 0f);
    }

    public void Init(float heightLimit, float timeToTopmostHeight, Vector3 startPosition, Vector3 endPosition)
    {
        this.HeightLimit = heightLimit;
        this.TimeToTopmostHeight = timeToTopmostHeight;

        _startPosition = startPosition;
        _endPosition = endPosition;

        CalcParabolaTrack();
    }

    private void CalcParabolaTrack()
    {
        float endHeight = _endPosition.y - _startPosition.y;
        float height = HeightLimit;
        //float height = MaxHeight - transform.position.y;
        _gravity = 2 * height / (TimeToTopmostHeight * TimeToTopmostHeight);

        _vy = Mathf.Sqrt(2 * _gravity * height);

        float a = _gravity;
        float b = -2 * _vy;
        float c = 2 * endHeight;

        TimeToEndPosition = (-b + Mathf.Sqrt(b * b - 4 * a * c)) / (2 * a);

        //Debug.Log(TimeToEndPosition.ToString("#.###"));

        _vx = (_endPosition.x - _startPosition.x) / TimeToEndPosition;
    }
} 
```







참고

<http://blog.naver.com/PostView.nhn?blogId=whwodud98&logNo=50103673919>

<https://www.slideshare.net/semin204/ss-16331290>

[https://robatokim.tistory.com/entry/%EA%B2%8C%EC%9E%84%EC%88%98%ED%95%99-%EC%97%AD%ED%83%84%EB%8F%84%EA%B3%84%EC%82%B0%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%91%90%EC%A0%90-%EC%82%AC%EC%9D%98-%ED%8F%AC%EB%AC%BC%EC%84%A0-%EA%B5%AC%ED%95%98%EA%B8%B0](https://robatokim.tistory.com/entry/게임수학-역탄도계산을-이용한-두점-사의-포물선-구하기)

[https://0mind.tistory.com/entry/%ED%8F%AC%EB%AC%BC%EC%84%A0%EC%9A%B4%EB%8F%99-%EA%B3%B5%EC%8B%9D](https://0mind.tistory.com/entry/포물선운동-공식)