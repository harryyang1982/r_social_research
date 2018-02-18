---
title: "4장 - R프로그래밍 기초 1"
author: "양승훈"
date: '2018/2/7'
---

## 안내

이제 본격적으로 R을 다룬다. 주의해야 할 사항은 다음과 같다.

* 교수가 진행하는 코드를 오타 없이 타이핑 한다. 대부분의 문제는 오타에서 발생한다.
* 수업시간은 빠르게 흐른다. 졸 새가 없을 것이다. 잠깐 흐트러지면 다음 시간에 무엇을 배웠는지 까먹기 일쑤다. 충분한 휴식시간이 보장되니, 수업시간에는 최대한 집중할 수 있도록 한다.
* 수업의 내용을 한 번은 복습하는 게 좋다. 복습시간은 보통 2시간 수업 후에 10분을 넘기지 않는다. 한 번만 코드를 읽어보고 무엇을 했는지를 되새겨 보면 A+ 학점을 받고, 다른 학기의 모든 수업에서 데이터 분석 기법을 활용할 수 있게 된다. 데이터분석 기법은 사회학 뿐만 아니라, 앞으로 회사생활이나 다른 일을 하게 될 때에도 요긴하게 쓸 수 있는 기술이다. 늘 '실전용' 기술이라고 생각하고 배우는 것이 좋다.

## R Programming 기초 1-1 : 숫자연산

모든 프로그래밍 언어는 기본적으로는 계산기이다. 계산기를 써본 학생들은 모두 알겠지만, 숫자를 치고 연산자(+, -, *, / 등)를 누르면 값이 나온다. 프로그래밍 언어가 계산기보다 조금 더 나은 것은 '변수'를 지정해 저장할 수 있다는 것인데, 이 변수 형태는 가장 기본적인 데이터 형식이라고 말할 수 있다. 이런 변수의 기본 단위를 R에서는 **벡터**라고 부른다.

벡터를 만들어 보면서 설명하겠다. 벡터는 숫자, 문자가 기본이다. 숫자는 자연수, 0 등을 포함한 정수(integer)와 실수(real number, R에서는 double)로 나뉜다. 간단한 연산과 벡터 지정을 해보자. 

* 모든 연산은 Ctrl + 1 번 키를 눌러 'source' 창에서 진행하도록 한다.

### 벡터 할당

R에서 어떤 벡터에 값을 집어넣을 때 "<-" 기호를 쓴다. "A <- 30"이라고 치면 A라는 변수에 30이라는 값을 집어넣는 셈이다. 

변수는 1개의 값 뿐만 아니라, 많은 숫자의 값도 집어넣을 수 있는데, 그 때는 c()를 활용한다. c()는 1개의 벡터도 만들 수 있다. 

예를 들면: "k <- c(30, 40, 50)" 같은 식으로 입력하면, k는 30, 40, 50이라는 값을 포함하는 숫자 벡터가 된다. 

이렇게 값을 집어넣는 것을 변수에 값을 **할당**한다고 표현한다. 아래의 예를 실행해 보자.

```{r numeric calculation}
# 벡터와 연산자

## 벡터 만들기

x <- c(80, 85, 70)
x 

c(80, 85, 70) -> x
x

## 벡터 원소가 하나일 때

x <- c(80)
x

x <- 80
x
```

#### 연습 문제

1. y에 10을 할당하시오.
2. z에 1, 3, 5, 7, 9를 할당하시오.
3. k에 -1, 1, 3, -5, 7를 할당하시오. 결과는 어떻게 되는가?

### 벡터 연산과 산술 연산

이제 본격적으로 벡터로 된 변수를 가지고 연산을 해보자. R은 연산하는 과정을 통해 나온 값도 변수에 할당할 수 있다. 예를 들면 "x <- 3+5"를 입력하면 x에는 8이라는 값이 할당 된다. 아래의 예제를 실행해 보자.

```{r vector calculation}
## 산술 연산

x <- 5+2 ### 더하기
x

x <- 5/3 ### 나누기
x

x <- 5^2 ### 자승
x

x <- 5%%3 ### 나눌 때의 나머지
x

x <- 5%/%3 ### 몫
x

## 벡터와 사칙연산

x <- c(1,2,3,4)
y <- c(2,3,4,5)
z <- c(1,2)

w <- x+y
w

w <- x+5
w

w <- y/2
w

w <- x+z
w

w <- x/z
w

w <- z/x
w

```

