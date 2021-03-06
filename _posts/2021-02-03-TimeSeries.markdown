---
title:  "[Fastcampus] Time Series Feature Engineering"
excerpt: "시계열 데이터 분석 Feature Engineering"

categories:
  - Fastcampus
tags: fastcampus

date: 2021-02-03
last_modified_at: 2021-02-03

comments: true
use_math: true
---

### 시계열 데이터 분석 Feature Engineering  


* 본 게시글은 패스트캠퍼스 **파이썬을 활용한 시계열 데이터 분석** 강의를 듣고 작성되었습니다.

#### 1. 빈도(Frequency)
계절성 패턴이 나타나기 전까지의 데이터 갯수  

1. 데이터가 어떤 frequency로 있는지 확인
2. 여러 frequency를 사용하여 데이터 분석
3. 원데이터 결측값 채우기

이에 대한 설명은 아래와 같습니다.

먼저 데이터가 어떤 빈도로 있는지 확인합니다. 예를 들어 월별 데이터인 경우 12, 주별 데이터인 경우 52의 값을 가지게 됩니다.

데이터 분석 시, 여러 frequency를 사용하여 분석을 시도해야 합니다. 예를 들어 내년 매출을 예측하고자 하면 년도별 데이터를 이용할지 혹은 일별 데이터를 이용하여 예측하고 aggregate할지 생각해야합니다. 이 때, 원데이터보다 빈도를 더 작은 단위로 예측하는 경우 대부분 평균을 이용하여 aggregate합니다.

frequency를 변환하는 과정에서 NA값이 발생하고 이를 채우고자 할 때 사용하는 대표적인 방법은 다음과 같습니다. 그중에서도 뒤의 값으로 채우는 bfill과 앞의 값으로 채우는 ffill을 많이 사용합니다.

| Method | Description |
|---------|-----------------------------------------------------------|
| bfill | Backward fill |
| ffill | Forward fill |
| first | First valid data value |
| last | Last valid data value |
| mean | Mean of values in time range |
| median | Median of values in time range |

원데이터에 결측값이 있는 경우에도 위의 방법과 마찬가지로 결측값을 채워줘야 합니다.

#### 2. 추세(Trend)
시계열이 시간에 따라 증가 혹은 감소하는 경향  

\\( Y_t = f(t) + Y^s_t \\)  

trend가 제거된 $Y^s_t$ 로 분석하는게 더 정확할 수 있습니다. 이를 $Y^s_t = Y_t - f(t)$ 로 표현할 수도 있지만 $Y_t = aT + bX$ 로 표현할 수도 있습니다. 이는 추세와 $X$ 의 선형결합으로 표현한 것으로 추세를 제거하여 변환할 필요 없이 feature로 반영하는 것입니다.

#### 3. 계절성(Seasonality)
일정한 빈도로 주기적으로 반복되는 패턴

#### 4. 주기(Cycle)
일정하지 않은 빈도로 발생하는 패턴

계절성과 주기를 혼동하기 쉬운데 주기는 scale이 일정하지 않은 경우를 뜻합니다. 하지만 현실적으로 계절성과 주기를 엄격하게 구분짓는 것은 어려워 두 개념 모두 사용되는 경우가 많습니다.

#### 5. 시계열 데이터 분해

\\( Y_t = T_t + S_t + e_t \\)  

시계열 데이터는 추세, 계절성, 주기로 표현할 수 있습니다.

#### 6. 잔차(Residual)
위의 식처럼 원데이터에서 추세와 계절성을 제거한 값

#### 7. 더미변수(Dummy Variables)
범주형 변수를 0과 1을 이용하여 구분하는 것  

ex) 계절 더미변수  
아래와 같이 봄, 여름, 가을, 겨울은 0과 1을 이용하여 3개의 더미변수로 표현할 수 있습니다.

| $Y_t$ | $X_1$ | $X_2$ | $X_3$ |
| :------------: | :------------: | :------------: | :------------: |
| $Y_1$ | 1 | 0 | 0 |
| $Y_2$ | 0 | 1 | 0 |
| $Y_3$ | 0 | 0 | 1 |

더미변수는 각 X의 값에 따른 Y의 값을 파악할 수 있다는 장점이 있으나 범주가 너무 많으면 사용하기 어렵다는 단점이 있습니다.

#### 8. 지연값(Lagged Values)
변수의 지연된 값을 독립변수로 반영하는 것

지연값은 X와 Y의 시간축이 동일한지 판단하는 데 사용되며 변수의 지연된 값을 독립변수로 반영하여 파악합니다. 예를 들어 광고비와 매출의 관계로 이해할 수 있습니다. 소비되는 광고비와 매출은 동시에 이루어지지 않으므로 지연값이 필요합니다. 이는 ARIMA, VAAR, NNAR 등이 활용되며 시계열 분석 외에도 많이 사용되는 기법입니다.

#### 9. 시간변수
시간변수를 미시/거시적으로 분리하거나 통합하여 생성된 변수
ex) 2021년 2월 3일 오후 1시 13분 17초
세분화된 시간 해석이 가능하며 변수에 많은 정보를 담고 있어 예측력이나 적합도에 도움이 됩니다.

### 결론
1. 시계열 구성요소는 **각 변수의 시간패턴**을 파악하는데 중요합니다. 시간 정보가 담겨있는 X를 통해서 Y와의 관계를 파악할 수 있습니다.
2. Feature Engineering으로 어떠한 **시간 차원**에서 분석할 것인지, 어떤 **입력형태**를 사용할 것인지 결정할 수 있습니다.
3. 생성된 변수가 기존의 모델에서 반영하지 않던 패턴이라면 **예측력**을 높일 수 있습니다.
4. 시계열 구성요소로 시간 정보를 세세하게 분해하여 볼 수 있기 때문에 정확도 뿐만 아니라 **설명력**에도 도움이 됩니다.
