---
title:  "[Algorithm] Word Embedding"
excerpt: "자연어처리 단어 임베딩"

categories: algorithm
tags: algorithm

date: 2021-07-17
last_modified_at: 2021-07-17

layout: post
comments: true
use_math: true
---

* 본 게시글을 Efficient Estimation of Word Representations in Vector Space 논문을 읽고 작성되었습니다.

자연어처리(NLP, Natural Language Processing)는 일상생활에서 사용하는 언어인 자연어의 의미를 분석하여 컴퓨터가 처리할 수 있도록 하는 과정입니다. 그 중에서도 컴퓨터가 자연어를 이해할 수 있도록 단어를 변환하는 과정을 **Embedding**이라고 합니다. 초기 NLP는 단어를 하나의 작은 단위로 취급하여 one-hot-encoding 방식을 사용했습니다. 이러한 방식은 컴퓨터가 각 단어의 유사도를 판별할 수 없고 데이터의 크기에 따라 성능이 크게 좌우된다는 단점이 있습니다. 이를 보완하기 위해 distributed representation 방식이 사용됩니다. 이는 비슷한 분포를 가진 단어들은 비슷한 의미를 가진다는 의미로 같은 문맥에서 등장하는 단어는 비슷한 의미를 가질 것이라는 뜻입니다.

### 1. Model Architectures
#### 1. NNLM
* Neural Network를 이용하여 단어를 벡터화하는 초기 모델
* Input layer, Projection layer, Hidden layer, Output layer로 구성
* 단어의 수를 선택하는 파라미터 지정해주어야 함
* 중심 단어 이전의 단어만 고려하고 그 이후의 단어는 고려하지 못함
* 계산 복잡도가 매우 높고 느림

#### 2. RNNLM
* NNLM의 한계를 극복하기 위한 모델
* Projection layer 없이 Hidden layer에 recurrent한 연결함
* 과거 정보가 Hidden layer에 표현되는 RNN 모델로 단기 기억 형성

### 2. New Log-linear Models
앞서 설명한 모델의 계산 복잡도는 대부분 모델의 non-linear hidden layer에서 비롯되었습니다. 이는 neural network의 장점이지만, 데이터를 효율적으로 학습할 수 있는 방법이 필요합니다. 새로운 architecture는 앞선 모델을 이용하여 두 가지 단계를 거쳐 학습합니다. 먼저 연속 단어 벡터는 간단한 모델을 사용하여 학습한 다음 N-gram NNLM을 이러한 distributed representation 에서 학습합니다.

#### 1. CBOW
* 빈칸 앞 뒤의 단어를 고려하여 빈칸에 들어갈 단어를 예측하는 모델
* non-linear hidden layer 없이 projection layer가 모든 단어를 공유함
* non-linear hidden layer 없이 projection layer가 

#### 2. Skip-gram
