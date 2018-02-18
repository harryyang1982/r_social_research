---
title: "2장 - R/Rstudio 프로그램 설치와 기본 활용법(단축키)"
author: "양승훈"
date: '2018/2/6'
---

## R/RStudio 프로그램 설치

* R 설치

[CRAN](https://cran.r-project.org/) 에 접속하여 각자의 운영체제를 고려하여, **R for Windows** 또는 **R for OS X**의 최신 버전을 다운 받는다.

![CRAN 화면](http://cfile26.uf.tistory.com/image/99D4EF335A0B36B6127F44)
![설치 화면](http://cfile25.uf.tistory.com/image/99C5CC335A0B36B6147115)
![설치 화면2](http://cfile1.uf.tistory.com/image/99C7EC335A0B36B714AA6E)

* RStudio 설치

[RStudio](https://www.rstudio.com/products/rstudio/download/) 에 접속하여 각자의 운영체제를 고려하여 RStudio의 최신 버전을 다운 받는다. 

![RStudio 화면](http://cfile2.uf.tistory.com/image/995CB6335A0B3C221B8E50)
![Rstudio 선택 화면](http://cfile5.uf.tistory.com/image/995B25335A0B3C231B78BE)

RStudio는 상업용 사용이나, 서버용으로 나온 유료판이 있기 때문에 무료판(FREE, 맨 왼쪽 아래)을 다운 받도록 한다.

![RStudio 선택 화면](http://cfile8.uf.tistory.com/image/995D95335A0B3C231BF436)

최신의 RStudio를 선택하면 된다. (최 상단)

![RStudio 설치 화면](http://cfile4.uf.tistory.com/image/995D31335A0B3C241B0F29)

## 콘솔의 기본 활용법

![RStudio 실행 화면](http://cfile4.uf.tistory.com/image/995DB1335A0B3C241B57D1)

위의 화면을 살펴 보자. 왼쪽에 있는 화면을 콘솔이라고 한다. **Control + Shift + N** 키를 눌러보자. 'Untitled1'이라는 화면이 왼쪽 위에 생긴다. 이것을 소스창이라고 한다.

오른 쪽 상단에는 **Environment/History/Connections**라는 메뉴 버튼이 있고, 아래에 파일을 불러오고 저장하는 아이콘이 있다. 순서대로 보면 1) 데이터 파일 열기, 2) 데이터 파일 저장, 3) 데이터 불러오기(csv/xlsx 등등), 4) 데이터 지우기 순이다. 작업을 하다가 엉킬 경우, 주저하지 말고 빗자루 모양의 데이터 지우기 버튼을 누르면 된다.

오른 쪽 하단에는 **Files/Plots/Packages/Help/View** 메뉴 버튼이 있다. 그 아래에는 다양한 그래프를 선택할 수 있는 화살표, 작은 그래프를 확대시켜주는 줌(Zoom), 그래프를 그림파일로 저장할 수 있는 Export 메뉴 버튼이 있다. 그 외 Packages 메뉴가 중요한데, 이 Packages 메뉴를 누르면 현재 설치된 패키지를 확인하고 업데이트 하거나 삭제할 수 있다. (**패키지에 대한 설명은 이 장의 후반에 계속할 것이다**)

## 콘솔의 초기 셋팅

아래의 콘솔창에 몇 가지 명령어를 입력해 보자. 학교 전산실 환경은 부팅을 할 때마다 모든 R과 관련된 환경이 새로 정리되므로 똑같이 수행해야 한다. (install.packages 명령어에 있는 repos 이하는 생략해도 된다.)

```{r initial packages}

install.packages("tidyverse", repos = "http://cran.r-project.org")
library(tidyverse)

```

처음으로 R을 통해서 명령어를 입력한 셈이다. 두 가지를 해석해 보자면, 
첫 번째 install.packages는 R에서 다양한 통계적 표현을 도와주는 명령어의 묶음인 패키지를 설치하는 명령이다. install.packages**("패키지 이름")**의 형태로 입력한다.
두 번째 library는 설치한 패키지를 메모리에 불러와, 패키지 안의 명령어를 쓸 수 있게 하는 명령어이다. library(**패키지 이름**) 방식으로 입력한다.

한 학기 수업을 진행하면서 tidyverse 패키지 외에는 설치할 패키지가 별로 없다. 왜냐하면 tidyverse 패키지 안에 우리가 앞으로 사용하게 될 dplyr(데이터 전처리), tidyr(데이터 전처리), ggplot2(데이터 시각화), readr(데이터 입출력), purrr(함수형 프로그래밍) 패키지가 모두 담겨 있기 때문이다. 물론 패키지나 명령어 모두를 지금 기억할 필요는 없다. 그저 install.packages 명령어와 library 명령어만 익히면 된다.

## 주요 단축키 일람

* 가장 중요한 R의 단축키는 **Alt + Shift + K** 버튼이다. 왜냐하면 이 단축키를 누르면 모든 다른 단축키를 확인할 수 있기 때문이다(!).

* 파일 처리 단축키 : 자주 빈번하게 쓰는 단축키는 아무래도 파일 저장(**Ctrl + S**), 새 파일(**Ctrl + Shift + N**), 파일 불러오기(**Ctrl + Shift + O**) 버튼이다.

* 코드 주석화 단축키(**Ctrl + Shift + C**)는 현재는 큰 의미가 없지만, 앞으로 큰 의미를 가지게 될 단축키이다. 이런 저런 명령어를 입력했는데, 당장 쓸 일이 없거나. 그냥 RStudio에서 노트 필기를 했을 때 이것들을 실행시키지 않기 위해 사용한다. 처음에는 익숙하지 않다가, 나중에는 빈번하게 사용하는 자신들을 확인하게 될 것이다.

* 화면 이동 단축키(**Ctrl + 1**, **Ctrl + 2** 등등)는 4등분된 화면을 넘나드는 단축키이다. 1~5까지 하나하나 차례대로 눌러보면, 자신이 필요한 화면에 커서를 단축키를 통해 움직일 수 있다.

## 기초 연산 연습

우선 **Ctrl + 2**를 눌러 우측 화단에 콘솔에 커서를 옮겨보자.

다음과 같은 코드를 실행하면서 연산이 잘 되는지를 실험해 보자.

```{r basic calculation}

# 기초 연산

1 + 1 ### 더하기

7 - 2 ### 빼기

2 * 8 ### 곱하기

16 / 4 ### 나누기

16 %/% 2 ### 16을 2로 나눈 몫

16 %% 3 ### 16을 3으로 나눈 나머지

# 복잡한 연산

(-3 + (3 ^ 2 - 4 * 5 * 1)) / 2 * 1 ### (x^2+3x+5)를 푸는 근의 공식

3^2 * pi ### 반지름이 3인 원의 넓이

```

다음 시간에는 엑셀을 통한 자료 만지기를 진행한다.

3장: 엑셀 익히기(vlookup, 데이터 패키지 익히기)
4장: R프로그래밍 기초(1): 숫자 연산, 변수 지정, 데이터 구조, 함수형 프로그래밍(for-loop / map)
5장: R프로그래밍 기초(2): tidy 문법 익히기
