---
title: "1장 - 수업 안내"
author: "양승훈"
date: '2018/2/5'
---

## 수업개요

사회학과에서 개설한 데이터분석 수업(1학기 데이터분석기법과실습, 2학기 최신사회분석기법과실습)은 사회에서 만들어지는 데이터를 읽고(read), 전처리하여(preprocessing), 시각화 시키고(visualizing), 분석하는(analyzing) 방법을 배운다. 

1학기에는 R을 활용한 통계분석에 초점을 맞추고, 2학기에는 다양한 최신의 분석기법(textmining, 사회관계망 분석, 시계열 분석 등)을 배운다. 

본 수업을 위해 R을 배운다. 이 교재 또한, R의 패키지인 knitR을 활용하여 RMarkdown을 통해 작성한 것이다.

## 수업진행 방식

이 수업은 이론적으로는 50% 이론, 50% 실습으로 진행한다. 단, 실질적으로는 100% 실습으로 느껴질 것이다. 

* 이론: 교수가 개념을 설명하고 라이브 코딩을 통해서 내용을 전달하면, 학생들은 이를 따라서 코딩하면서 실행여부를 확인한다.
* 실습: 교수가 예제문제를 제시하면 이를 2~3명 조를 통해서 풀이한다.

## 수업평가

* 중간/기말고사 : 각 15점(총 30점)
* 퀴즈(총 5회) : 각 5점 (총 25점)
* 개인 과제 : 25점
* 보너스 점수 : 10점
* 출석 : 10점

