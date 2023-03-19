---
layout: post
title: "[Python] 백준17626 Four Squares"
subtitle: Algorithm
date: '2023-01-18 00:00:02 +0900'
categories: study
tags: algorithm
image:
  path: /assets/img/algorithm/main.PNG
---

[백준17626 Four Squares 링크](https://www.acmicpc.net/problem/17626)

<!--more-->

## 문제
![문제](/assets/img/algorithm/230118/문제-Four Squares.PNG)

## 예제 입력
![예제](/assets/img/algorithm/230118/예제-Four Squares.PNG)

---

## 코드
```Python
n = int(input())

dp = [0]*50001
dp[1] = 1

for i in range(2, n + 1):
    dp[i] = dp[i - 1] + 1
    for j in range(2, int(i**0.5) + 1): # 2의 제곱, 3의 제곱 등...
        dp[i] = min(dp[i], dp[i - j**2] + 1)

print(dp[n])
```
## 설명
파이썬을 통해서 사용자로부터 입력받아 자료형 list를 사용하여 dp알고리즘으로 Four Squares를 구현했습니다. <br>

---

## 결과
![결과](/assets/img/algorithm/230118/결과-Four Squares.PNG)