우리는 벡터값을 통해서 사칙연산이 가능함을 확인할 수 있다. 특이한 점은 벡터가 포함한 원소의 개수이 다른 x와 z의 계산이다. x를 z로 더하면, 1+1, 2+2, 3+1, 4+2 같은 방식으로 수행돼 x는 c(2, 4, 4, 6)의 값이 할당된다. z의 갯수(길이)가 2배로 자동으로 곱해지는 것이다. 이러한 특성은 나중에 데이터를 분석할 때에도 요긴하게 사용되거나 헷갈리게 작용되기도 한다. 참조하자.

### 문자 벡터 처리

앞서서 프로그래밍 언어가 계산기에서 출발했다고 언급했다. 그러나 프로그래밍 언어는 숫자 뿐 아니라 문자도 처리할 수 있다. 예를 들어 "x <- "A"" 라고 입력하면, x에 A라는 문자열이 값으로 입력되는 것이다. 문자도 숫자와 마찬가지로 c()를 통해서 여러가지를 입력할 수 있다.

```{r character operation}

x <- c(1,2,3) ###숫자
x

y <- c("A", "B", "C") ###문자
y

y <- c("A", 1, 2) ###문자일까 숫자일까
y

```

흥미로운 것은 문자와 숫자를 같이 처리했을 때다. typeof라는 명령어를 통해 각 변수의 속성을 파악해 보자.

```{r typeof}

typeof(x)

typeof(y)

```

x는 숫자로, y는 문자로 파악된다. 즉, 문자와 숫자를 같이 할당하면 결과가 문자로 변환된다. 나중에 다양한 데이터를 불러서 작업을 하다보면 숫자인데 문자로 속성이 나오는 경우가 있다. 그럴 때 내용을 살피면 문자 한 두 개가 섞여 있는 경우가 허다하다. 이럴 때는 그러한 내용들을 결측(NA)처리 해줘야 한다. (결측에 대해서는 나중에 확인 하도록 하겠다.)

또 하나 주의해야 할 점은 x와 y는 직접 산술이 되지 않는다는 점이다. x와 y를 더하거나 빼거나 곱하거나 나누면 에러가 발생한다. 즉 문자와 숫자는 직접 계산할 수 없다!

### 논리 연산자 벡터 처리

들어본 학생이 있을 수 있는데, 컴퓨터는 기본적으로 0과 1을 통해서 모든 연산을 처리한다. 0은 스위치를 끄는 것이고(OFF), 1은 스위치를 켜는 것이다(ON). 또한 0은 FALSE, 즉 거짓을 의미하고, 1은 TRUE, 즉 참을 의미한다. R은 TRUE, FALSE를 **논리 연산자**로 분류한다. 논리 연산자가 어떻게 처리되는지를 아래의 코드를 통해서 살펴보자.

```{r logical vector}
## 비교 연산자

x <- 5<3 ### 5가 3보다 작은지 확인하는 내용을 x에 할당
x

y <- c(10,20,30)
z <- y<=10 ### z에 y와 10을 비교해 같거나 더 작은 숫자가 있는지 확인해 논리연산자를 할당
z

## 논리 연산자

x <- TRUE ### 직접 참인 논리연산자를 할당
y <- FALSE ### 직접 거짓인 논리연산자를 할당

```

논리 연산자가 어려워 보이는데, 조금 익숙해지면 쓸모가 많다. 이런 데이터를 생각해 보자.

```{r logical operation}
k <- c("M", "F", "M", "F", "F", "F", "M", "M", "M", "M", "M", "M")
m <- k == "M"
mean(m)

```

k는 어느 반의 학생들의 성별을 입력한 벡터이다. m은 k가 "M", 즉 남자인지를 확인해서 논리 연산자로 저장한 벡터이다. 마지막 줄의 "mean(m)"은 m의 평균을 구하는 것인데, 앞서 이야기했듯이 논리 연산자 TRUE는 1, FALSE는 0으로 컴퓨터가 처리한다. 결과 값이 0.666667로 나온다. 그 결과는 무엇을 의미할까??

