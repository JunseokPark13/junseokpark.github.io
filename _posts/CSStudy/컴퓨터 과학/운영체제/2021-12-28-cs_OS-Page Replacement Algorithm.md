---
title: '[CS] 운영체제 - 페이지 교체 알고리즘'
author: Bandito
date: 2021-12-28 18:04:00 +0900
categories: [Study, CS]
tags: [CS, Computer Sceince]
comment: true
---

# 페이지 교체 알고리즘

## 페이지 교체 알고리즘이란
+ 운영체제는 주 기억장치보다 더 큰 용량의 프로그램을 실행하기 위해 프로그램의 일부만 주 기억장치에 적재하여 사용하는 **가상 메모리 기법** 을 사용한다.
+ **요구 페이지 기법**으로 프로세스가 특정 페이지를 로딩하는데, 필요한 페이지가 주 기억장치에 적재되지 않았을 시에는 이를 **페이지 부재** 라고 한다.
+ 페이지 부재 시에는 페이지를 찾아 빈 프레임에 로딩해야 하는데, 만약 페이지를 올릴 빈 프레임이 없을 경우에는 기존의 프레임과 교체를 수행해야 한다.
    - 프레임 : 물리 메모리를 일정한 크기로 나눈 블록
    - 페이지 : 가상 메모리를 일정한 크기로 나눈 블록
+ 이 때 사용하는 것이 **페이지 교체 알고리즘** 이다.


<br>


## 페이지 교체 알고리즘의 종류

### FIFO (First In First Out)

<br>

![image](https://user-images.githubusercontent.com/49611158/147542331-adeca234-93e8-4c3a-9373-e102cb53ed1f.png)

<br>

+ 가장 간단한 알고리즘으로, 메모리에 올라온지 가장 오래된 페이지를 교체한다.
+ 각 페이지가 올라온 시간을 페이지에 기록하거나, 페이지가 올라온 순서를 큐에 저장하는 방식을 사용한다.
+ 이해가 쉽고 구현이 간단하지만, 항상 성능을 보장하지는 않는다.
    - 자주 사용하는 페이지가 순서에 밀려 계속 Unload 와 load 를 반복하는 경우가 생길 수 있다.

<br>

### Optimal 

<br>

![image](https://user-images.githubusercontent.com/49611158/147543118-674188c4-4ba4-4ed0-bde5-396c710093b1.png)

<br>

+ 앞으로 가장 오랫동안 사용되지 않을 페이지를 교체하는 알고리즘이다.
+ 가장 오랫동안 사용되지 않을 페이지를 알고 교체하기 때문에 모든 페이지 교체 알고리즘 중 **가장 페이지 교체 수가 적다**.
+ 이를 위해서는 프로세스가 앞으로 사용할 페이지를 미리 알아야 하는데, 이를 실제 활용에서는 알 방법이 없기 때문에 **구현이 불가능**한 알고리즘이다.
+ 때문에 이 알고리즘은 실제 구현보다는 다른 알고리즘과 비교 연구 목적을 위해 주로 사용된다.


<br>

### LRU(Least Recently Used)

<br>

![image](https://user-images.githubusercontent.com/49611158/147545470-5199cb0a-8148-41d1-b37a-2e065be61f18.png)

<br>

+ 가장 오래 사용되지 않은 페이지를 교체하는 알고리즘이다.
+ 구현이 불가능한 Optimal 알고리즘 방식과 비슷한 효과를 낼 수 있는 방법을 사용한 방식이라고 할 수 있다.
+ Optimal 보다는 페이지 교체 횟수가 많지만, FIFO 보다는 효율적이다.
+ 많은 운영체제가 채택하는 알고리즘이다.

<br>

### LFU(Least Frequently Used)

<br>

![image](https://user-images.githubusercontent.com/49611158/147547210-5e2beba9-4745-470b-89b5-b3cc8b0fb525.png)

<br>

+ 참조 횟수가 가장 적은 페이지를 교체하는 알고리즘이다. 
+ 교체 대상이 될 수 있는 페이지가 여러 개일 경우, LRU 알고리즘을 따라 가장 오래 사용되지 않은 페이지를 교체한다.
+ 초기에 한 페이지를 집중적으로 참조하다가 이후 다시 참조하지 않는 경우, 초기에 쌓인 참조 회수 때문에 메모리에 계속 남아있는 문제가 발생할 수 있다.

<br>

### MFU(Most Frequently Used)

<br>

![image](https://user-images.githubusercontent.com/49611158/147547383-52553c8d-2870-4e1f-b155-7f35952b3eb5.png)

<br>

+ LFU 알고리즘과는 반대로, 참조 횟수가 가장 많은 페이지를 교체하는 알고리즘이다.
+ 참조 횟수가 적은 페이지는 최근에 사용된 것이기 때문에 앞으로 사용될 가능성이 높다는 판단 하에 진행한다.
+ 하지만 LFU에 비해서 구현에 상당한 비용이 들고, 최적 페이지 교체 정책을 LRU 만큼 제대로 구현하지 못하기 때문에 사용률은 낮다.

<br>

### NUR(Not Used Recently)

<br>

![image](https://user-images.githubusercontent.com/49611158/147547596-fcecdb40-26d6-4fec-ab38-195c0d70917d.png)

<br>

+ LRU 와 유사하게 최근에 사용하지 않은 페이지를 교체한다.
+ 각 페이지마다 두개의 비트 (참조 비트, 변형 비트)가 사용된다.
    - 참조 비트 (r) : 페이지가 참조되지 않았을 때 0, 호출되었을 때 1 (모든 참조 비트를 주기적으로 0으로 변경함)
    - 변형 비트 (m) : 페이지 내용이 변경되지 않았을 때는 0, 변경되었을 때는 1
    - 변형비트를 더 우선적으로 생각한다. 
+ 적은 오버헤드로 적절한 성능을 가진다.
+ 교체되는 페이지의 참조 시점이 가장 오래되었다는 것을 보장하지는 못한다.