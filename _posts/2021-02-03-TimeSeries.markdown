---
title:  "Fastcampus"
excerpt: "시계열 Feature Engineering"

categories:
  - Fastcampus
tags:
  - [Fastcampus, 패스트캠퍼스, Python, 파이썬, 시계열]

date: 2021-02-03
last_modified_at: 2021-02-03
---

### 빈도(Frequency)
계절성 패턴이 나타나기 전까지의 데이터 갯수  

1. 데이터가 어떤 frequency로 있는지 확인
2. 여러 frequency를 사용하여 데이터 분석 필요 (변환과정에서 생기는 결측값 채우기)
3. 원데이터 결측값 채우기

이에 대한 설명은 아래와 같다.
1. ex) 월별 데이터인 경우 12, 주별 데이터인 경우 52
2. 데이터 분석 시, 여러 frequency를 사용하여 분석을 시도해야 한다.  
ex) 내년 매출을 예측하고자 할 때,
년도별 데이터를 이용할지 혹은 일별 데이터를 이용하여 예측하고 aggregate할지 생각해야한다. 이 때, 대부분 평균을 이용하여 aggregate한다.

frequency를 변환하는 과정에서 NA값이 발생하고 이를 채우고자 할 때 사용하는 대표적인 방법은 다음과 같다. 그중에서도 뒤의 값으로 채우는 bfill과 앞의 값으로 채우는 ffill을 많이 사용한다.

| Method | Description |
|---------|-----------------------------------------------------------|
| bfill | Backward fill |
| ffill | Forward fill |
| first | First valid data value |
| last | Last valid data value |
| mean | Mean of values in time range |
| median | Median of values in time range |

3. 원데이터에 결측값이 있는 경우 위의 방법과 마찬가지로 결측값을 채워줘야 한다.

### 추세(Trend)
시계열이 시간에 따라 증가 혹은 감소하는 경향
<center>$Y_t = f(t) + Y^s_t$</center>
trend가 제거된 $Y^s_t$로 분석하는게 더 정확할 수 있다. 이를 $Y^s_t = $Y_t - f(t)$ 로 표현할 수도 있지만 $Y_t = aT + bX$ 로 표현할 수도 있다. 이는 추세와 $X$의 선형결합으로 표현한 것으로 추세를 제거하여 변환할 필요 없이 feature로 반영하는 것이다.

### 계절성(Seasonality)
일정한 빈도로 주기적으로 반복되는 패턴

### 주기(Cycle)
일정하지 않은 빈도로 발생하는 패턴

계절성과 주기를 혼동하기 쉬운데 주기는 scale이 일정하지 않은 경우를 뜻한다. 하지만 현실적으로 계절성과 주기를 엄격하게 구분짓는 것은 어려워 두 개념 모두 기억하도록 하자.

### 시계열 데이터 분해
<center>$Y_t = T_t + S_t + e_t$</center>
시계열 데이터는 추세, 계절성, 주기로 표현할 수 있다.

### 잔차(Residual)
위의 식에서도 알 수 있듯이 잔차는 원데이터에서 추세와 계절성을 제거한 것이다.
