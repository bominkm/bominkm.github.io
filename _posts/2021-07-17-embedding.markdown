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

자연어처리(NLP, Natural Language Processing)는 일상생활에서 사용하는 언어인 자연어의 의미를 분석하여 컴퓨터가 처리할 수 있도록 하는 과정입니다. 그 중에서도 컴퓨터가 자연어를 이해할 수 있도록 단어를 변환하는 과정을 **Embedding**이라고 합니다. 초기 NLP는 단어를 하나의 작은 단위로 취급하여 one-hot-encoding 방식을 사용했습니다. 이러한 방식은 컴퓨터가 각 단어의 유사도를 판별할 수 없고 데이터의 크기에 따라 성능이 크게 좌우된다는 단점이 있습니다. 이를 보완하기 위해 distributed representation 방식이 사용됩니다. 이는 비슷한 분포를 가진 단어들은 비슷한 의미를 가진다는 의미로 같은 문맥에서 등장하는 단어는 비슷한 의미를 가질 것이라는 뜻입니다.

* NNLM
* RNNLM