답은 k반 학생들 중 남성이 66.6% 있다는 의미다. 논리 연산자와 친해지면 나중에 비율로서 데이터를 분석할 때 크게 용이하게 된다. (물론 겁먹을 필요는 없다. 5장에서 더 쉽게 처리하는 방법을 배운다.)

#### 좀 더 복잡한 논리 연산자 처리

이번에는 몇 가지 기호를 더 배워보도록 하겠다. "&"과 "|"이다. "&"는 "그리고(and)"라는 뜻이다. 산술기호로 하면 곱하기(*)를 의미한다. 고등학교 수학시간에 배운 교집합을 의미하기도 한다. "|"는 "또는(or)"이라는 뜻이다. 산술기호로 하면 더하기(+)를 의미한다. 사례를 살펴보자.

```{r logical operation2}
x | y

x & y

x <- 3
!x

isTRUE(y)

z <- c(TRUE, FALSE, FALSE)
z|y

```

x 또는 y인 경우를 보는 것이 첫 번째의 코드다. 앞서 봤듯이 x가 TRUE이고, y는 FALSE이다. 

x 또는 y는 참 또는 거짓이라는 말인데, 이게 헷갈리면 0 + 1을 생각해보면 된다. 0 + 1은 1, 즉 참이다. 
x 그리고 y는 참 그리고 거짓이라는 말이다. 역시 헷갈리면 0*1을 생각해보면 된다. 0*1은 0, 즉 거짓이다.
"x <- 3"을 할당하고 !x를 확인하면 값이 FALSE가 나온다. "!" 연산은 x의 부정이라는 말인데, x가 3이라는 값이 있는 '참'이기 때문에, !x는 거짓이 된다. (이건 좀 헷갈릴 수 있으니 다른 예로 해보자.)
isTRUE(y)는 y가 참인지를 확인해 달라는 명령어다. 앞서 y에 FALSE, 즉 거짓을 입력했으므로 isTRUE(y)는 FALSE를 답하게 된다.

z는 논리연산자를 모아서 벡터로 할당한 것이다. z|y는 어떻게 진행될까? z는 TRUE, FALSE, FALSE 그리고 y는 FALSE다. 답은 TRUE, FALSE, FALSE가 될 것이다. 왜 그런지는 생각해 볼 것!

#### 연습문제
* a <- c(TRUE, FALSE, FALSE) 를 할당하고, b <- c(FALSE, FALSE, TRUE)를 할당한 후 a&b와 a|b의 값을 생각해 보시오. 그리고 코드를 통해 확인해 보시오.

### 연속 벡터와 반복 벡터 만들기

이번에 배워볼 것은 연속 벡터와 반복 벡터를 만드는 것이다.

#### 연속 벡터 처리

예를 들어, 1부터 100까지 1씩 올라가는 벡터를 만들고 싶다. 일일이 1부터 100까지 칠 것인가? 이건 뭔가 컴퓨터에 대한 모독이자, 손에 대한 혹사가 아닐까? 프로그래밍의 목적은 '노가다'를 최소한으로 줄이는 것이다. R 역시 그런 '노가다'를 줄이기 위한 방법을 갖고 있다. 그럼 어떻게 해야 할까? 아래의 코드를 보자.

```{r sequence operation}
## 연속 값으로 벡터 만들기 

x <- 1:100
x

y <- 100:1
y

x <- seq(1, 100)
x

x <- seq(100, 1)
x

x <- seq(1, 100, by=3)
x

y <- seq(1, 100, length.out=5)
y

```

먼저 "1:100"과 같은 방식으로 연속되는 숫자 벡터를 만들 수 있다. 1:100이라고 치면 1,2,3,4,5,....100까지 숫자가 나온다. ":" 명령어는 반대로도 쓸 수 있다. 즉 100:1을 치면 100부터 1까지 100,99,98,97,.....1까지 숫자가 나온다.

좀 더 세련된 방식으로 정리한 명령어가 있다. 그게 바로 위의 seq 명령어다. 예를 들어 1부터 100까지 순서대로 벡터를 만들 경우, seq(1, 100)이라고 치기만 하면 된다. 그러면 마찬가지로 1,2,3,4,5,...100까지 숫자가 나온다. 반대로 숫자를 나래비 세울 경우 seq(100, 1)이라고 치면 된다. 

