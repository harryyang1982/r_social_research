---
title: "3장 - 엑셀 익히기"
author: "양승훈"
date: '2018/2/6'
---

## 데이터 구조 익히기

수업시간에 만지게 될 모든 자료는 **행**과 **열**로 구성되어 있다고 봐도 과언이 아니다. 우리 입에 익은 읽는 순서는 행렬의 행과 열이지만, 분석을 할 때는 열과 행을 생각하는 것이 편리하다. 

아래의 엑셀 화면을 보고 생각해 보자.

![엑셀 시트 예제](http://cfile30.uf.tistory.com/image/2713A43C52E7918805B584)

#### 열
열에는 변수가 담긴다. '국어', '영어', '수학', '평균'이 각각의 변수를 뜻한다.

#### 행
행에는 기록이 담긴다. 홍길동의 기록행에는 90(국어), 95(영어), 수학(85)가 오고, 평균은 90점이다.
마찬가지로 홍길순의 기록행에는 80, 90, 85, 85이 온다.

### 열과 행 다루기: 평균과 합계
엑셀에서 가장 많이 다루는 함수는 'sum'과 'average'이다. sum은 합계를 구하고, average는 평균을 구한다. 마지막 열과 마지막 행에 적용을 해보면, 다음과 같다.

"SUM(B2:B6)"으로 명령어를 넣으면 모두의 국어 성적 합계가 나온다. 이를 **B열의 합계**라고 부를 수 있다. 
반대로 **2행의 합계**도 구할 수 있다. "SUM(B2:E2)"라고 입력하면 된다.

### 연습 문제
* C열의 합계를 구하시오.
* 강세나의 평균을 구하시오. (참조: 평균은 AVERAGE 함수를 쓴다.)
* E열 평균과 7행 평균을 비교하여 같은지 확인하시오.

## 엑셀 데이터 분석 추가하기

아래의 버튼을 눌러 데이터 분석 도구를 추가한다.

![데이터 분석 도구 추가 1](http://cfile5.uf.tistory.com/image/12171B3551392ABF2F8574)

메뉴의 '도구'를 눌러 'EXCEL 추가 기능'을 찾는다. 아래에 있는 '관리' 기능을 보면 'EXCEL 추가 기능'이 뜨는데, 여기서 '이동' 버튼을 누른다. 들어가면 '데이터 분석' 항목을 체크한 후 '확인'을 누른다.

그러고 나면 아래와 같은 내용이 우측 상단 리본에 생긴다.

![데이터 분석 도구 추가 2](http://cfile6.uf.tistory.com/image/0341123C51392B8828EC66)

이제 엑셀을 통해서 기본적인 데이터 분석과 함께 전처리를 할 수 있는 상태가 된다.

## mtcars 데이터 분석

미국 자동차 연비를 다룬 mtcars.xlsx 파일을 통해서 기본적인 통계 분석을 진행해 보겠다.

* 먼저 mtcars.xlsx 파일을 다운로드 받는다.
[링크](https://goo.gl/rZ6DPZ)

### 기술 통계 확인하기 1: 평균, 분위계수, 중위값 구하기

![mtcars 화면](https://statfactory.files.wordpress.com/2017/01/showtable.png?w=832&h=539)

mtcars 파일은 A부터 K열까지 각각 mpg, cyl, disp, hp, drat, wt, qsec, vs, am, gear, carb 등 모두 11개의 변수(열)로 구성되어 있다. 그리고 제목을 제외하고 32개 행으로 이루어져 있다. 데이터 구조로 보자면 mtcars[32, 11] 형태인 것이다.

기초 통계를 볼 때 가장 많이 활용하는 것은 평균, 분위계수(1,2,3,4 분위), 중위값 등이다.
각각의 명령어는 아래와 같다.

* AVERAGE(범위) : 평균
예: AVERAGE(A1:A10)
* QUARTILE.EXC(범위, 분위계수) : 분위계수(1,2,3,4 분위)
예: QUARTILE.EXC(B2:B32, 3) 3분위 계수를 구한다.
* MEDIAN(범위) : 중위값
예: MEDIAN(C3:C32)

#### 연습문제

* mpg의 평균과 합계를 구하시오(명령어: AVERAGE, SUM) 
* qsec의 평균과 합계를 구하시오

### 기술 통계 확인하기 2: 히스토그램 보기, 상관관계 보기, 회귀분석 하기

#### 히스토그램 그리기

기초 통계를 보면서 또한 많이 확인하게 되는 것은 바로 히스토그램이다. 히스토그램은 도수(구간)를 지정해 그 구간 안에 위치하는 값이 몇 개씩인지를 세는 것을 의미한다. 엑셀의 *데이터분석* 기능을 활용하면 손쉽게 히스토그램을 그릴 수 있다. 아래의 그림처럼 실행해 보자.

먼저 분석을 위해 오른쪽 M칸에 급간을 만들고 mpg 변수를 분석하기 위한 구간표를 짜보자.
M열에 0, 5, 10, 15, 20, 25, 30, 35를 입력해 보자.

그 후 **데이터** 리본에 달려 있는 **데이터분석** 기능을 눌러보자.

![데이터 분석 화면](http://cfile8.uf.tistory.com/image/21553F4058293C7B134BE7)

*히스토그램*을 선택하고 나면 아래와 같은 화면이 나온다.

![히스토그램](http://cfile22.uf.tistory.com/image/21490D3D58293C91094B6D)

입력 범위에 mpg 변수를 지정하고(A2:A33), 계급 구간을 정한다(M2:M9). 그리고 나면 출력 범위(O1)를 지정한다. 마지막으로 차트출력도 체크한다. 그러고 OK 버튼을 누르면 아래와 같은 결과가 나온다.

![히스토그램출력](http://cfile3.uf.tistory.com/image/2773033E58293CA2131587)

엑셀을 통해서 히스토그램을 출력했다.

### 상관관계 보기

상관관계는 각 기록(행) 변수들의 값(열)의 분포가 서로 어떤 수리적인 상관관계를 갖고 있는지를 표현하는 것을 의미한다. 엑셀의 *상관관계* 분석을 통해서 수행할 수 있다. 상관관계 값은 -1부터 1까지로 나타나는데, 0이 아무 상관관계가 관찰되지 않는 것을 의미하며, 1이나 -1은 완전한 상관관계(같은 수이거나 완전한 역수이거나)를 의미한다.

곧바로 수행해보자. 

**데이터** 리본에 달려 있는 **데이터 분석** 기능을 누른 후, *상관관계 분석* 버튼을 누르면 아래와 같은 화면이 나온다.

![상관관계분석화면](http://mblogthumb3.phinf.naver.net/20150514_266/noalnose_1431565983226r3eJX_PNG/%BF%A2%BC%BF_5.png?type=w2)

우리는 모든 변수들이 어떤 상관관계를 갖고 있는지 궁금하기 때문에 범위에 ($A$2:$K$32)를 지정한다. 그 이후 확인 버튼을 누르면 곧바로 결과가 아래처럼 나온다.

![상관관계분석결과](https://github.com/harryyang1982/harryyang1982.github.io/raw/master/images/schot.png)

#### 연습문제

* 1을 제외하고 가장 높은 값을 나타내는 변수는 무엇인가?

### 기술 통계 확인하기 3: 선형회귀 그래프 그려보기

마지막으로 확인할 기술통계는 회귀분석이다. 사회조사통계 시간에 여러분을 가장 많이 괴롭힌 그래프일 것이다. 엑셀이나 R을 사용하면 손쉽게 회귀분석 결과를 확인하고, 그래프까지 그려볼 수 있다. 엑셀의 *회귀분석*을 통해서 수행할 수 있다. 회귀분석에서 중요한 값은 R-sqaure 값 그리고 p-value이다. p-value가 0.05보다 클 경우 대립가설이 기각되고 귀무가설(혹은 영가설)이 승인되기 때문에 출력된 회귀분석 값이 큰 의미가 없다고 볼 수 있다. 물론 그렇다고 p-value 값이 0.05보다 작을 경우 반드시 회귀분석 결과를 인정할 수 있는 것은 아니지만, 그럼에도 불구하고 나름대로 유의미하다는 평가는 내릴 수 있다.

곧바로 수행해 보자. 이번에는 mpg 변수와 wt 변수간의 회귀분석을 해보자. mpg(연비)에 wt(중량)이 미치는 영향을 파악해 보는 것이다. Y는 연비, X는 중량이 된다. 실행을 위해 **데이터** 리본의 **데이터 분석** 기능을 누른 후, **회귀분석** 버튼을 눌러보자.

Y값에는 mpg 변수의 값을 입력하고(A2:A32), X값에는 wt 변수의 값을 입력한 후 확인 버튼을 누른다. 그러면 아래와 같은 화면이 출력된다.

![회귀분석결과](https://github.com/harryyang1982/harryyang1982.github.io/raw/master/images/regression_schot.png)

화면을 해석해 보자. 우선 확인해야 하는 것은 R-Square 값이다. 0.752가 나온다. R-Square는 상관계수의 제곱이다. 즉 상관관계가 0.8 이상이 나온다는 의미다. 높은 상관관계를 갖고 있으므로 X(독립변수)가 Y(종속변수)를 충실히 해석하고 있다는 의미다. 맨 아래 표의 P-Value도 확인해 보자. 1.294E-10이라고 나온다. E-10은 0.1의 10승(10^-10)을 의미한다. 즉 0.0000001294를 의미한다. 0.05보다 훨씬 작으므로 회귀선을 그리는 것이 의미있다는 결과다.

그런데, 우리는 숫자를 보는 것보다는 직관적으로 그래프를 보고 결과를 확인하는 게 수월하다. 어떻게 하면 될까? 엑셀의 그래프 그리기 기능을 활용하면 된다.

mtcars 시트(아래의 시트 버튼 클릭)를 눌러서 다시 원래 데이터로 돌아간다. A열과 F열을 선택(수업시간에 설명)한 후 우측 **삽입** 리본을 눌러 **권장차트**(중앙에 위치) 버튼을 누른다. 맨 꼭대기를 보면 **분산형** 그래프가 보일 것이다. 이것을 클릭한다. 

![회귀그래프그리기](https://github.com/harryyang1982/harryyang1982.github.io/blob/master/images/regression_graph.png?raw=true)

그 후 좌측 상단의 **빠른 모양** 버튼이 있다. 그걸 누르면 몇 개의 그래프가 보이는데, 이 중 우측 하단에 f 글자가 써있는 그래프가 보인다. 이걸 클릭 한다. 그러고 나면 회귀 그래프가 그려진다. 

![회귀그래프](https://github.com/harryyang1982/harryyang1982.github.io/raw/master/images/regression_graph2.png)

그래프에는 회귀식과 회귀선, R-Square 모두가 입력되어 있다. (나중에 그릴 R 그래프는 좀 더 멋지고 화려한 모습이 될 테니 기대해도 좋다.)

### 다음 시간 안내

다음 시간에는 R프로그램 기초(1)을 배운다.

4장: R프로그래밍 기초(1): 숫자 연산, 변수 지정, 데이터 구조, 함수형 프로그래밍(for-loop / map)
5장: R프로그래밍 기초(2): tidy 문법 익히기