### A를 받기 위한 방법
![A 받기](https://thumbs.dreamstime.com/z/how-to-get-plus-grade-score-school-paper-report-test-exam-other-written-assignment-43473319.jpg)

1. 수업에 빠지지 않는다.
* 결석 점수는 크게 의미 없지만, 수업에서 빠진 것을 수습하려면 시간이 2배로 걸린다.
* 수업에 빠진 경우 교재를 보고 풀어보고, 안 되는 내용을 교수에게 메일로 물어보거나 상담을 신청한다.

2. 수업에 늦지 않는다.
* 지각 점수도 크게 의미 없지만, 늦으면 그 만큼 타이핑 해야 하는 양이 늘어난다.
* 수업에 지각한 경우, 수업 반장에게 물어보고, 그래도 안 되면 교수에게 메일로 물어보거나 상담을 신청한다.

3. 보너스 점수를 타자
* 퀴즈나 중간고사/기말고사에는 보너스 문제가 있다. (배점과 별개)
* 그 외에도 개인 과제시 교수의 질문에 대답을 잘 하거나, 준비 과정을 성실하게 할 경우 보너스 점수를 준다.

### 통계(?), 통계(!)

사회조사방법론, 사회조사통계론 수업을 수강하면서 수강생들이 겪게되는 가장 큰 어려움은 통계학이다. 1학기에는 방법론 수업에서 배웠던 내용들을 R프로그래밍을 통해 좀 더 쉽게 해결하는 과정을 통해서 통계학을 단련한다.

### R을 배우는 이유

통계를 배우기 위해 가장 쉬운 도구는 엑셀이다. 그러나 수업에서는 엑셀을 R에서 진행한 작업을 확인하는 수준으로 최소한만 배운다. 그 이유는 엑셀의 주요함수가 R에 모두 구현되어 있고, R이 엑셀과 병행하여 사용하는 워드보다도 더 효과적인 문서를 만들 수 있기 때문이다. (이 교재도 RMarkdown을 통해서 제작했다.)

### 데이터 분석, 무엇을 하는가?

사례를 통해 데이터 분석을 어떻게 진행하고 그 결과를 어떻게 해석하는지 간략하게 살핀다. 물론 지금은 연습 시간이므로 실제로 코딩을 진행하지는 않는다.

#### 데이터 과학자가 하는 일 1 - 분류(classification)

야구를 보면 장타형, 출루형, 주루형 등의 속성을 가진 타자들이 있다. 이런 분류는 어떤 데이터를 통해서 확인할 수 있을까? 장타율, 출루율, 도루성공률 등을 통해서 확인할 수 있을 것이다. 이런 식으로 어떤 기준(분류)을 가지고 데이터를 검증하는 방식을 분류 알고리즘이라고 한다.

![데이터 과학자가 하는 일 1 - 분류](https://docs.microsoft.com/en-us/azure/machine-learning/studio/media/data-science-for-beginners-the-5-questions-data-science-answers/classification-algorithms.png)

##### 간단한 분류의 예시

아이리스라는 데이터를 활용해 보겠다. 아이리스 데이터는 통계학자인 피셔Fisher가 소개한 데이터로, 붓꽃의 3가지 종(setosa, versicolor, virginica)에 대해 꽃받침(sepal)과 꽃잎(petal)의 길이를 정리한 데이터다. 

```{r classification, echo = FALSE, message = F, warning = FALSE}
if(!require(tidyverse)) install.packages("tidyverse")
library(tidyverse)

iris %>% 
  ggplot(aes(Sepal.Length)) +
  geom_bar(aes(fill = Species))

iris %>% 
  ggplot(aes(Petal.Width)) +
  geom_bar(aes(fill = Species))

iris %>% 
  ggplot(aes(Petal.Length)) +
  geom_bar(aes(fill = Species))

iris %>% 
  group_by(Species) %>% 
  summarise(Sepal.Length = mean(Sepal.Length))

iris %>% 
  group_by(Species) %>% 
  summarise(Sepal.Length = mean(Sepal.Length)) %>% 
  ggplot(aes(x = Species, y = Sepal.Length)) +
  geom_col(aes(fill = Species))
  
```


이렇게 데이터의 내용을 평가하는 작업을 EDA(Exploratory Data Anaylsis)라고 한다. Sepal.Length, Petal.Length, Petal.Width의 분포를 살피면 분류할 수 있는 아이디어를 얻을 수 있다. 실제로 이를 검증해 보기 위해 의사결정트리(Decision Tree)를 만들어 볼 수 있다.

```{r classification decision tree, echo = F, message = F, warning = F}
library(party)

tree <- ctree(Species~., data = iris)
table(predict(tree, iris[,1:4]), iris$Species)

library(caTools)
set.seed(20180205)
indexes <- sample(1:nrow(iris), 70)
iris_train <- iris[indexes,]
iris_test <- iris[-indexes,]
m <- ctree(Species ~ ., data = iris_train)
table(predict(m, iris_test[,1:4]), iris_test$Species)
plot(m)
```

위의 코드를 통해서, 붓꽃의 종류는 Petal Length가 1.9보다 작거나 같을 경우 setosa일 확률이 높고, 그렇지 않을 경우 Petal Width가 1.7보다 작거나 같으면 versicolor, Petal Width가 1.7보다 클 경우 virginica임을 알 수 있다.

#### 데이터 과학자가 하는 일 2: 이상징후 포착


![데이터 과학자가 하는 일 2 - 이상징후 포착](https://docs.microsoft.com/en-us/azure/machine-learning/studio/media/data-science-for-beginners-the-5-questions-data-science-answers/anomaly-detection-algorithms.png)

두 사람의 사례를 들어보자. 사린이는 월 200만원을 벌어, 카드값으로 매월 100만원을 내고, 50만원을 저축하고, 나머지는 현금으로 소비한다. 어느 날 카드값이 1000만원이 나왔다. 이건 이상징후일까 아닐까? 경묵이는 월 300만원을 벌어, 보통 카드값으로 270만원을 내고, 30만원을 현금으로 쓴다. 저축은 하지 않는다. 그런데 어느 날 카드값이 100만원 나왔다. 이건 이상징후일까 아닐까?

이런 문제는 개인들에게는 금융 사기, 쉽게 말해 보이스 피싱을 당하느냐 마냐의 문제에 속한다. 사린이는 평소 100만원 카드값을 냈는데, 특별한 이유가 없이 1000만원이 나왔다면, 분명 보이스피싱을 당했거나 큰 사고가 났거나 질병에 걸렸을 것이기 때문이다. 그런데 그게 아니라 1200만원으로 소득이 올라(**그럴 리는 별로 없지만**) 기분을 냈다면, 이는 또 다른 문제가 될 것이다. 경묵이가 100만원만 카드값이 나온 것은 어떻게 해석해야 할까? 아마 좋은 일일 것이다. 재무관리를 통해서 현금 소비를 늘였을 수도 있다. 그러나 소득이 갑자기 줄어들어서 카드값을 줄였다면? 

똑같은 고민을 신용카드 회사도 할 것이다. 사린이의 결제액이 늘어났을 때 신용카드 회사는 사린이에게 돈을 더 쓰라고 쿠폰을 줘야 할까? 아니면 신용정보회사에 사린이의 금융사고 신고 내역을 조회해야 할까? 경묵이에게도 할인 쿠폰을 줘서 다시 카드를 쓰게 해야 할까, 아니면 소득이 줄어들었다는 것으로 간주해 혜택을 회수해야 할까? 

이런 결정을 하는 것들이 모두 데이터 분석의 이상징후 포착 알고리즘을 통해서 벌어지는 일이다.

```{r anomaly detection, echo = F, message = F, warning = F}

if(!require(AnomalyDetection)) devtools::install_github("twitter/AnomalyDetection")
library(AnomalyDetection)

data(raw_data)
AnomalyDetectionTs(raw_data, max_anoms=0.02, direction='both', plot=TRUE)

```

이러한 그래프를 통해 특이한 지점(9월 30일 저녁)을 포착하고, 이에 따른 진단을 할 수 있는 것이다.

#### 데이터 과학자가 하는 일 3 - 회귀 분석

![데이터 과학자가 하는 일 3 - 회귀](https://docs.microsoft.com/en-us/azure/machine-learning/studio/media/data-science-for-beginners-the-5-questions-data-science-answers/regression-algorithms.png)

매년 7월의 평균 날씨가 섭씨 24도였다고 가정하자. "7월 22일의 날씨는 몇도일까?"
TV 광고를 몇 번 하면, 갤럭시 노트는 한 대를 팔 수 있을까?

이런 질문에 대한 답변이 회귀분석을 통해 도출될 수 있다.

```{r linear regression, echo = F, message = F, warning = F}
library(tidyverse)  # data manipulation and visualization
library(modelr)     # provides easy pipeline modeling functions
library(broom)      # helps to tidy up model outputs

advertising <- read_csv("http://www-bcf.usc.edu/~gareth/ISL/Advertising.csv") %>%
  select(-X1)

set.seed(123)
sample <- sample(c(TRUE, FALSE), nrow(advertising), replace = T, prob = c(0.6,0.4))
train <- advertising[sample, ]
test <- advertising[!sample, ]

model1 <- lm(sales ~ TV, data = train)
summary(model1)
tidy(model1)

ggplot(train, aes(TV, sales)) +
  geom_point() +
  geom_smooth(method = "lm") +
  geom_smooth(se = FALSE, color = "red")
```

회귀분석을 통해 tv광고를 한 번 하면 스마트폰 0.05대를 팔 수 있다는 결과가 나온다. 즉 1대를 팔기 위해서는 TV광고가 20번 이상 노출되어야 가능하다는 것이다. 그리고 p-value를 통해서 그런 검증이 얼마나 맞는지를 확인할 수 있다. training set과 test set을 활용하면, 그 사례를 가지고 다른 사례에도 적용가능한지를 시뮬레이션 해볼 수 있다.

사회조사통계를 공부하면서 가장 어려운 것이 t-value, p-value, F statistics의 점수를 구해서 그 의미를 해석하는 것이었으리라. 하지만 R Programming을 통해서는 좀 더 직관적으로 이러한 내용의 의미를 해석할 수 있다. 아래의 그래프를 보자. 

```{r linear regression 2, echo = F, message = F, warning= F}
model1_results <- augment(model1, train)
model2 <- lm(sales ~ TV + radio + newspaper, data = train)
summary(model2)
tidy(model2)

list(model1 = broom::glance(model1), model2 = broom::glance(model2))

model1_results <- model1_results %>%
  mutate(Model = "Model 1")

model2_results <- augment(model2, train) %>%
  mutate(Model = "Model 2") %>%
  rbind(model1_results)

model1_results <- augment(model1, train)

model1_results <- model1_results %>%
  mutate(Model = "Model 1")

model2_results <- augment(model2, train) %>%
  mutate(Model = "Model 2") %>%
  rbind(model1_results)

ggplot(model2_results, aes(.fitted, .resid)) +
  geom_ref_line(h = 0) +
  geom_point() +
  geom_smooth(se = FALSE) +
  facet_wrap(~ Model) +
  ggtitle("Residuals vs Fitted")

```

TV 광고만 했을 때와, 라디오, 신문광고를 포함했을 때의 효과를 함께 비교해 볼 수도 있다. 회귀분석은 즉, 이렇게 다양한 변수를 통해서 우리가 원하는 예측을 도출할 수 있는 방법이다.

#### 데이터 과학자가 하는 일 4 - 클러스터링

![데이터 과학자가 하는 일 4 - 클러스터링](https://docs.microsoft.com/en-us/azure/machine-learning/studio/media/data-science-for-beginners-the-5-questions-data-science-answers/clustering-algorithms.png)

여러분이 이마트 매장 담당자라고 생각해보자. 면도기는 어디에 배치하면 될까? 여기에는 사회학적 상상력이 필요하다. 그러나 본인의 상상력만으로 문제를 풀 수 있는 것은 아니다. 

면도기와 기저귀, 면도기와 맥주. 이 중 어떤 것이 더 면도기 매출을 늘릴 수 있을까? 성별 분포나 동네의 특성에 대한 사회학적인 분석이 필요하다. 만약 30대 부부가 많이 사는 동네라면? 면도기는 기저귀에서 멀어지면 안 된다. 만약 20대 대학생이 많이 사는 동네라면? 면도기는 당연히 맥주와 멀지 않은 곳에 있어야 한다. 자취생의 필수품인 과자, 육포 등의 안주도 멀지 않은 곳에 있는 것이 유리할 것이다.

이러한 방식으로 분류가 정의되지 않은(unsupervised) 데이터를 통해 그룹을 추정하는 것을 클러스터링이라고 한다. 클러스터링을 통해 20대 대학생의 소비, 30대 남성의 소비 등에 대한 기준을 파악할 수 있다. 클러스터링은 데이터를 통해 사고하는 마케팅 담당자의 필수적인 기술이라고 할 수 있다. 아래의 예시는 영국 소설 몇 권을 무작위로 뽑아, 책의 단어들을 통해 어떤 소설인지를 추정하는 코드다.

```{r text clustering, echo = F, message= F, warning=F}
library(tidyverse)

# Latent Dirichlet Allocation

library(topicmodels)
data("AssociatedPress")
AssociatedPress

ap_lda <- LDA(AssociatedPress, k = 2, control = list(seed = 1234))

## Word-Topic Probabilities

library(tidytext)

ap_topics <- tidy(ap_lda, matrix = "beta")

ap_top_terms <- ap_topics %>% 
  group_by(topic) %>% 
  top_n(10, beta) %>% 
  ungroup() %>% 
  arrange(topic, -beta)

beta_spread <- ap_topics %>% 
  mutate(topic = paste0("topic", topic)) %>% 
  spread(topic, beta) %>% 
  filter(topic1 > .001 | topic2 > .001) %>% 
  mutate(log_ratio = log2(topic2 / topic1)) 

## Document-Topic Probabilities

ap_documents <- tidy(ap_lda, matrix = "gamma")

# Example: The Great Library Heist

titles <- c("Twenty Thousand Leagues under the Sea", "The War of the Worlds",
            "Pride and Prejudice", "Great Expectations")

library(gutenbergr)

books <- gutenberg_works(title %in% titles) %>% 
  gutenberg_download(meta_fields = "title")

reg <- regex("^chapter ", ignore_case = T)
by_chapter <- books %>% 
  group_by(title) %>% 
  mutate(chapter = cumsum(str_detect(text, reg))) %>% 
  ungroup() %>% 
  filter(chapter > 0) %>% 
  unite(document, title, chapter)

by_chapter_word <- by_chapter %>% 
  unnest_tokens(word, text)

word_counts <- by_chapter_word %>% 
  anti_join(stop_words) %>% 
  count(document, word, sort = T) %>% 
  ungroup()

## LDA on Chapters

chapters_dtm <- word_counts %>% 
  cast_dtm(document, word, n)

chapters_lda <- LDA(chapters_dtm, k = 4, control = list(seed = 1234))

chapter_topics <- tidy(chapters_lda, matrix = "beta")

top_terms <- chapter_topics %>% 
  group_by(topic) %>% 
  top_n(5, beta) %>% 
  ungroup() %>% 
  arrange(topic, -beta)

## Per-Document Classification

chapters_gamma <- tidy(chapters_lda, matrix = "gamma")
chapters_gamma <- chapters_gamma %>% 
  separate(document, c("title", "chapter"), sep = "_", convert = T)

chapters_gamma %>% 
  mutate(title = reorder(title, gamma * topic)) %>% 
  ggplot(aes(factor(topic), gamma)) +
  geom_boxplot() +
  facet_wrap(~title)
```

4권의 책이 나오고, 실제로 그 추정이 제대로 맞아 떨어짐을 확인할 수 있다. 

#### 데이터 과학자가 하는 일 5 - 증강학습

![데이터 과학자가 하는 일 5 - 증강학습](https://docs.microsoft.com/en-us/azure/machine-learning/studio/media/data-science-for-beginners-the-5-questions-data-science-answers/reinforcement-learning-algorithms.png)

앞에서 배운 4가지의 일. 즉, 분류, 이상징후 포착, 회귀, 클러스터링을 통해 무엇을 할 것인가? 그 최종적인 결론이 증강학습 알고리즘이다. 패턴 몇 가지가 보였을 때 최종적으로 다음 액션이 무엇이 좋을지를 추정하는 것은 알파고가 이세돌의 수를 보고 바둑에 기보하는 것과 같은 방식이다. 증강학습 알고리즘은 '끝판왕'이다.

## 수업에서 다룰 것들

이쯤에서 겁을 먹을 수 있을 것이다.
"저는 수포자.. 문송합니다.."

그러나 겁먹을 필요는 없다. 책에서는 5가지 중 4(분류, 이상징후 포착, 회귀, 클러스터링)가지를 간단하게 배우고, 2가지(분류, 회귀)에 집중할 것이다. 좀 더 긴 시간 동안 여러분이 배우게 될 것은 데이터의 입력과 출력, 전처리, 간단한 시각화, 추론 통계 검증(t-검정, 선형회귀)과 재미있는 프로그래밍이다.

### 앞으로의 진도

중간고사 전까지의 배울 범위(5장까지)는 다음과 같다.
2장: R/RStudio 프로그램 설치와 기본 활용법(단축키, 기초 연산)
3장: 엑셀 익히기(vlookup, 데이터 패키지 익히기)
4장: R프로그래밍 기초(1): 숫자 연산, 변수 지정, 데이터 구조, 함수형 프로그래밍(for-loop / map)
5장: R프로그래밍 기초(2): tidy 문법 익히기

그 이상이 궁금한 학생들이 있을까봐 나중의 진도도 공개는 한다. 하지만 지금 그걸 생각할 필요는 전혀 없다.