그런데 만약, 숫자를 3씩 건너뛰면서 만들고 싶다면 어떨까? 예를 들면 1, 4, 7, .... 100까지 말이다. 이럴 때는 인자(argument)를 추가해줘야 한다. 인자는 명령어(함수)에 보조적으로 필요한 부분을 추가할 때 쓴다. 

"seq(1, 100, by = 3)" 를 입력해 보자. 그러면 1, 4, 7, .... 100까지 입력이 된다.

그런데 만약 1부터 100까지 몇씩 건너뛸지는 모르지만 하여간 5개만 뽑아보고 싶을 수 있다. 그럴 때 쓰는 인자가 "length.out"이다.

"seq(1, 100, length.out=5)"라고 입력해 보자. 그러면 1, 25.75, 50.50, 75.25, 100.00 이라는 값을 얻을 수 있다.

이런 벡터 처리 방식을 연속 처리, 즉 **시퀀스 처리**라고 한다.

#### rep()와 반복 처리

이번에는 **반복 처리**를 해보자. 이런 경우를 생각해 보자. 만약 1을 100번 z라는 벡터에 저장하려면 어떻게 해야 할까? 1, 1, 1, 1, 1, 를 100번 치다보면 반드시 '뻑'이 날 것이다. 갯수가 안 맞거나, 오타 때문에 에러가 날 것이다. 좀 더 세련된 방식을 생각해 보자. R은 이런 고민을 해결하기 위해서 rep()라는 명령어를 만들었다. 

```{r rep}

rep(1, 100)

```

제일 먼저 rep(1, 100)은 1을 100번 반복해서 만들라는 명령어이다. 1, 1, 1, 1, ... 1이 나온다. 옆에 보면 [1] 같은 방식이 나오는데, 이것은 벡터의 숫서를 의미한다. 쭉 보면 100개가 제대로 됐음을 확인할 수 있다.

이번에는 벡터 단위로 생각해 보자. (앞서 배운 seq()를 함께 생각해 봐도 좋을 것이다.) 1,2,3으로 구성된 숫자 벡터 x를 2번 반복하려면 어떻게 하면 될까? rep(x, 2) 또는 rep(x, times=2)라고 치면 1,2,3,1,2,3이 된다. 그런데 1,2,3을 각각 반복하려면 어떻게 하면 될까? 즉 1,1,2,2,3,3 말이다. 이럴 때는 rep(x, each=2)를 입력하면 된다. 

```{r rep2}
x <- c(1,2,3)
rep(x, times=2)

rep(x, each=2)

```

#### 연습문제

1. a에 숫자 벡터 5, 7, 13, 20을 만드시오. 그런 후 a를 전체 반복(times)하여 b에 할당하고, a를 갭려 반복(each)하여 c에 할당하시오. 그리고 b와 c를 확인하시오.

### 고급 : 벡터 잘라내기

이번에는 벡터를 잘라내는 방법을 배워보겠다. 무슨 말인지 이해가 쉽지 않을 것이다. 벡터를 자른다는 것은 벡터의 순서를 확인하여 그 부분을 잘라내거나, 논리 연산자를 활용하여 벡터를 추려해는 것을 의미한다.

예를 들어 a 벡터에 c(5, 7, 13, 20)이 들어 있을 때 첫 번째와 두 번째만 뽑아서 쓰고 싶다면 어떻게 해야 할까? 이럴 때 쓰는 것을 **인덱싱(indexing)**이라고 한다. 방법은 a[c(1,2)]이다. 만약 한 개만 뽑아 내고 싶다면 a[1] 같은 방식으로 쓸 수 있다. 예제를 통해서 살펴보자.

```{r vector indexing}

x <- c(1,2,3,4,5)

x[c(1,3,5)]
x[-c(2,4)]

```

x에 1부터 5까지의 숫자를 넣는다. x에서 1,3,5번째 숫자만 뽑아내는 것이 두 번째 명령어이다. 그런데 만약 2번째와 4번째만 빼고 싶을 수도 있다. 그럴 때는 c 앞에 "-" 기호를 붙여주면 된다. x[-c(2, 4)] 같은 방식으로 말이다. 그것이 세 번째 명령어이다.

