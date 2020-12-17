# Machine Learning

| 1Dep                       | 2Dep                              | 3Dep                 |
| -------------------------- | --------------------------------- | -------------------- |
| 기계학습(Machine Learning) | 지도학습(Supervised Learning)     | 분류(Classification) |
|                            |                                   | 회귀(Regression)     |
|                            | 비지도학습(Unsupervised Learning) | 군집화(Clustering)   |
|                            |                                   | 변환(Transform)      |
|                            |                                   | 연관(Association)    |
|                            | 강화학습(Reinforcement Learning)  |                      |

## 지도학습(Supervised Learning)

```
맞춰야 하는 값.
문제가 있고 정답이 있다.
즉, 정답이 있는 문제를 해결해야 하는 모델을 만드는 방식을 지도학습이라고 한다.
지도학습에는 분류(Classification)와 회귀(Regression)가 있다.

예를 들어,

"어떤 학생이 대학원에 합격할 지의 여부를 예측하여라.", "저 사람이 결혼할 지 평생 혼자 살 지를 예/아니오로 값을 예측하여라", "지금의 집 값이 7억인데 내년에는 집 값이 얼마가 될 것인지를 예측하여라." 등과 같이 정확한 값이 있는 것을 예측하는 것까지 모두 지도학습의 범주에 속한다. Target value(label)가 있는 것이라고도 한다.
```

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

