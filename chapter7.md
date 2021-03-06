안내
----

마지막에서는 R을 활용한 추론통계를 수행한다. 기초통계가 평균과 관련된 분포를 확인하는 것이었다면(평균, 중위값, 최대값, 최소값, 분위계수, 표준편차, 분산 등), 추론통계는 가설을 검증하는 작업이라고 볼 수 있다.

최신 통계의 트렌드는 크게 보아 1) 예측 분석(predictive analysis, Machine Learning을 통해 수행)과 2) 다변량 회귀분석의 확장, 3) 베이지언 통계라고 볼 수 있다. 예측 분석이 컴퓨터 과학자들이 주로 개척하는 영역이라면, 회귀분석과 베이지언 통계는 통계학자를 포함한 사회과학자들이 끊임없이 탐구하는 영역이라고 볼 수 있다.

이번 장에서는 주눅들지 않는 수준에서 수행할 수 있는 통계 검정 기법을 배우도록 하겠다. 모두다 수학을 싫어하고 필자 역시 싫어하기 때문에 간단한 수준만 수행하도록 한다.

준비
----

특별한 준비가 필요하지 않다. R이야말로 애초부터 통계분석을 하기 위해 만든 프로그래밍 언어이기 때문이다.

### One-sampe t-test

One-sample t-test는 모집단의 평균이 정해져 있을 때, 표본의 평균이 모집단의 평균과 신뢰구간(95%)에서 같은지(H0:귀무가설), 다른지(H1:대립가설)를 검정하는 테스트다.

``` r
x <- c(15.5, 11.21, 12.67, 8.87, 12.15, 9.88, 2.06, 14.50, 0, 4.97)
mean(x)
```

    ## [1] 9.181

``` r
sd(x)
```

    ## [1] 5.234965

``` r
shapiro.test(x)
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  x
    ## W = 0.92341, p-value = 0.3863

``` r
t.test(x, mu=8.1)
```

    ## 
    ##  One Sample t-test
    ## 
    ## data:  x
    ## t = 0.653, df = 9, p-value = 0.5301
    ## alternative hypothesis: true mean is not equal to 8.1
    ## 95 percent confidence interval:
    ##   5.436132 12.925868
    ## sample estimates:
    ## mean of x 
    ##     9.181

t-test 결과를 보면 p-value는 0.53으로 귀무가설이 기각되지 않는다. 즉 모집단과 표본은 통계적으로 유의미한 평균의 차이를 갖지 않는다는 의미다. 여기에서 단측검정을 실시해볼 수도 있다. 기존의 양측검정은 '차이'를 검증하는 것이었다면, 단측검정은 '방향 + 차이'를 검증하는 셈이다. 즉, "더 큰지", "더 작은지"를 검증하는 것이다.

``` r
t.test(x, mu=8.1, conf.level = 0.99, alter="greater")
```

    ## Warning in t.test.default(x, mu = 8.1, conf.level = 0.99, alter =
    ## "greater"): partial argument match of 'alter' to 'alternative'

    ## 
    ##  One Sample t-test
    ## 
    ## data:  x
    ## t = 0.653, df = 9, p-value = 0.265
    ## alternative hypothesis: true mean is greater than 8.1
    ## 99 percent confidence interval:
    ##  4.510276      Inf
    ## sample estimates:
    ## mean of x 
    ##     9.181

### paired t-test vs wilcoxon signed-rank test

이번에는 모집단의 평균을 모를 때, 두 집단을 비교하는 t-test다. 이를 위해 paired t-test와 wilcoxon signed-rank test를 실시해 본다.

``` r
data(sleep)
head(sleep)
```

    ##   extra group ID
    ## 1   0.7     1  1
    ## 2  -1.6     1  2
    ## 3  -0.2     1  3
    ## 4  -1.2     1  4
    ## 5  -0.1     1  5
    ## 6   3.4     1  6

``` r
str(sleep)
```

    ## 'data.frame':    20 obs. of  3 variables:
    ##  $ extra: num  0.7 -1.6 -0.2 -1.2 -0.1 3.4 3.7 0.8 0 2 ...
    ##  $ group: Factor w/ 2 levels "1","2": 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ ID   : Factor w/ 10 levels "1","2","3","4",..: 1 2 3 4 5 6 7 8 9 10 ...

``` r
with(sleep, 
     shapiro.test(extra[group == 2] - extra[group == 1]))
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  extra[group == 2] - extra[group == 1]
    ## W = 0.82987, p-value = 0.03334

