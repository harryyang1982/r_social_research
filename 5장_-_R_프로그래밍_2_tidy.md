안내
----

이번 시간에는 tidy문법을 배운다. tidy문법은 R을 문과생들도 배울 수 있게 기여한 Hadley Wickham과 그가 있는 회사인 RStudio에서 만든 패키지인 tidyverse 패키지를 활용한 문법이라고 볼 수 있다. 대학생들, 그리고 많은 현업의 데이터분석가들이 쓰는 패키지가 이 tidyverse 패키지이다.

![Hadley Wickham](https://pbs.twimg.com/profile_images/905186381995147264/7zKAG5sY.jpg)

준비
----

tidyverse 패키지를 설치하고, 메모리에 불러온다.

``` r
if(!require(tidyverse)) install.packages("tidyverse", repos = "cran.r-project.org")
```

    ## Loading required package: tidyverse

    ## ── Attaching packages ──────────────────────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 2.2.1     ✔ purrr   0.2.4
    ## ✔ tibble  1.4.2     ✔ dplyr   0.7.4
    ## ✔ tidyr   0.8.0     ✔ stringr 1.2.0
    ## ✔ readr   1.1.1     ✔ forcats 0.2.0

    ## ── Conflicts ─────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(tidyverse)
```

tidyverse 패키지는 dplyr, tidyr, readr, purrr, tibble, stringr, ggplot2 등의 패키지를 포함하고 있는 메타-패키지이다. **메타-패키지**란 말은 다양한 함수를 보유한 패키지들을 다시 통합하여 하나의 패키지로 묶었다는 말이다. tidyverse 패키지 모두를 능숙하게 사용할 수 있게 되면 보통 중급 R 데이터 분석가라고 한다. 쉽게 말하면 중급 R 데이터 분석가가 되면 회사의 경영관리팀, 기획팀 등에 취업할 때 상당한 메리트를 갖게 된다. 이것을 증명하기 위한 시험은 한국에서는 **데이터분석 준전문가(adsp)**가 있다.

고급 분석가는 machine learning(기계학습) 또는 고급 통계(SVM)를 잘 하거나, Functional Programming(함수형 프로그래밍) / Objective Oriented Programming(객체지향 프로그래밍)을 잘 하는 사람들을 뜻하며, 이들의 몸값은 보통 $100,000/year 정도 된다. 물론 고급 분석가가 되기 위해서는 통계학 외에도 선형대수 / 미적분학 같은 공대 수준 수학에 통달해야 한다.

여러분은 중급수준의 R 데이터 분석가가 될 수 있다. 1년 정도 교수의 수업을 듣고 [R for Data Science](http://r4ds.had.co.nz/)나, [Text Mining with R](https://www.tidytextmining.com/) 정도의 기술을 익혀 텍스트 마이닝(단어 단위 분석이나 문장 분석)과 네트워크 분석 정도를 수행할 수 있다면, 충분히 고급 인력으로 취업시장에서 자리잡을 수 있다. 물론 하기 나름이다. 굳이 고급 수학을 잘 할 필요는 없고, 필요한 자료를 R이 잘 알아들을 수 있게 하다보면 모든 과정을 잘 수행할 수 있다. 기술보다 자신이 만지는 데이터를 잘 파악하는 능력이 중요할 수 있다. 수업에 집중하면 먹고 사는 문제에 조금은 수월하게 접근할 수 있다.

dplyr : tidyR의 시작
--------------------

처음 배울 tidyverse의 패키지는 바로 dplyr이다. dplyr만 잘 소화하면 어떻게 생긴 데이터든 쉽게 필요한 내용을 추려서 요약해 확인할 수 있다. dplyr은 tidyverse 패키지에 설치되어 있으므로 특별히 다시 설치할 필요가 없다.

filter()
--------

처음 배울 dplyr 함수는 filter()이다. filter()는 각각 행(row)을 추려내는 역할을 한다. 이 분석을 위해 dplyr에 설치되어 있는 mpg 데이터를 활용해보도록 하자. mpg 데이터는 지난 시간에 배웠던 mtcars 데이터를 조금 더 확장해서 펼쳐놓은 데이터다. 데이터를 불러보자.

``` r
data(mpg)
glimpse(mpg)
```

    ## Observations: 234
    ## Variables: 11
    ## $ manufacturer <chr> "audi", "audi", "audi", "audi", "audi", "audi", "...
    ## $ model        <chr> "a4", "a4", "a4", "a4", "a4", "a4", "a4", "a4 qua...
    ## $ displ        <dbl> 1.8, 1.8, 2.0, 2.0, 2.8, 2.8, 3.1, 1.8, 1.8, 2.0,...
    ## $ year         <int> 1999, 1999, 2008, 2008, 1999, 1999, 2008, 1999, 1...
    ## $ cyl          <int> 4, 4, 4, 4, 6, 6, 6, 4, 4, 4, 4, 6, 6, 6, 6, 6, 6...
    ## $ trans        <chr> "auto(l5)", "manual(m5)", "manual(m6)", "auto(av)...
    ## $ drv          <chr> "f", "f", "f", "f", "f", "f", "f", "4", "4", "4",...
    ## $ cty          <int> 18, 21, 20, 21, 16, 18, 18, 18, 16, 20, 19, 15, 1...
    ## $ hwy          <int> 29, 29, 31, 30, 26, 26, 27, 26, 25, 28, 27, 25, 2...
    ## $ fl           <chr> "p", "p", "p", "p", "p", "p", "p", "p", "p", "p",...
    ## $ class        <chr> "compact", "compact", "compact", "compact", "comp...

``` r
head(mpg)
```

    ## # A tibble: 6 x 11
    ##   manufacturer model displ  year   cyl trans drv     cty   hwy fl    class
    ##   <chr>        <chr> <dbl> <int> <int> <chr> <chr> <int> <int> <chr> <chr>
    ## 1 audi         a4     1.80  1999     4 auto… f        18    29 p     comp…
    ## 2 audi         a4     1.80  1999     4 manu… f        21    29 p     comp…
    ## 3 audi         a4     2.00  2008     4 manu… f        20    31 p     comp…
    ## 4 audi         a4     2.00  2008     4 auto… f        21    30 p     comp…
    ## 5 audi         a4     2.80  1999     6 auto… f        16    26 p     comp…
    ## 6 audi         a4     2.80  1999     6 manu… f        18    26 p     comp…

지금까지 쓰지 않았던 glimpse(mpg)란 명령어가 들어가 있다. glimpse는 head보다는 좀 더 자세하게 데이터 내용을 보여주는 명령어이다. glimpse 명령어를 수행하면 데이터 안의 변수가 무엇이 있는지 확인해 주고, 그 속성을 보여주며, 처음 10개 정도의 값을 가로 방향으로 펼쳐서 보여준다. 또 엑셀과 같은 방식으로 데이터를 확인하는 방법도 있다. View(mpg) 명령어를 활용하는 것이다. (곧바로 수행해 보자)

mpg 데이터에는 11개 변수가 있고, 234개 관측(행)이 있다. 이 데이터를 어떻게 요리할 지 생각해 보자. manufacturer은 제작사, model는 자동차 모델명, displ은 배기량, year는 출시년도, cyl은 기통, trans는 기아변속 방식을 뜻한다. drv는 구동방식이고, cty와 hwy는 각각 시내 연비/고속도로 연비를 뜻한다. class는 차의 형태 분류를 말한다.

### 연속변수 처리(continuous variable operation)

이제 몇 가지 기준으로 자동차 데이터를 분석해 보자. 우선 filter부터 배워보자. filter는 특정한 기준을 만족하는 행을 출력하는 명령어이다. 우선 시내 연비를 기준으로 생각해 보자.

``` r
summary(mpg$cty)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    9.00   14.00   17.00   16.86   19.00   35.00

cty 변수를 보면 평균 16.86, 중위값 17을 보여준다. 여기서 중위값이 17보다 높은 차들만 분류해 보도록 하자.

``` r
filter(mpg, cty > 17)
```

    ## # A tibble: 102 x 11
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl   
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr>
    ##  1 audi         a4        1.80  1999     4 auto(l… f        18    29 p    
    ##  2 audi         a4        1.80  1999     4 manual… f        21    29 p    
    ##  3 audi         a4        2.00  2008     4 manual… f        20    31 p    
    ##  4 audi         a4        2.00  2008     4 auto(a… f        21    30 p    
    ##  5 audi         a4        2.80  1999     6 manual… f        18    26 p    
    ##  6 audi         a4        3.10  2008     6 auto(a… f        18    27 p    
    ##  7 audi         a4 quat…  1.80  1999     4 manual… 4        18    26 p    
    ##  8 audi         a4 quat…  2.00  2008     4 manual… 4        20    28 p    
    ##  9 audi         a4 quat…  2.00  2008     4 auto(s… 4        19    27 p    
    ## 10 chevrolet    malibu    2.40  1999     4 auto(l… f        19    27 r    
    ## # ... with 92 more rows, and 1 more variable: class <chr>

처음관측값의 행은 234개였는데, filter를 처리하고 나니 102개만 남았다. cty값이 17개 이상인 것만 남겼기 때문에 그보다 작은 것들이 모두 떨어져서 그렇다.

#### 연습문제

1.  hwy가 10 이상인 것들만 추리시오
2.  year가 2000년 이후인 것만 추리시오
3.  cty가 10 미만이고, year가 2000년 미만인 것들만 추리시오. (&를 활용할 것)

### 이산변수 처리

여기서 이산변수가 무엇이지를 잠시 살펴볼 필요가 있다. 앞서 나왔던 hwy나 cty 등은 연속 변수다. 온도나 연비 등은 특정한 기준을 만든 것이 아니라, 그 값을 그저 '측정' 한 것들이다. 키, 몸무게도 마찬가지다. 반면, cyl이나 displ 같은 변수는 기준에 맞춰 숫자를 할당한다. 실린더 기통은 4개이거나 6개이거나 8개일 수밖에 없다. 이런 변수들은 나중에 factor로 분류해 처리할 수도 있다. 하지만 이 부분은 나중에 다루기로 하자.

그렇다면 이산변수는 filter와 어떻게 만날 수 있을 것인가? 예를 들어 cyl이 4인 경우만 추리면 어덯게 하면 될까? 그럴 때는 %in% 를 통해서 변수의 내용을 추릴 수 있다. 아래를 살펴보자.

``` r
filter(mpg, cyl %in% 4)
```

    ## # A tibble: 81 x 11
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl   
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr>
    ##  1 audi         a4        1.80  1999     4 auto(l… f        18    29 p    
    ##  2 audi         a4        1.80  1999     4 manual… f        21    29 p    
    ##  3 audi         a4        2.00  2008     4 manual… f        20    31 p    
    ##  4 audi         a4        2.00  2008     4 auto(a… f        21    30 p    
    ##  5 audi         a4 quat…  1.80  1999     4 manual… 4        18    26 p    
    ##  6 audi         a4 quat…  1.80  1999     4 auto(l… 4        16    25 p    
    ##  7 audi         a4 quat…  2.00  2008     4 manual… 4        20    28 p    
    ##  8 audi         a4 quat…  2.00  2008     4 auto(s… 4        19    27 p    
    ##  9 chevrolet    malibu    2.40  1999     4 auto(l… f        19    27 r    
    ## 10 chevrolet    malibu    2.40  2008     4 auto(l… f        22    30 r    
    ## # ... with 71 more rows, and 1 more variable: class <chr>

물론 %in% 뒤에서 여러 개를 추려서 볼 수도 있다. cyl이 4와 6인 경우를 생각해 보자.

``` r
filter(mpg, cyl %in% c(4, 6))
```

    ## # A tibble: 160 x 11
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl   
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr>
    ##  1 audi         a4        1.80  1999     4 auto(l… f        18    29 p    
    ##  2 audi         a4        1.80  1999     4 manual… f        21    29 p    
    ##  3 audi         a4        2.00  2008     4 manual… f        20    31 p    
    ##  4 audi         a4        2.00  2008     4 auto(a… f        21    30 p    
    ##  5 audi         a4        2.80  1999     6 auto(l… f        16    26 p    
    ##  6 audi         a4        2.80  1999     6 manual… f        18    26 p    
    ##  7 audi         a4        3.10  2008     6 auto(a… f        18    27 p    
    ##  8 audi         a4 quat…  1.80  1999     4 manual… 4        18    26 p    
    ##  9 audi         a4 quat…  1.80  1999     4 auto(l… 4        16    25 p    
    ## 10 audi         a4 quat…  2.00  2008     4 manual… 4        20    28 p    
    ## # ... with 150 more rows, and 1 more variable: class <chr>

c()를 활용하여 cyl이 4와 6인 차종을 뽑아낼 수 있게 됐다.

#### 연습문제

1.  displ이 1.8인 경우만 추려내시오.
2.  displ이 2.0이고 cyl이 6, 8인 경우만 추려내시오.

### 문자열 필터

이번에는 문자열을 다뤄보자. 원리는 똑같다. 해당되는 내용을 요청하면 된다. 예를 들어보자. class가 "suv"인 차들만 필터해보자.

``` r
filter(mpg, class == "suv")
```

    ## # A tibble: 62 x 11
    ##    manufacturer model      displ  year   cyl trans drv     cty   hwy fl   
    ##    <chr>        <chr>      <dbl> <int> <int> <chr> <chr> <int> <int> <chr>
    ##  1 chevrolet    c1500 sub…  5.30  2008     8 auto… r        14    20 r    
    ##  2 chevrolet    c1500 sub…  5.30  2008     8 auto… r        11    15 e    
    ##  3 chevrolet    c1500 sub…  5.30  2008     8 auto… r        14    20 r    
    ##  4 chevrolet    c1500 sub…  5.70  1999     8 auto… r        13    17 r    
    ##  5 chevrolet    c1500 sub…  6.00  2008     8 auto… r        12    17 r    
    ##  6 chevrolet    k1500 tah…  5.30  2008     8 auto… 4        14    19 r    
    ##  7 chevrolet    k1500 tah…  5.30  2008     8 auto… 4        11    14 e    
    ##  8 chevrolet    k1500 tah…  5.70  1999     8 auto… 4        11    15 r    
    ##  9 chevrolet    k1500 tah…  6.50  1999     8 auto… 4        14    17 d    
    ## 10 dodge        durango 4…  3.90  1999     6 auto… 4        13    17 r    
    ## # ... with 52 more rows, and 1 more variable: class <chr>

여기서는 "=="를 활용했다. 숫자가 아니기 때문에 "&gt;"나 "&lt;"는 활용할 수 없다. 하지만 "&"나 "|"는 가능하다. 이번에는 숫자와 문자 모두를 사용해서 필터해 보자. manufacturer가 "hyundai"이고, hwy가 25미만인 차들만 찾아보자.

``` r
filter(mpg, manufacturer == "hyundai" & hwy < 25)
```

    ## # A tibble: 3 x 11
    ##   manufacturer model displ  year   cyl trans drv     cty   hwy fl    class
    ##   <chr>        <chr> <dbl> <int> <int> <chr> <chr> <int> <int> <chr> <chr>
    ## 1 hyundai      tibu…  2.70  2008     6 auto… f        17    24 r     subc…
    ## 2 hyundai      tibu…  2.70  2008     6 manu… f        16    24 r     subc…
    ## 3 hyundai      tibu…  2.70  2008     6 manu… f        17    24 r     subc…

몇 가지 연산을 더 해겠다. 따라해 보자.

``` r
filter(mpg, year > 2000 & class %in% c("subcompact", "suv")) #2000년 이후, subcompact이거나 suv인 차
```

    ## # A tibble: 49 x 11
    ##    manufacturer model      displ  year   cyl trans drv     cty   hwy fl   
    ##    <chr>        <chr>      <dbl> <int> <int> <chr> <chr> <int> <int> <chr>
    ##  1 chevrolet    c1500 sub…  5.30  2008     8 auto… r        14    20 r    
    ##  2 chevrolet    c1500 sub…  5.30  2008     8 auto… r        11    15 e    
    ##  3 chevrolet    c1500 sub…  5.30  2008     8 auto… r        14    20 r    
    ##  4 chevrolet    c1500 sub…  6.00  2008     8 auto… r        12    17 r    
    ##  5 chevrolet    k1500 tah…  5.30  2008     8 auto… 4        14    19 r    
    ##  6 chevrolet    k1500 tah…  5.30  2008     8 auto… 4        11    14 e    
    ##  7 dodge        durango 4…  4.70  2008     8 auto… 4        13    17 r    
    ##  8 dodge        durango 4…  4.70  2008     8 auto… 4         9    12 e    
    ##  9 dodge        durango 4…  4.70  2008     8 auto… 4        13    17 r    
    ## 10 dodge        durango 4…  5.70  2008     8 auto… 4        13    18 r    
    ## # ... with 39 more rows, and 1 more variable: class <chr>

``` r
filter(mpg, drv %in% "r" | class %in% "suv")
```

    ## # A tibble: 76 x 11
    ##    manufacturer model     displ  year   cyl trans  drv     cty   hwy fl   
    ##    <chr>        <chr>     <dbl> <int> <int> <chr>  <chr> <int> <int> <chr>
    ##  1 chevrolet    c1500 su…  5.30  2008     8 auto(… r        14    20 r    
    ##  2 chevrolet    c1500 su…  5.30  2008     8 auto(… r        11    15 e    
    ##  3 chevrolet    c1500 su…  5.30  2008     8 auto(… r        14    20 r    
    ##  4 chevrolet    c1500 su…  5.70  1999     8 auto(… r        13    17 r    
    ##  5 chevrolet    c1500 su…  6.00  2008     8 auto(… r        12    17 r    
    ##  6 chevrolet    corvette   5.70  1999     8 manua… r        16    26 p    
    ##  7 chevrolet    corvette   5.70  1999     8 auto(… r        15    23 p    
    ##  8 chevrolet    corvette   6.20  2008     8 manua… r        16    26 p    
    ##  9 chevrolet    corvette   6.20  2008     8 auto(… r        15    25 p    
    ## 10 chevrolet    corvette   7.00  2008     8 manua… r        15    24 p    
    ## # ... with 66 more rows, and 1 more variable: class <chr>

### magrittr, 읽기 쉬운 코드의 시작이자 dplyr의 완성형

지금까지 dplyr을 배우면서 filter(DF, 기준) 방식으로 코드를 입력했을 것이다. 하지만 조금 더 간결하게 해보자. 이걸 magrittr 방식이라고 하며, pipe라고 부른다. pipe를 부르는 방법은 Ctrl + Shift + M 키보드를 누르는 것이다. 아래의 코드를 보자.

``` r
mpg %>% 
  filter(year > 2000 & class %in% c("subcompact"))
```

    ## # A tibble: 16 x 11
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl   
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr>
    ##  1 ford         mustang   4.00  2008     6 manual… r        17    26 r    
    ##  2 ford         mustang   4.00  2008     6 auto(l… r        16    24 r    
    ##  3 ford         mustang   4.60  2008     8 manual… r        15    23 r    
    ##  4 ford         mustang   4.60  2008     8 auto(l… r        15    22 r    
    ##  5 ford         mustang   5.40  2008     8 manual… r        14    20 p    
    ##  6 honda        civic     1.80  2008     4 manual… f        26    34 r    
    ##  7 honda        civic     1.80  2008     4 auto(l… f        25    36 r    
    ##  8 honda        civic     1.80  2008     4 auto(l… f        24    36 c    
    ##  9 honda        civic     2.00  2008     4 manual… f        21    29 p    
    ## 10 hyundai      tiburon   2.00  2008     4 manual… f        20    28 r    
    ## 11 hyundai      tiburon   2.00  2008     4 auto(l… f        20    27 r    
    ## 12 hyundai      tiburon   2.70  2008     6 auto(l… f        17    24 r    
    ## 13 hyundai      tiburon   2.70  2008     6 manual… f        16    24 r    
    ## 14 hyundai      tiburon   2.70  2008     6 manual… f        17    24 r    
    ## 15 volkswagen   new bee…  2.50  2008     5 manual… f        20    28 r    
    ## 16 volkswagen   new bee…  2.50  2008     5 auto(s… f        20    29 r    
    ## # ... with 1 more variable: class <chr>

위의 첫번째 코드와 똑같은 결과가 나온다. 달라진 것은? 코드가 생각하는 논리대로 작성된다는 것이다. 예를 들면 이런 것이다.

-   baseR 방식 : 동사(목적어, 주변수, 나머지 변수)
-   tidyR 방식 : 목적어 %&gt;% 동사(주변수, 나머지 변수)

두 방식의 차이가 무엇일까? 실제로 데이터를 분석하는 입장에서 생각해 보자. (3분간 주변 친구와 토론을 해본다.)

### select()

이번에는 select()에 대해 배워보자. filter가 행을 추려냈다면, select는 열을 추려낸다. 즉 보고 싶은 변수를 추려낸다. mpg 데이터를 가지고 살펴보자.

``` r
mpg %>% 
  glimpse #변수 확인하기
```

    ## Observations: 234
    ## Variables: 11
    ## $ manufacturer <chr> "audi", "audi", "audi", "audi", "audi", "audi", "...
    ## $ model        <chr> "a4", "a4", "a4", "a4", "a4", "a4", "a4", "a4 qua...
    ## $ displ        <dbl> 1.8, 1.8, 2.0, 2.0, 2.8, 2.8, 3.1, 1.8, 1.8, 2.0,...
    ## $ year         <int> 1999, 1999, 2008, 2008, 1999, 1999, 2008, 1999, 1...
    ## $ cyl          <int> 4, 4, 4, 4, 6, 6, 6, 4, 4, 4, 4, 6, 6, 6, 6, 6, 6...
    ## $ trans        <chr> "auto(l5)", "manual(m5)", "manual(m6)", "auto(av)...
    ## $ drv          <chr> "f", "f", "f", "f", "f", "f", "f", "4", "4", "4",...
    ## $ cty          <int> 18, 21, 20, 21, 16, 18, 18, 18, 16, 20, 19, 15, 1...
    ## $ hwy          <int> 29, 29, 31, 30, 26, 26, 27, 26, 25, 28, 27, 25, 2...
    ## $ fl           <chr> "p", "p", "p", "p", "p", "p", "p", "p", "p", "p",...
    ## $ class        <chr> "compact", "compact", "compact", "compact", "comp...

``` r
mpg %>% 
  select(model, year, class)
```

    ## # A tibble: 234 x 3
    ##    model       year class  
    ##    <chr>      <int> <chr>  
    ##  1 a4          1999 compact
    ##  2 a4          1999 compact
    ##  3 a4          2008 compact
    ##  4 a4          2008 compact
    ##  5 a4          1999 compact
    ##  6 a4          1999 compact
    ##  7 a4          2008 compact
    ##  8 a4 quattro  1999 compact
    ##  9 a4 quattro  1999 compact
    ## 10 a4 quattro  2008 compact
    ## # ... with 224 more rows

select() 명령을 통해 model, year, class 변수를 입력했다. 결과는 행은 그대로 있고, model, year, class 3가지 열만 등장했다.

그런데 보고 싶은 열이 8개이면 어떻게 하는 게 좋을까? 일일이 노가다 하는 게 적성에 맞지 않을 것이다. 전체 열이 11개인 것을 감안하면, 방법은 3가지이다.

1.  보기 싫은 열을 "-"로 제외 - 예: mpg %&gt;% select(-hwy, -fl, -class)
2.  보고 싶은 열을 ":"로 묶기 - 예 : mpg %&gt;% select(manufacturer:cty)
3.  보기 싫은 열을 "-:"로 묶어서 제외 - 예: mpg %&gt;% select(-hwy:-class)

두 가지 방법 다 실험을 해 보자.

``` r
mpg %>% select(-hwy, -fl, -class)
```

    ## # A tibble: 234 x 8
    ##    manufacturer model      displ  year   cyl trans      drv     cty
    ##    <chr>        <chr>      <dbl> <int> <int> <chr>      <chr> <int>
    ##  1 audi         a4          1.80  1999     4 auto(l5)   f        18
    ##  2 audi         a4          1.80  1999     4 manual(m5) f        21
    ##  3 audi         a4          2.00  2008     4 manual(m6) f        20
    ##  4 audi         a4          2.00  2008     4 auto(av)   f        21
    ##  5 audi         a4          2.80  1999     6 auto(l5)   f        16
    ##  6 audi         a4          2.80  1999     6 manual(m5) f        18
    ##  7 audi         a4          3.10  2008     6 auto(av)   f        18
    ##  8 audi         a4 quattro  1.80  1999     4 manual(m5) 4        18
    ##  9 audi         a4 quattro  1.80  1999     4 auto(l5)   4        16
    ## 10 audi         a4 quattro  2.00  2008     4 manual(m6) 4        20
    ## # ... with 224 more rows

``` r
mpg %>% select(manufacturer:cty)
```

    ## # A tibble: 234 x 8
    ##    manufacturer model      displ  year   cyl trans      drv     cty
    ##    <chr>        <chr>      <dbl> <int> <int> <chr>      <chr> <int>
    ##  1 audi         a4          1.80  1999     4 auto(l5)   f        18
    ##  2 audi         a4          1.80  1999     4 manual(m5) f        21
    ##  3 audi         a4          2.00  2008     4 manual(m6) f        20
    ##  4 audi         a4          2.00  2008     4 auto(av)   f        21
    ##  5 audi         a4          2.80  1999     6 auto(l5)   f        16
    ##  6 audi         a4          2.80  1999     6 manual(m5) f        18
    ##  7 audi         a4          3.10  2008     6 auto(av)   f        18
    ##  8 audi         a4 quattro  1.80  1999     4 manual(m5) 4        18
    ##  9 audi         a4 quattro  1.80  1999     4 auto(l5)   4        16
    ## 10 audi         a4 quattro  2.00  2008     4 manual(m6) 4        20
    ## # ... with 224 more rows

``` r
mpg %>% select(-hwy:-class)
```

    ## # A tibble: 234 x 8
    ##    manufacturer model      displ  year   cyl trans      drv     cty
    ##    <chr>        <chr>      <dbl> <int> <int> <chr>      <chr> <int>
    ##  1 audi         a4          1.80  1999     4 auto(l5)   f        18
    ##  2 audi         a4          1.80  1999     4 manual(m5) f        21
    ##  3 audi         a4          2.00  2008     4 manual(m6) f        20
    ##  4 audi         a4          2.00  2008     4 auto(av)   f        21
    ##  5 audi         a4          2.80  1999     6 auto(l5)   f        16
    ##  6 audi         a4          2.80  1999     6 manual(m5) f        18
    ##  7 audi         a4          3.10  2008     6 auto(av)   f        18
    ##  8 audi         a4 quattro  1.80  1999     4 manual(m5) 4        18
    ##  9 audi         a4 quattro  1.80  1999     4 auto(l5)   4        16
    ## 10 audi         a4 quattro  2.00  2008     4 manual(m6) 4        20
    ## # ... with 224 more rows

어느 편이 가장 효율적일지는 그 때 그 때 다르다. 필요한 부분을 잘 추려내는 것은 분명한 능력이다.

마지막으로, 여러가지 방법을 다 섞어서 select를 해보자.

``` r
mpg %>% select(model, year, class, -hwy, -fl)
```

    ## # A tibble: 234 x 3
    ##    model       year class  
    ##    <chr>      <int> <chr>  
    ##  1 a4          1999 compact
    ##  2 a4          1999 compact
    ##  3 a4          2008 compact
    ##  4 a4          2008 compact
    ##  5 a4          1999 compact
    ##  6 a4          1999 compact
    ##  7 a4          2008 compact
    ##  8 a4 quattro  1999 compact
    ##  9 a4 quattro  1999 compact
    ## 10 a4 quattro  2008 compact
    ## # ... with 224 more rows

``` r
mpg %>% select(year, cty:class, -hwy)
```

    ## # A tibble: 234 x 4
    ##     year   cty fl    class  
    ##    <int> <int> <chr> <chr>  
    ##  1  1999    18 p     compact
    ##  2  1999    21 p     compact
    ##  3  2008    20 p     compact
    ##  4  2008    21 p     compact
    ##  5  1999    16 p     compact
    ##  6  1999    18 p     compact
    ##  7  2008    18 p     compact
    ##  8  1999    18 p     compact
    ##  9  1999    16 p     compact
    ## 10  2008    20 p     compact
    ## # ... with 224 more rows

### filter()와 select()의 혼합

이제 좀 더 수를 좁혀보자. filter()와 select()를 함께 사용해보자. 필요한 행과 필요한 열을 추려낼 수 있는 것이다. 이럴 때 어떻게 하면 될까? pipe( %&gt;% )를 두 번 쓰면 된다.

``` r
mpg %>% 
  filter(cty > 20) %>% 
  select(model, year, cty:class)
```

    ## # A tibble: 45 x 6
    ##    model   year   cty   hwy fl    class     
    ##    <chr>  <int> <int> <int> <chr> <chr>     
    ##  1 a4      1999    21    29 p     compact   
    ##  2 a4      2008    21    30 p     compact   
    ##  3 malibu  2008    22    30 r     midsize   
    ##  4 civic   1999    28    33 r     subcompact
    ##  5 civic   1999    24    32 r     subcompact
    ##  6 civic   1999    25    32 r     subcompact
    ##  7 civic   1999    23    29 p     subcompact
    ##  8 civic   1999    24    32 r     subcompact
    ##  9 civic   2008    26    34 r     subcompact
    ## 10 civic   2008    25    36 r     subcompact
    ## # ... with 35 more rows

model, year, cty부터 class까지의 변수가 선택되고, filter 명령어를 통해 시내연비가 20보다 큰 차종들만 선택이 됐다. 이러한 방식으로 자신이 보고 싶은 자료를 찾아보는 것을 **데이터 전처리**라고 한다. filter()와 select()는 가장 기초적인 전처리 방식이라고 볼 수 있다.

이제 본격적으로 전처리를 수행해 보자.

group\_by()와 summarise()
-------------------------

이런 경우를 생각해 보자. 차종에 따른 연비는 어떻게 다를까? 차종을 filter하고 연비를 filter하는 것이 아니다. 차종에 따른 연비들의 평균이나 합계가 나와줘야 하는 것이다. 엑셀을 쓰다보면 '피벗 테이블(pivot table)'을 쓰는 경우가 있는데, 이 경우가 바로 그렇다. dplyr 패키지는 group\_by()와 summarise()라는 명령어를 통해 이 문제를 해결하게 도와준다.

예를 들어보자. 위에서 언급한 차종에 따른 고속도로 연비 평균을 구해보자. 우선 실행해야 하는 것은 group\_by()이다. group\_by(기준 변수)를 실행한 후 결과를 보자.

``` r
mpg %>% 
  group_by(model)
```

    ## # A tibble: 234 x 11
    ## # Groups:   model [38]
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl   
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr>
    ##  1 audi         a4        1.80  1999     4 auto(l… f        18    29 p    
    ##  2 audi         a4        1.80  1999     4 manual… f        21    29 p    
    ##  3 audi         a4        2.00  2008     4 manual… f        20    31 p    
    ##  4 audi         a4        2.00  2008     4 auto(a… f        21    30 p    
    ##  5 audi         a4        2.80  1999     6 auto(l… f        16    26 p    
    ##  6 audi         a4        2.80  1999     6 manual… f        18    26 p    
    ##  7 audi         a4        3.10  2008     6 auto(a… f        18    27 p    
    ##  8 audi         a4 quat…  1.80  1999     4 manual… 4        18    26 p    
    ##  9 audi         a4 quat…  1.80  1999     4 auto(l… 4        16    25 p    
    ## 10 audi         a4 quat…  2.00  2008     4 manual… 4        20    28 p    
    ## # ... with 224 more rows, and 1 more variable: class <chr>

결과를 보면 "Groups: model \[38\]"이라는 한 줄이 추가되었을 뿐, 특별한 변화가 없다. 하지만 이건 기준을 잡았으니, 다음 연산을 하라는 이야기다. 이제 summarise()를 통해 고속도로 연비(hwy)의 평균을 구해보자.

``` r
mpg %>% 
  group_by(model) %>% 
  summarise(hwy_mean = mean(hwy))
```

    ## # A tibble: 38 x 2
    ##    model              hwy_mean
    ##    <chr>                 <dbl>
    ##  1 4runner 4wd            18.8
    ##  2 a4                     28.3
    ##  3 a4 quattro             25.8
    ##  4 a6 quattro             24.0
    ##  5 altima                 28.7
    ##  6 c1500 suburban 2wd     17.8
    ##  7 camry                  28.3
    ##  8 camry solara           28.1
    ##  9 caravan 2wd            22.4
    ## 10 civic                  32.6
    ## # ... with 28 more rows

보다시피 모델별 hwy 평균이 나왔다. summarise()를 쓸 때는, 아래와 같은 요령으로 한다.

-   mpg %&gt;% group\_by(model) %&gt;% summarise(hwy\_mean = mean(hwy))
-   mpg %&gt;% group\_by(model) %&gt;% summarise(hwy\_sum = sum(hwy))
-   mpg %&gt;% group\_by(model) %&gt;% summarise(hwy\_mean = mean(hwy), hwy\_sum = sum(hwy))

summarise 함수는 마지막 명령어처럼 여러개의 요약도 가능하다.

#### 연습문제

1.  manufacturer별로 cty, hwy의 평균을 구해보시오.
2.  class별로 cty, hwy의 평균과 합계를 구해보시오.

### arrange를 이용한 데이터 정렬

![이래선 안 된다](http://benbestphd.com/dplyr-tidyr-tutorial/index_files/figure-html/unnamed-chunk-21-1.png)

위의 그래프를 잠시 보자. 어딘가 너저분 하지 않나? 이유는 간단하다. 우리 눈은 내림차순 정렬이든, 오름차순 정렬이든 가지런하게 정리되어 있는 것을 좋아한다. 이런 것을 **정렬된 데이터(sorted data)**라고 한다. dplyr로 이런 저런 연산을 하면서 양념처럼 빼먹으면 안 되는 것이 바로 정렬이다.

아까 실행했던 코드를 하나 띄워보자.

``` r
mpg %>% 
  group_by(model) %>% 
  summarise(hwy_mean = mean(hwy), hwy_sum = sum(hwy))
```

    ## # A tibble: 38 x 3
    ##    model              hwy_mean hwy_sum
    ##    <chr>                 <dbl>   <int>
    ##  1 4runner 4wd            18.8     113
    ##  2 a4                     28.3     198
    ##  3 a4 quattro             25.8     206
    ##  4 a6 quattro             24.0      72
    ##  5 altima                 28.7     172
    ##  6 c1500 suburban 2wd     17.8      89
    ##  7 camry                  28.3     198
    ##  8 camry solara           28.1     197
    ##  9 caravan 2wd            22.4     246
    ## 10 civic                  32.6     293
    ## # ... with 28 more rows

``` r
mpg %>% 
  group_by(model) %>% 
  summarise(hwy_mean = mean(hwy), hwy_sum = sum(hwy)) %>% 
  arrange(hwy_mean)
```

    ## # A tibble: 38 x 3
    ##    model                  hwy_mean hwy_sum
    ##    <chr>                     <dbl>   <int>
    ##  1 ram 1500 pickup 4wd        15.3     153
    ##  2 durango 4wd                16.0     112
    ##  3 k1500 tahoe 4wd            16.2      65
    ##  4 f150 pickup 4wd            16.4     115
    ##  5 land cruiser wagon 4wd     16.5      33
    ##  6 range rover                16.5      66
    ##  7 dakota pickup 4wd          17.0     153
    ##  8 navigator 2wd              17.0      51
    ##  9 expedition 2wd             17.3      52
    ## 10 grand cherokee 4wd         17.6     141
    ## # ... with 28 more rows

``` r
mpg %>% 
  group_by(model) %>% 
  summarise(hwy_mean = mean(hwy), hwy_sum = sum(hwy)) %>% 
  arrange(desc(hwy_mean))
```

    ## # A tibble: 38 x 3
    ##    model        hwy_mean hwy_sum
    ##    <chr>           <dbl>   <int>
    ##  1 corolla          34.0     170
    ##  2 new beetle       32.8     197
    ##  3 civic            32.6     293
    ##  4 jetta            29.1     262
    ##  5 altima           28.7     172
    ##  6 a4               28.3     198
    ##  7 camry            28.3     198
    ##  8 camry solara     28.1     197
    ##  9 sonata           27.7     194
    ## 10 malibu           27.6     138
    ## # ... with 28 more rows

arrange 속에 정렬하고 싶은 기준 값을 넣으면 최종적으로 가지런히 데이터가 정리되어 나온다. desc를 넣으면 내림차순으로 자료가 정리된다.

### 결측치 처리

혹시 summarise()를 실행하다가 결과에 NA가 뜨고 계산이 안 될 때가 있다. 그럴 때는 데이터를 불러온 행의 처음에 filter(!is.na(변수))를 써주면 문제가 해결된다. 혹은 summarise()에 쓰는 sum()함수나 mean()함수에 "na.rm = TRUE"를 추가한다. 아래와 같이 한다.

``` r
nycflights13::flights %>% 
  filter(!is.na(dep_delay)) %>% 
  group_by(month) %>% 
  summarise(delay_mean = mean(dep_delay))
```

    ## # A tibble: 12 x 2
    ##    month delay_mean
    ##    <int>      <dbl>
    ##  1     1      10.0 
    ##  2     2      10.8 
    ##  3     3      13.2 
    ##  4     4      13.9 
    ##  5     5      13.0 
    ##  6     6      20.8 
    ##  7     7      21.7 
    ##  8     8      12.6 
    ##  9     9       6.72
    ## 10    10       6.24
    ## 11    11       5.44
    ## 12    12      16.6

``` r
nycflights13::flights %>% 
  group_by(month) %>% 
  summarise(delay_mean = mean(dep_delay, na.rm = TRUE))
```

    ## # A tibble: 12 x 2
    ##    month delay_mean
    ##    <int>      <dbl>
    ##  1     1      10.0 
    ##  2     2      10.8 
    ##  3     3      13.2 
    ##  4     4      13.9 
    ##  5     5      13.0 
    ##  6     6      20.8 
    ##  7     7      21.7 
    ##  8     8      12.6 
    ##  9     9       6.72
    ## 10    10       6.24
    ## 11    11       5.44
    ## 12    12      16.6

#### 연습문제

1.  mpg 데이터의 year에 따른 hwy, cty의 평균을 구하고, cty\_mean 기준으로 내림차순 정렬하시오.
2.  mpg 데이터의 class에 따른 cty, hwy의 합을 구하고, hwy\_sum 기준으로 오름차순 정렬하시오.

### mutate를 통한 변수(열) 만들기

dplyr 기능 중 마지막으로 배울 mutate는 열을 만든다. 예를 들어 보자. hwy를 cty로 나눈, 즉 hwy/cty를 시내 대비 고속도로 연비(hwy\_per\_cty)라고 해보자. mpg 데이터에 이러한 항목을 추가하려면 어떻게 해야 할까? (고전적인 방법이 있지만 그건 몰라도 된다.)

``` r
mpg %>% 
  mutate(hwy_per_cty = hwy / cty)
```

    ## # A tibble: 234 x 12
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl   
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr>
    ##  1 audi         a4        1.80  1999     4 auto(l… f        18    29 p    
    ##  2 audi         a4        1.80  1999     4 manual… f        21    29 p    
    ##  3 audi         a4        2.00  2008     4 manual… f        20    31 p    
    ##  4 audi         a4        2.00  2008     4 auto(a… f        21    30 p    
    ##  5 audi         a4        2.80  1999     6 auto(l… f        16    26 p    
    ##  6 audi         a4        2.80  1999     6 manual… f        18    26 p    
    ##  7 audi         a4        3.10  2008     6 auto(a… f        18    27 p    
    ##  8 audi         a4 quat…  1.80  1999     4 manual… 4        18    26 p    
    ##  9 audi         a4 quat…  1.80  1999     4 auto(l… 4        16    25 p    
    ## 10 audi         a4 quat…  2.00  2008     4 manual… 4        20    28 p    
    ## # ... with 224 more rows, and 2 more variables: class <chr>,
    ## #   hwy_per_cty <dbl>

이게 끝이다. 우측 끝에 hwy\_per\_cty라는 변수가 생기고 hwy를 cty로 나눈 값이 들어가 있다. tidyR을 쓰는 이유는 다른 게 아니다. 가장 쉽기 때문이다.

종합 연습문제
-------------

이제 tidyR 패키지의 데이터 전처리(data preprocessing / data wrangling) 기능을 모두 배워봤다. 아래의 실전 자료 분석 문제풀이를 통해 여러분의 실력을 길러 보자.

1.  비행기 데이터 문제(nycflights13)

-   "nycflights13" 패키지를 설치한다. (install.packages("nycflights13"))
-   library(nycflights13) 명령어로 패키지를 로드하고, flights 데이터를 불러온다. (data(flights))

``` r
library(nycflights13)
data(flights)

glimpse(flights)
```

    ## Observations: 336,776
    ## Variables: 19
    ## $ year           <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013,...
    ## $ month          <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
    ## $ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
    ## $ dep_time       <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 55...
    ## $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 60...
    ## $ dep_delay      <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2...
    ## $ arr_time       <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 7...
    ## $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 7...
    ## $ arr_delay      <dbl> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -...
    ## $ carrier        <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV",...
    ## $ flight         <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79...
    ## $ tailnum        <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN...
    ## $ origin         <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR"...
    ## $ dest           <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL"...
    ## $ air_time       <dbl> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138...
    ## $ distance       <dbl> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 94...
    ## $ hour           <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5,...
    ## $ minute         <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, ...
    ## $ time_hour      <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013...

-   비행 달이 7, 8, 9월인 행만 추려내시오.
-   목적지(dest)가 "IAH" 이거나 "HOU"인 행만 추려내시오.
-   도착지연 시간(arr\_delay)이 60분 이고, 출발지연 시간(dep\_delay)이 0분인 행만 추려내시오.
-   year, month, day 열만 추려내시오.
-   dep\_time부터 arr\_delay열까지 한꺼번에 추려내시오.
-   year, month, day 에 따른 dep\_delay의 평균을 구하시오. (결측치도 처리할 것)
-   목적지(dest)에 따른 dep\_delay의 평균을 구해 내림차 순으로 정리하시오.