#### 연습문제

1. a <- c(8, 7, 5, 3, 3, 1, 8, 6) 을 할당하고, 이 중 6번째 숫자만 추출하는 명령어를 만들어 보시오.
2. a에서 2, 4, 7번째 숫자만 추출하시오.
3. a에서 1, 7, 8번째 숫자만 빼고 나머지를 추출하시오.

#### 조건식을 활용한 벡터 인덱싱

벡터를 처리할 때 조금 더 나아가 조건식을 쓸 수도 있다. 앞서 언급한 x>3, x>=4 이런 방식 말이다. 예제를 통해 확인 하자.

```{r}
x[x>2]

x[x>=2 & x<=4]

x[2] <- 20
x

x[c(3,4)] <- 15
x

x[x<=15] <- 10
x

```

첫번째 코드는 x 중 x가 2보다 큰 숫자가 있을 경우 그것들만 출력해 달라는 명령어이다. 두번째 코드는 x가 2보다 크거나 같고, 4보다 작거나 같은 숫자만 출력해 달라는 명령어이다. 

인덱싱을 활용하여 벡터에 값을 할당할 수도 있다. "x[2] <- 20" 이라는 명령어를 입력하면 벡터 x의 2번째 항목의 값을 20으로 바꾸어 할당할 수 있게 된다. 마찬가지로 x[c(3,4)] <- 15를 입력하면 벡터 x의 3번째, 4번째 항목의 값을 15로 바꾸어 할당할 수 있게 된다. 마지막 x[x<=15] <- 10을 입력하면, 벡터 x의 값 중 15보다 작거나 같은 숫자가 있을 경우 그것들을 모두 10으로 바꿔 할당하라는 의미가 된다.

### 벡터의 기초 통계 확인 하기 ###

벡터를 만들었으면 써먹어야 한다. 엑셀을 배울 때 활용했던 명령어들을 떠올려 보자. SUM, AVERAGE 등등이 있다. R에도 당연히 그런 명령어들이 있다. 익혀보도록 하자.

```{r}

x <- seq(1, 10)
sum(x)

mean(x)

var(x)

sd(x)

sqrt(x)
var(x) ^ (1/2) == sd(x)

length(x)

x <- c(1,2, -3)
abs(x)


```

우선 x를 만들었다. 1, 2, 3, 4, ... 10이다. 이 값들의 합을 구하는 명령어는 **sum()**이다. **mean()**은 벡터의 평균을 구한다. **var()**는 벡터의 분산을 구한다. **sd()**은 표준편차를 구한다. **sqrt(x)**는 양의 제곱근을 구하는 명령어이다.

그런데 조금 더 나아가 보자. 직접 분산과 표준편차가 맞는지 확인해 보자. 분산에 제곱근을 씌우면 표준편차가 된다. 달리 말하면 sqrt(var(x))는 sd(x)와 같아야 한다. 혹은 var(x) ^ (1/2)는 sd(x)와 같아야 한다. "var(x) ^ (1/2) == sd(x)"는 분산의 제곱근과 표준편차가 같은지를 확인하는 명령이다. "=="는 같은지를 확인하는 명령어이다. 

length()는 벡터의 갯수(길이)를 구하는 명령어이다. abs()는 절대값을 구하는 명령어이다.

#### 연습 문제
- x를 활용해 sum()과 length()를 활용해서 평균을 구하는 함수를 만들고 이를 mean()과 비교해 보시오.

### 결측값: NULL, NA(not available), NaN(Not a Number)

이따금 데이터를 보다보면 NA를 빈번히 발견하고, 계산을 하다보면 NaN을 발견하게 되는 경우가 있다. 드물지면 NULL을 발견하는 경우가 있다. NA는 입력하다가 빠진 경우, 즉 **결측값**을 의미한다. NaN은 0을 0으로 나누는 등 계산될 수 없는 경우를 의미한다. NULL은? 그냥 빈 것으로 가정하는 값을 의미한다. (해석이 어렵다...)

코드를 통해 이러한 값들을 어떻게 처리할 수 있는지 확인해 보자.