``` r
with(sleep,
     wilcox.test(extra[group == 2] - extra[group == 1], exact=F))
```

    ## 
    ##  Wilcoxon signed rank test with continuity correction
    ## 
    ## data:  extra[group == 2] - extra[group == 1]
    ## V = 45, p-value = 0.009091
    ## alternative hypothesis: true location is not equal to 0

``` r
with(sleep,
     t.test(extra[group == 1],
            extra[group == 2], paired= T))
```

    ## 
    ##  Paired t-test
    ## 
    ## data:  extra[group == 1] and extra[group == 2]
    ## t = -4.0621, df = 9, p-value = 0.002833
    ## alternative hypothesis: true difference in means is not equal to 0
    ## 95 percent confidence interval:
    ##  -2.4598858 -0.7001142
    ## sample estimates:
    ## mean of the differences 
    ##                   -1.58

p-value는 두 검정 모두에서 유의미하게 나온다(p-value &lt;0.05). 따라서 두 집단에는 유의미한 통계적 차이가 있다. 본 데이터에서는 수면제가 유의미한 효과가 있었다는 이야기가 된다.

### ANOVA 테스트 : 집단별 차이가 통계적으로 의미가 있는지 검증해 보기

-   10대, 20대, 30대의 평균 소비액, 정말로 유의미한 차이인지 확인하려면?

매우 간단하면서도 유용한 분석 방법부터 살펴보자. 일원배치 분산분석(One-way ANOVA)은 독립된 세 집단 이상의 평균을 비교하고자 할 때 사용하는 분석 방법이다. 좀 더 자세히는 평균의 차이가 의미가 있는지 없는지를 알아보고자 할 때 사용한다.

예를 들어보겠다. 연령대 별로 월 평균 게임에 사용하는 금액을 조사했더니, 10대는 18,200원, 20대는 20,500원 30대는 19,300원을 사용한다는 결과가 나왔다고 가정해 보자. 이러한 구매 금액이 정말로 유의미한 차이인지는 어떻게 확인할 수 있을까? 1,000원 정도씩 차이가 나는데, 이걸 차이가 있다고 보아야 하는 건지, 차이가 매우 근소하기 때문에 차이가 없다고 보아야 할 것 같기도 하고…

이럴 때 일원배치 분산분석을 사용하면 이러한 집단 간 평균 차이가 통계적으로 의미가 있는 숫자인지 아닌지를 판단할 수 있다.

일원배치 분산분석은 회사에서도 자주 사용하는 편이다. 특히 플레이어 분석을 할때 연령대 별, 게임 이용 기간 대 별 등등 그룹으로 구분해서 보아야 할 때는 거의 필수적으로 사용하기 때문에 알아두면 쓸모가 많은 분석 방법이다. 게다가 매우 간단하다. 예제로 한번 확인해 보겠다.

#### 일원배치 분산분석의 예

R에 내장되어 있는 iris 데이터로 일원배치 분산분석을 해보자. 일원배치 분산 분석을 할 때는 aov 함수와 bartlett.test 함수 두가지를 사용한다.

먼저 aov으로 일원배치 분산분석(ANOVA)을 해 보겠다. 기본 적인 문법은 aov(대상변수~그룹변수, data=데이터명)의 순서로 하면 된다. 이때 주의해야 할 점은 그룹 변수는 범주형(factor)이어야 한다는 것이다. (가지고 있는 데이터 셋으로 분석하실 때는 as.factor함수를 사용해서 변수 유형을 변경해야 한다.)

``` r
analysis<-aov(Sepal.Width~Species, data=iris)
summary(analysis)
```

    ##              Df Sum Sq Mean Sq F value Pr(>F)    
    ## Species       2  11.35   5.672   49.16 <2e-16 ***
    ## Residuals   147  16.96   0.115                   
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

일원배치 분산분석 결과 P-value 값이 매우 작게 나와 귀무가설이 기각됐다. (\*\*\*표시) 이 결과만 보면” iris의 품종(Species) 별로 Sepal.Width 평균은 다르다”라고 판단할 수가 있는 것이다. 단, 일원배치 분산분석이 성립하기 위한 전제 조건이 있다. 바로 오차의 등분산성 검정이다. bartlett.test함수를 사용하면 간단히 확인할 수 있다.

``` r
bartlett.test(Sepal.Width~Species, data=iris)
```

    ## 
    ##  Bartlett test of homogeneity of variances
    ## 
    ## data:  Sepal.Width by Species
    ## Bartlett's K-squared = 2.0911, df = 2, p-value = 0.3515

p-value가 0.05보다 크므로 귀무가설을 기각할 수가 없다. 오차의 등분산성 가정을 만족한다고 판단할 수가 있다.
