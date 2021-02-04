---
title:  "Recursive Algorithm"
excerpt: "재귀 알고리즘"

categories: algorithm
tags: algorithm

date: 2021-02-05
last_modified_at: 2021-02-05

layout: post
comments: true
use_math: true
---

**재귀**는 어떠한 사건에서 자기 자신을 포함하고 다시 자기 자신을 사용하여 정의하는 경우를 뜻합니다. 대표적인 예시로 자연수의 정의와 팩토리얼이 있습니다. 자연수의 정의는 어떤 자연수의 바로 다음 수도 자연수입니다. 팩토리얼은 `factorial()` 함수의 원리로 이해할 수 있는데요. `factorial()` 함수는 `n*factorial(n-1)`로 계산하고 이 과정에서 자신과 똑같은 함수를 호출합니다.

재귀 알고리즘은 풀어야 할 문제나 계산할 함수 또는 처리할 자료구조가 재귀적으로 정의되는 경우에 적용됩니다.

재귀 알고리즘을 재귀적으로 나타내는 방법을 알아봅시다. 맨 끝에서 실행되는 재귀 호출인 꼬리 재귀를 제거하거나 스택을 이용하여 값을 저장하여 비재귀적으로 나타낼 수 있습니다.
