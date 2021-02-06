---
title:  "[Programmers] Level 2 소수찾기"
excerpt: "프로그래머스 완전탐색 레벨 2 소수찾기"

categories: programmers
tags: programmers

date: 2021-02-06
last_modified_at: 2021-02-06

layout: post
comments: true
use_math: true
---

### 1. 문제
출처: <https://programmers.co.kr/learn/courses/30/lessons/42839>  

**문제설명**  
한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다. 각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요. 

**제한사항**  
* numbers는 길이 1 이상 7 이하인 문자열입니다.   
* numbers는 0~9까지 숫자만으로 이루어져 있습니다.  
* 013은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.  

**예시**  

| numbers | return | explanation |
|:-----------------------------------------------------:|:-----------------------------------------------------:|-----------------------------------------------------|
| "17" | 3 | [1, 7]으로는 숫자 [1, 7, 17, 71]을, 소수 [7, 17, 71]을 만들 수 있습니다. |
| "011" | 2 | [0, 1, 1]으로는 숫자 [0, 1, 10, 11, 101, 110]을, 소수 [11, 101]를 만들 수 있습니다. |


### 2. 풀이
#### 1) 알고리즘
##### (1) 가능한 숫자 조합 만들기

``` python
# 리스트에 담기
lists = []
for i in range(len(numbers)):
    lists.append(numbers[i])
    
# 숫자 조합 만들기
for digit in range(len(numbers)):
    new = list(set(list(permutations(lists, digit+1))))
    
    # 숫자로 만들기
    numbers = []
    for i in range(len(new)):
        
        # 첫번째 숫자가 0인 경우 제외
        if new[i][0] == '0':
            continue
            
        number = 0
        for j in range(len(new[0])):
            number += int(new[i][j])*(10**(len(new[0])-(j+1)))
        numbers.append(number)
```

* permutation(list, len)  
```python
from itertools import permutations 
lists = ['0', '1', '1']
list(permutations(lists, len(lists)))
```

* set을 이용하여 중복 제거  
```python
list(set(list(permutations(lists, len(lists)))))
```

##### (2) 소수찾기

```python
# 소수 찾기
for j in range(len(value)):  
    prime = []
    if num != 1:
        for k in range(2, num):    
            if num % k == 0:   
                prime.append(k)
                break
        if len(prime) == 0:  
            answer.append(num)
```

##### 2) 성능향상
##### (1) 가능한 숫자 조합 만들기  

```python
lists = list(numbers)
for i in range(len(lists)):
    value = list(set(list(map(''.join, permutations(lists, i+1)))))
```

* map(function, list)  
```python
# 문자열 이어 붙이기
lists = ['0', '1', '1']
list(map(''.join, permutations(lists, len(lists))))
```

##### (2) 소수 찾기
```python
# 소수 찾기
answer = []
for j in range(len(value)): 
    num = int(value[j])  
    if num != 1:
        if num % 2 == 0: # 짝수
            continue
        for odd in range(3, int(num**0.5), 2): # 홀수
            if num % odd == 0:
                break
        answer.append(num)
```

##### 3) 최종 풀이
```python
from itertools import permutations 

def solution(numbers):
    
    # 리스트
    lists = list(numbers)
    answer = []
    
    # 배열의 원소를 조합
    for i in range(len(lists)):
        
        # 중복 제거
        value = list(set(list(map(''.join, permutations(lists, i+1)))))
        
        # 소수 찾기
        for j in range(len(value)):
            # 첫 글자가 '0'이 아닌 경우만
            if value[j][0] != '0':   
                num = int(value[j])  
                if num != 1:
                    if num % 2 == 0:
                        continue
                    for odd in range(3, int(num**0.5), 2):
                        if num % odd == 0:
                            break
                    answer.append(num)

    return len(answer)
```