```{r NA operation}

x <- NULL
is.null(x)

y <- c(1,2,3, NA, 5)
y

z <- 10/0
z

w <- 0/0
w


```

is.null()은 벡터의 값이 NULL인지 아닌지를 확인하는 명령어다. z처럼 10을 0으로 나누면 무한대의 값이 나오는데, 이럴 때는 Inf라는 값이 나온다. 앞서 언급한 것처럼 0을 0으로 나누면? NaN이 나온다.

## R Programming 기초 1-2: 데이터 구조

지금까지 살펴본 것은 모두 벡터(vector)이다. 엑셀로 치면 한 개의 변수, 열을 의미한다. 이제 이 공간을 확장해 보도록 하겠다. 일단 몇 가지는 생략한다. R에는 array, matrix, list 등의 다양한 데이터 형태가 있지만, 우리 수업에서는 오로지 **데이터 프레임**data.frame만 배우기로 한다. 

### 데이터 프레임
**데이터 프레임**은 엑셀에서 봤던 [X,Y] 형태로 된 데이터이다. X는 행, Y는 열이다. 이걸 잊어선 안 된다. 행과 열이 헷갈리면 오류가 끝나지 않는다.

```{r dataframe 1}
## 두 명의 고객 정보로 데이터 프레임 만들기
x <- data.frame(name=c("홍길동", "손오공"), age=c(20,30), address=c("서울", "부산"))
x

```

x는 가장 간단한 형태의 데이터 프레임이다. 3개의 열(변수:name, age, address)을 갖고 있고, 2개의 행(홍길동과 손오공의 기록 2개)을 가진 데이터 프레임이다. 즉 [2 x 3]의 데이터 프레임인 것이다.

앞으로 만지게 될 모든 데이터는 데이터프레임이 될 것이다. 데이터프레임은 벡터들을 각각의 열로 구성하는 형태의 데이터 구조라고 볼 수 있다. 이것을 잊어서는 안 된다.

데이터 프레임에는 행과 열을 자동으로 추가할 수 있는 데 이 명령어를 rbind() (행추가), cbind() (열추가) 라고 한다. 

```{r binding columns and rows}

# 열과 행 단위 추가
x <- cbind(x, dep=c("e-비즈", "경영"))
x

x <- rbind(x, data.frame(name="장발장", age=40, address="파리", dep="행정"))
x


```


#### 데이터 프레임에서 값 추려내기(인덱싱)

앞서 벡터에서 배운 것처럼 데이터 프레임에서도 인덱싱이 가능하다. 예를 들어보자. 아래의 코드를 보자.

```{r df vector indexing}
x[3,2] # 3행의 2열 값 보기
x[3,] # 3행만 보기
x[,2] # 2열만 보기
x[-2,] # 2열만 빼고 보기
x["name"] # "name"에 해당하는 행만 보기
x$name # name에 해당하는 행만  보기(위와 같음)
x[["성명"]] # name에 해당하는 행의 요소만 보기(위와 같아 보이나 벡터 이름(label)이 빠짐)
x[[1]] # 1행의 요소만 보기
x[[1]][2] # 1행의 요소 중 2번째 보기
x[1,2] <- 21 # 1행, 2열의 값을 21로 바꾸기
x

x[1, "나이"] <- 22
x
```

이러한 연산 모두를 암기할 필요는 없다. 나중에 손에 익은 것들을 살피면 되고 한 학기 내내 할 일들이다. **겁먹지 말것**. 

* 결과에 대해서는 함께 토론해 보도록 하자.

### 데이터 읽고 불러오기

지금까지는 벡터나 데이터 프레임을 만들어 왔다. 하지만 이렇게 해서는 '빅 데이터 시대'에 노가다만 하다가 하루가 끝난다. 앞으로 수업에서는 데이터 프레임을 만들 일이 없다. 계속해서 남이 만든 데이터를 활용할 예정이다. 그러기 위해서는 남이 만든 데이터를 불러다가 실행할 수 있어야 한다. 그 방법을 찾아보자.

#### 내부 데이터 읽어오기

R은 그 자체로 많은 데이터프레임을 갖고 있다. 어떤 데이터들이 있는지 확인하려면 data() 를 입력해 보면 된다. 해보자.

```{r data sets}

data()

data(package = .packages(all.available = TRUE))

```

