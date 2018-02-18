---
title: "5장 - R 프로그래밍 2"
author: "양승훈"
date: '2018/2/7'
---

## 안내

이번 시간에는 tidy문법을 배운다. tidy문법은 R을 문과생들도 배울 수 있게 기여한 Hadley Wickham과 그가 있는 회사인 RStudio에서 만든 패키지인 tidyverse 패키지를 활용한 문법이라고 볼 수 있다. 대학생들, 그리고 많은 현업의 데이터분석가들이 쓰는 패키지가 이 tidyverse 패키지이다. 

![Hadley Wickham](https://pbs.twimg.com/profile_images/905186381995147264/7zKAG5sY.jpg)

## 준비

tidyverse 패키지를 설치하고, 메모리에 불러온다.

```{r loading tidyverse}

if(!require(tidyverse)) install.packages("tidyverse", repos = "cran.r-project.org")
library(tidyverse)

```

tidyverse 패키지는 dplyr, tidyr, readr, purrr, tibble, stringr, ggplot2 등의 패키지를 포함하고 있는 메타-패키지이다. **메타-패키지**란 말은 다양한 함수를 보유한 패키지들을 다시 통합하여 하나의 패키지로 묶었다는 말이다. tidyverse 패키지 모두를 능숙하게 사용할 수 있게 되면 보통 중급 R 데이터 분석가라고 한다. 쉽게 말하면 중급 R 데이터 분석가가 되면 회사의 경영관리팀, 기획팀 등에 취업할 때 상당한 메리트를 갖게 된다. 이것을 증명하기 위한 시험은 한국에서는 **데이터분석 준전문가(adsp)**가 있다. 

고급 분석가는 machine learning(기계학습) 또는 고급 통계(SVM)를 잘 하거나, Functional Programming(함수형 프로그래밍) / Objective Oriented Programming(객체지향 프로그래밍)을 잘 하는 사람들을 뜻하며, 이들의 몸값은 보통 $100,000/year 정도 된다. 물론 고급 분석가가 되기 위해서는 통계학 외에도 선형대수 / 미적분학 같은 공대 수준 수학에 통달해야 한다. 

여러분은 중급수준의 R 데이터 분석가가 될 수 있다. 1년 정도 교수의 수업을 듣고 [R for Data Science](http://r4ds.had.co.nz/)나, [Text Mining with R](https://www.tidytextmining.com/) 정도의 기술을 익혀 텍스트 마이닝(단어 단위 분석이나 문장 분석)과 네트워크 분석 정도를 수행할 수 있다면, 충분히 고급 인력으로 취업시장에서 자리잡을 수 있다. 물론 하기 나름이다. 굳이 고급 수학을 잘 할 필요는 없고, 필요한 자료를 R이 잘 알아들을 수 있게 하다보면 모든 과정을 잘 수행할 수 있다. 기술보다 자신이 만지는 데이터를 잘 파악하는 능력이 중요할 수 있다. 수업에 집중하면 먹고 사는 문제에 조금은 수월하게 접근할 수 있다.


## dplyr : tidyR의 시작

처음 배울 tidyverse의 패키지는 바로 dplyr이다. dplyr만 잘 소화하면 어떻게 생긴 데이터든 쉽게 필요한 내용을 추려서 요약해 확인할 수 있다. dplyr은 tidyverse 패키지에 설치되어 있으므로 특별히 다시 설치할 필요가 없다.

## filter()

처음 배울 dplyr 함수는 filter()이다. filter()는 각각 행(row)을 추려내는 역할을 한다. 이 분석을 위해 dplyr에 설치되어 있는 mpg 데이터를 활용해보도록 하자. mpg 데이터는 지난 시간에 배웠던 mtcars 데이터를 조금 더 확장해서 펼쳐놓은 데이터다. 데이터를 불러보자.

```{r}
data(mpg)
glimpse(mpg)
head(mpg)
```

지금까지 쓰지 않았던 glimpse(mpg)란 명령어가 들어가 있다. glimpse는 head보다는 좀 더 자세하게 데이터 내용을 보여주는 명령어이다. glimpse 명령어를 수행하면 데이터 안의 변수가 무엇이 있는지 확인해 주고, 그 속성을 보여주며, 처음 10개 정도의 값을 가로 방향으로 펼쳐서 보여준다. 또 엑셀과 같은 방식으로 데이터를 확인하는 방법도 있다. View(mpg) 명령어를 활용하는 것이다. (곧바로 수행해 보자)

mpg 데이터에는 11개 변수가 있고, 234개 관측(행)이 있다. 이 데이터를 어떻게 요리할 지 생각해 보자. 
manufacturer은 제작사, model는 자동차 모델명, displ은 배기량, year는 출시년도, cyl은 기통, trans는 기아변속 방식을 뜻한다. drv는 구동방식이고, cty와 hwy는 각각 시내 연비/고속도로 연비를 뜻한다. class는 차의 형태 분류를 말한다.

### 연속변수 처리(continuous variable operation)

이제 몇 가지 기준으로 자동차 데이터를 분석해 보자. 우선 filter부터 배워보자. filter는 특정한 기준을 만족하는 행을 출력하는 명령어이다. 우선 시내 연비를 기준으로 생각해 보자. 

```{r}
summary(mpg$cty)
```

cty 변수를 보면 평균 16.86, 중위값 17을 보여준다. 여기서 중위값이 17보다 높은 차들만 분류해 보도록 하자.

```{r initial filter}
filter(mpg, cty > 17)
```

처음관측값의 행은 234개였는데, filter를 처리하고 나니 102개만 남았다. cty값이 17개 이상인 것만 남겼기 때문에 그보다 작은 것들이 모두 떨어져서 그렇다.

#### 연습문제

1. hwy가 10 이상인 것들만 추리시오
2. year가 2000년 이후인 것만 추리시오
3. cty가 10 미만이고, year가 2000년 미만인 것들만 추리시오. (&를 활용할 것)

### 이산변수 처리

여기서 이산변수가 무엇이지를 잠시 살펴볼 필요가 있다. 앞서 나왔던 hwy나 cty 등은 연속 변수다. 온도나 연비 등은 특정한 기준을 만든 것이 아니라, 그 값을 그저 '측정' 한 것들이다. 키, 몸무게도 마찬가지다. 반면, cyl이나 displ 같은 변수는 기준에 맞춰 숫자를 할당한다. 실린더 기통은 4개이거나 6개이거나 8개일 수밖에 없다. 이런 변수들은 나중에 factor로 분류해 처리할 수도 있다. 하지만 이 부분은 나중에 다루기로 하자.

그렇다면 이산변수는 filter와 어떻게 만날 수 있을 것인가? 예를 들어 cyl이 4인 경우만 추리면 어덯게 하면 될까? 그럴 때는 %in% 를 통해서 변수의 내용을 추릴 수 있다. 아래를 살펴보자.

```{r}
filter(mpg, cyl %in% 4)
```

물론 %in% 뒤에서 여러 개를 추려서 볼 수도 있다. cyl이 4와 6인 경우를 생각해 보자.

```{r}
filter(mpg, cyl %in% c(4, 6))
```

c()를 활용하여 cyl이 4와 6인 차종을 뽑아낼 수 있게 됐다.

#### 연습문제

1. displ이 1.8인 경우만 추려내시오.
2. displ이 2.0이고 cyl이 6, 8인 경우만 추려내시오.

### 문자열 필터

이번에는 문자열을 다뤄보자. 원리는 똑같다. 해당되는 내용을 요청하면 된다. 예를 들어보자. class가 "suv"인 차들만 필터해보자.

```{r chracter filter}

filter(mpg, class == "suv")

```

여기서는 "=="를 활용했다. 숫자가 아니기 때문에 ">"나 "<"는 활용할 수 없다. 하지만 "&"나 "|"는 가능하다. 이번에는 숫자와 문자 모두를 사용해서 필터해 보자. manufacturer가 "hyundai"이고, hwy가 25미만인 차들만 찾아보자.

```{r}
filter(mpg, manufacturer == "hyundai" & hwy < 25)
```

몇 가지 연산을 더 해겠다. 따라해 보자.

```{r}
filter(mpg, year > 2000 & class %in% c("subcompact", "suv")) #2000년 이후, subcompact이거나 suv인 차
filter(mpg, drv %in% "r" | class %in% "suv")
```

### magrittr, 읽기 쉬운 코드의 시작이자 dplyr의 완성형

지금까지 dplyr을 배우면서 filter(DF, 기준) 방식으로 코드를 입력했을 것이다. 하지만 조금 더 간결하게 해보자. 이걸 magrittr 방식이라고 하며, pipe라고 부른다. pipe를 부르는 방법은 Ctrl + Shift + M 키보드를 누르는 것이다. 아래의 코드를 보자.

```{r magrittr}

mpg %>% 
  filter(year > 2000 & class %in% c("subcompact"))

```

위의 첫번째 코드와 똑같은 결과가 나온다. 달라진 것은? 코드가 생각하는 논리대로 작성된다는 것이다. 
예를 들면 이런 것이다.

* baseR 방식 : 동사(목적어, 주변수, 나머지 변수)
* tidyR 방식 : 목적어 %>% 동사(주변수, 나머지 변수)

두 방식의 차이가 무엇일까? 실제로 데이터를 분석하는 입장에서 생각해 보자. (3분간 주변 친구와 토론을 해본다.)

### select()

이번에는 select()에 대해 배워보자. filter가 행을 추려냈다면, select는 열을 추려낸다. 즉 보고 싶은 변수를 추려낸다. mpg 데이터를 가지고 살펴보자.

``` {r select}
mpg %>% 
  glimpse #변수 확인하기

mpg %>% 
  select(model, year, class)
```

select() 명령을 통해 model, year, class 변수를 입력했다. 결과는 행은 그대로 있고, model, year, class 3가지 열만 등장했다.

그런데 보고 싶은 열이 8개이면 어떻게 하는 게 좋을까? 일일이 노가다 하는 게 적성에 맞지 않을 것이다. 전체 열이 11개인 것을 감안하면, 방법은 3가지이다. 

1. 보기 싫은 열을 "-"로 제외 - 예: mpg %>% select(-hwy, -fl, -class)
2. 보고 싶은 열을 ":"로 묶기 - 예 : mpg %>% select(manufacturer:cty)
3. 보기 싫은 열을 "-:"로 묶어서 제외 - 예: mpg %>% select(-hwy:-class)

두 가지 방법 다 실험을 해 보자.

```{r select 2}
mpg %>% select(-hwy, -fl, -class)
mpg %>% select(manufacturer:cty)
mpg %>% select(-hwy:-class)
```

어느 편이 가장 효율적일지는 그 때 그 때 다르다. 필요한 부분을 잘 추려내는 것은 분명한 능력이다.

마지막으로, 여러가지 방법을 다 섞어서 select를 해보자.

``` {r select 3}
mpg %>% select(model, year, class, -hwy, -fl)
mpg %>% select(year, cty:class, -hwy)
```

### filter()와 select()의 혼합

이제 좀 더 수를 좁혀보자. filter()와 select()를 함께 사용해보자. 필요한 행과 필요한 열을 추려낼 수 있는 것이다. 이럴 때 어떻게 하면 될까? pipe( %>% )를 두 번 쓰면 된다.

```{r filter & select}
mpg %>% 
  filter(cty > 20) %>% 
  select(model, year, cty:class)

```

model, year, cty부터 class까지의 변수가 선택되고, filter 명령어를 통해 시내연비가 20보다 큰 차종들만 선택이 됐다. 이러한 방식으로 자신이 보고 싶은 자료를 찾아보는 것을 **데이터 전처리**라고 한다. filter()와 select()는 가장 기초적인 전처리 방식이라고 볼 수 있다.

이제 본격적으로 전처리를 수행해 보자.

## group_by()와 summarise()

이런 경우를 생각해 보자. 차종에 따른 연비는 어떻게 다를까? 차종을 filter하고 연비를 filter하는 것이 아니다. 차종에 따른 연비들의 평균이나 합계가 나와줘야 하는 것이다. 엑셀을 쓰다보면 '피벗 테이블(pivot table)'을 쓰는 경우가 있는데, 이 경우가 바로 그렇다. dplyr 패키지는 group_by()와 summarise()라는 명령어를 통해 이 문제를 해결하게 도와준다.

예를 들어보자. 위에서 언급한 차종에 따른 고속도로 연비 평균을 구해보자. 우선 실행해야 하는 것은 group_by()이다. group_by(기준 변수)를 실행한 후 결과를 보자.

```{r group_by}
mpg %>% 
  group_by(model)
```

결과를 보면 "Groups: model [38]"이라는 한 줄이 추가되었을 뿐, 특별한 변화가 없다. 하지만 이건 기준을 잡았으니, 다음 연산을 하라는 이야기다. 이제 summarise()를 통해 고속도로 연비(hwy)의 평균을 구해보자.

```{r group_by & summarise}

mpg %>% 
  group_by(model) %>% 
  summarise(hwy_mean = mean(hwy))

```

보다시피 모델별 hwy 평균이 나왔다. summarise()를 쓸 때는, 아래와 같은 요령으로 한다. 

* mpg %>% group_by(model) %>% summarise(hwy_mean = mean(hwy))
* mpg %>% group_by(model) %>% summarise(hwy_sum = sum(hwy))
* mpg %>% group_by(model) %>% summarise(hwy_mean = mean(hwy), hwy_sum = sum(hwy))

summarise 함수는 마지막 명령어처럼 여러개의 요약도 가능하다.

#### 연습문제

1. manufacturer별로 cty, hwy의 평균을 구해보시오.
2. class별로 cty, hwy의 평균과 합계를 구해보시오.

### arrange를 이용한 데이터 정렬

![이래선 안 된다](http://benbestphd.com/dplyr-tidyr-tutorial/index_files/figure-html/unnamed-chunk-21-1.png)

위의 그래프를 잠시 보자. 어딘가 너저분 하지 않나? 이유는 간단하다. 우리 눈은 내림차순 정렬이든, 오름차순 정렬이든 가지런하게 정리되어 있는 것을 좋아한다. 이런 것을 **정렬된 데이터(sorted data)**라고 한다. dplyr로 이런 저런 연산을 하면서 양념처럼 빼먹으면 안 되는 것이 바로 정렬이다. 

아까 실행했던 코드를 하나 띄워보자.

``` {r arrange}

mpg %>% 
  group_by(model) %>% 
  summarise(hwy_mean = mean(hwy), hwy_sum = sum(hwy))

mpg %>% 
  group_by(model) %>% 
  summarise(hwy_mean = mean(hwy), hwy_sum = sum(hwy)) %>% 
  arrange(hwy_mean)

mpg %>% 
  group_by(model) %>% 
  summarise(hwy_mean = mean(hwy), hwy_sum = sum(hwy)) %>% 
  arrange(desc(hwy_mean))

```

arrange 속에 정렬하고 싶은 기준 값을 넣으면 최종적으로 가지런히 데이터가 정리되어 나온다. desc를 넣으면 내림차순으로 자료가 정리된다.

### 결측치 처리

혹시 summarise()를 실행하다가 결과에 NA가 뜨고 계산이 안 될 때가 있다. 그럴 때는 데이터를 불러온 행의 처음에 filter(!is.na(변수))를 써주면 문제가 해결된다. 혹은 summarise()에 쓰는 sum()함수나 mean()함수에 "na.rm = TRUE"를 추가한다. 아래와 같이 한다.

```{r}

nycflights13::flights %>% 
  filter(!is.na(dep_delay)) %>% 
  group_by(month) %>% 
  summarise(delay_mean = mean(dep_delay))

nycflights13::flights %>% 
  group_by(month) %>% 
  summarise(delay_mean = mean(dep_delay, na.rm = TRUE))

```

#### 연습문제

1. mpg 데이터의 year에 따른 hwy, cty의 평균을 구하고, cty_mean 기준으로 내림차순 정렬하시오.
2. mpg 데이터의 class에 따른 cty, hwy의 합을 구하고, hwy_sum 기준으로 오름차순 정렬하시오.

### mutate를 통한 변수(열) 만들기

dplyr 기능 중 마지막으로 배울 mutate는 열을 만든다. 예를 들어 보자.
hwy를 cty로 나눈, 즉 hwy/cty를 시내 대비 고속도로 연비(hwy_per_cty)라고 해보자. mpg 데이터에 이러한 항목을 추가하려면 어떻게 해야 할까? (고전적인 방법이 있지만 그건 몰라도 된다.)

```{r mutate}
mpg %>% 
  mutate(hwy_per_cty = hwy / cty)
```

이게 끝이다. 우측 끝에 hwy_per_cty라는 변수가 생기고 hwy를 cty로 나눈 값이 들어가 있다. tidyR을 쓰는 이유는 다른 게 아니다. 가장 쉽기 때문이다.


## 종합 연습문제

이제 tidyR 패키지의 데이터 전처리(data preprocessing / data wrangling) 기능을 모두 배워봤다. 아래의 실전 자료 분석 문제풀이를 통해 여러분의 실력을 길러 보자.

1. 비행기 데이터 문제(nycflights13)

* "nycflights13" 패키지를 설치한다. (install.packages("nycflights13")) 
* library(nycflights13) 명령어로 패키지를 로드하고, flights 데이터를 불러온다. (data(flights))

```{r}
library(nycflights13)
data(flights)

glimpse(flights)
```

* 비행 달이 7, 8, 9월인 행만 추려내시오.
* 목적지(dest)가 "IAH" 이거나 "HOU"인 행만 추려내시오.
* 도착지연 시간(arr_delay)이 60분 이고, 출발지연 시간(dep_delay)이 0분인 행만 추려내시오.
* year, month, day 열만 추려내시오.
* dep_time부터 arr_delay열까지 한꺼번에 추려내시오.
* year, month, day 에 따른 dep_delay의 평균을 구하시오. (결측치도 처리할 것)
* 목적지(dest)에 따른 dep_delay의 평균을 구해 내림차 순으로 정리하시오.

