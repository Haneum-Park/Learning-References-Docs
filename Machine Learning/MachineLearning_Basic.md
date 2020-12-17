# Machine Learning

| 1Dep                       | 2Dep                              | 3Dep                 |
| -------------------------- | --------------------------------- | -------------------- |
| 기계학습(Machine Learning) | 지도학습(Supervised Learning)     | 분류(Classification) |
|                            |                                   | 회귀(Regression)     |
|                            | 비지도학습(Unsupervised Learning) | 군집화(Clustering)   |
|                            |                                   | 변환(Transform)      |
|                            |                                   | 연관(Association)    |
|                            | 강화학습(Reinforcement Learning)  |                      |

![출처: https://opentutorials.org/module/4916/28934](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/4916/12287.jpeg)



## 지도학습(Supervised Learning)

```
맞춰야 하는 값.
문제가 있고 정답이 있다.
즉, 정답이 있는 문제를 해결해야 하는 모델을 만드는 방식을 지도학습이라고 한다.
지도학습에는 분류(Classification)와 회귀(Regression)가 있다.

예를 들어,

"어떤 학생이 대학원에 합격할 지의 여부를 예측하여라.", "저 사람이 결혼할 지 평생 혼자 살 지를 예/아니오로 값을 예측하여라", "지금의 집 값이 7억인데 내년에는 집 값이 얼마가 될 것인지를 예측하여라." 등과 같이 정확한 값이 있는 것을 예측하는 것까지 모두 지도학습의 범주에 속한다. Target value(label)가 있는 것이라고도 한다.
```

![출처: https://process-mining.tistory.com/98](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FyEqFW%2FbtqAbnhbIEc%2FjzXu4mVNInnbHwipbUsXCK%2Fimg.png)

### 분류(Classification)

```
예측하는 값이 Categorical한 것을 말한다(예측하는 값들의 범주가 있는 것).
이 예측하는 값은 합격여부 처럼 예/아니오로 답이 나올 수도 있고, 어떤 사람의 출신 지역을 예측하는 것처럼 여러 가지의 값이 될 수도 있다.
이 때, 앞의 경우처럼 예측값이 두 개인 경우를 Binary Classification, 뒤의 경우를 Multi-class Classification이라고 한다. 
이의 예시로는 Support Vector Machine, Logistic Regression 등이 있다.
```

### 회귀(Regression)

```
예측하는 값이 Continuous한 것을 말한다.
분류에서 들었던 예시처럼 집 값이 얼마가 될 지 예측하는 것 등이 이에 해당한다.
```



## 비지도학습(Unsupervised Learning)

```
지도학습과는 반대되는 개념이다.
맞춰야하는 값이 없는 것을 말한다.
즉, label이 없는 문제를 해결해야하는 것이다.
비지도학습에는 군집화(Clustering), 변환(Transform), 연관(Association)이 있다.

예를 들어,

100명의 사람들을 비슷한 사람들끼리 3개의 묶음으로 묶어야 한다고 하면, 우리는 각자 1-3으로 라벨링된 사람들을 기준으로 라벨링되지 않은 사람들을 묶는 것이 아니라, 아무런 라벨없이 이들의 특성을 종합적으로 파악해서 묶어야 할 것이다. 이러한 경우를 비지도 학습이라고 한다.
```

![출처: https://process-mining.tistory.com/98](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FteOhY%2FbtqAdcTiDgO%2FgxWk6zkJwLcVIZl3YHojfK%2Fimg.png)

### 군집화(Clustering)

```
비슷한 것들을 묶는 것을 말한다.
주로 K-means clustering, DBSCAN, SOM등 클러스터링엔 다양한 알고리즘이 존재한다.
```

### 연관(Association)

```
어떤 사건이 얼마나 자주 함께 발생하는지, 서로 얼마나 연관되어 있는지를 분석하는 것을 말한다.
```

### 변환(Transform)

```
데이터를 새롭게 표현하여 사람이나 다른 머신러닝 알고리즘이 원래 데이터보다 쉽게 해석할 수 있도록 만드는 알고리즘
```



## 강화학습(Reinforcement Learning)

```
시행착오를 통해 학습하는 방법이다.
이러한 강화(reinforcement)를 바탕으로 실수와 보상을 통해 학습을 하여 목표를 찾아가는 알고리즘이다.

예를 들어,

아이가 처음 걸을 때 걷는 방법을 어떻게 행동할 줄 모르지만, 환경과 상호작용하면서 걷는 법을 알아가는 것이다.

강화학습의 특징은 두 가지이다.
1. Trial and Error
2. Delayed Reward

첫 번째, 환경과 상호작용으로 학습하는 것과 관련이 있다.
즉, 시행착오를 겪으며 자신을 조정해 나가는 것이다.
좋은 행동을 했을 경우 좋은 반응이 환경으로부터 오게된다. 이 반응을 보상이라고 한다.
강화학습의 핵심 쟁점 중 하나는 "어떻게 상을 더 많이 받을 것이냐"이다.

두 번째, 강화학습이 다루는 문제는 시간이라는 개념이 포함되어있다는 것과 관련이 있다.
강화학습은 시간의 순서가 있는 문제를 풀기 때문에 지금 한 행동으로 인한 환경의 반응이 행동 이후에 나타난다.
이럴 경우 환경이 반응할 때까지 여러가지 다른 행동들을 시간의 순서대로 했기 때문에 어떤 행동이 좋은 행동이었는지 판단하기 어려운 점이 이다.
```