"data()"를 입력하면, baseR, 즉 R 자체에 깔려 있는 데이터를 보여준다.
"data(package = .packages(all.available = TRUE))"를 입력하면, RStudio에 깔려 있는 데이터 전체를 보여준다. 수십~백개가 넘는 데이터를 우리는 사용할 수 있다. (**그렇다고 다 사용하는 건 아니다**)

그럼 가장 많이 사용되는 한 두개만 불러보자.

```{r load data sets}

data(mtcars)
data(quakes)

head(mtcars)
head(quakes)

```

앞서 엑셀로 만져봤던 mtcars 데이터와, 지진에 대한 정보인 quakes 데이터를 확인할 수 있다. data() 명령어를 실행하고 나면, RStudio 우측 상단 'Environment'에 mtcars와 quakes가 생겨난 것을 볼 수 있다. mtcars는 "32obs. of 11 variables"란다. 32 행 X 11 열이라는 이야기다. quakes는? 1000행 X 5행임을 파악할 수 있다. head()는 맨 앞의 6개 행만 불러다 보여주는 명령어다. head(mtcars, 10) 같은 방식으로 두 번째 인자의 숫자를 지정하면 그 숫자만큼 나온다. (앞으로는 더 쉽게 확인하는 방법도 배울 것이다.)

mtcars와 quakes는 어떻게 생긴 데이터일까? 앞으로 배우는 모든 데이터는 아래와 같은 방식으로 검증해 보면 대략의 내용을 파악할 수 있다.

```{r summary functions}

head(quakes, n=10) # 처음 10행만 보여주기
tail(quakes, n=6) # 맨 뒤 6행만 보여주기 --> 개수를 세기 좋다.

names(quakes) # 열의 이름을 보여주기
str(quakes) # 문자, 숫자, 팩터(나중에 배움), 날짜 등의 속성을 보여줌

dim(quakes) # 몇 행, 몇 열인지를 알려줌

summary(quakes) # 전체 데이터프레임의 요약을 보여줌

summary(quakes$mag) # 데이터프레임의 특정 열의 요약을 보여줌

```

주목할 것은 summary() 명령어이다. summary() 명령어를 실행하면, 분위 계수(엑셀의 QUARTIL.EXC)를 보여주고 중위값(median), 평균(mean), 최소값(min), 최대값(max) 모두를 보여준다. 데이터를 보고 뭐가 뭔지 모를 때는 summary()를 실행하면 된다. (나중에 배울 glimpse()가 더 좋긴 하지만..)

#### 외부 데이터 읽어오기

그러나 더 많은 데이터는 R '바깥'에 더 많다. 수 많은 엑셀파일과 csv파일이 굴러다닌다. 이것들을 어떻게 읽을 수 있을까? 그럴 때 필요한 명령어가 read.csv() / dplyr::read_csv()과 readxl::read_excel() 명령어이다. 아래와 같은 방식으로 실행한다.

```{r echo=F, eval=F}

readr::write_csv(quakes, "quakes.csv")
```


```{r read outside }
library(readr)
#x <- read_csv("파일명")
#x

library(readxl)
#x <- read_excel("파일명")

```

파일이름만 read_csv, read_excel에 넣으면 된다. 그러고 나면 x에 데이터프레임이 할당된다.

마지막으로 가져올 데이터가 파일이 아니라, 온라인 상에 있을 때가 있다. 그럴 때도 큰 차이는 없다. 아래의 코드를 참조해 보자.

```{r read online}
url <- "https://vincentarelbundock.github.io/Rdatasets/csv/datasets/Titanic.csv"
x <- read.csv(url)
head(x)
```

url이라는 문자 벡터를 만들어, read.csv() 명령어를 통해 불러와 x에 할당했다. 그리고 처음 6개 행을 확인했다. 이런 방식으로 외부의 데이터도 R에서 충분히 활용할 수 있다. 만약 xlsx 파일이라면? read_excel을 쓰면 된다.

### 다음 시간 안내

다음 시간에는 R프로그램이 기초(2)를 배운다. 다음 장까지 마치고 나면 세상의 모든 데이터를 수월하게 다룰 수 있게 된다.
5장: R프로그래밍 기초(2): tidy 문법 익히기 