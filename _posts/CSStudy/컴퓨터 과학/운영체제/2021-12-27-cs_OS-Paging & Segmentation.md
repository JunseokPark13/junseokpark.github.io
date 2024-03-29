---
title: '[CS] 운영체제 - 페이징 & 세그멘테이션'
author: Bandito
date: 2021-12-27 19:43:00 +0900
categories: [Study, CS]
tags: [CS, Computer Sceince]
comment: true
---

# 페이징 & 세그멘테이션

## 가상 메모리 (Virtual Memory)

<br>

![image](https://user-images.githubusercontent.com/49611158/147457032-c38ab809-d34a-4c99-92ad-07cc04c8a93b.png)

<br>

+ 실제 메모리 크기와 상관 없이 메모리를 사용할 수 있도록 가상 메모리 주소를 사용하는 것
+ 프로세스의 일부분만 메모리에 로드하고, 나머지는 보조기억장치(가상 메모리 공간)에 둔다.
+ 이를 통해 실행 중인 프로세스가 가상의 공간을 참조하여, 마치 커다란 물리 메모리를 갖고 있는 것 처럼 사용할 수 있다.
+ 가상 메모리 사용의 장점
    - 실제 메모리 (RAM)보다 더 큰 공간 사용 가능
    - 가상의 주소 공간을 사용하여 논리적인 연속성 제공
    - 물리 메모리의 주소 공간을 알 필요가 없어짐
+ MMU를 통하여 가상 주소를 실제 메모리 주소로 변환하여 사용한다.

<br>

## 메모리 관리 기법

### 연속 메모리 기법
+ 프로그램 전체가 메모리에 연속적으로 할당되어야 하는 관리 기법
+ 고정 분할 기법 : 메모리가 고정된 파티션으로 분할, 내부 단편화 발생
+ 동적 분할 기법 : 파티션들이 동적 생성, 자신의 크기와 같은 파티션에 적재. **외부 단편화 발생**

### 불연속 메모리 관리
+ 프로그램의 일부가 서로 다른 주소 공간에 할당될 수 있는 기법
+ Page : 프로세스를 고정된 크기의 작은 블록들로 나눴을 때, 해당 블록들을 페이지라 함
+ Frame : 페이지 크기와 같은 주 기억장치 메모리 블록
+ Segment : 서로 다른 크기의 논리적 단위


<br>

## 메모리 단편화 (Memory Fragmentation)
+ 컴퓨터에서 어떠한 프로그램을 실행할 때, 메모리의 공간을 연속적인 형태로 할당하여 사용하게 된다.
+ 이렇게 프로그램이 메모리에 할당, 해제를 반복하다보면 메모리 공간의 남은 부분이 조각조각 나뉘게 된다.
    - 실제로 사용 가능한 메모리는 충분하지만, 할당이 불가능한 상태가 발생할 수 있다. 이러한 상황을 **메모리 단편화** 라고 한다.

### 내부 단편화
+ 메모리를 할당할 때, 프로세스가 필요한 양보다 더 큰 메모리가 할당되어 프로세스에서 사용하는 메모리 공간이 낭비되는 상황
    - 어떤 프로그램에서 OS가 5MB 만큼 메모리를 할당하였지만, 실제로는 1MB 만 사용하고 있을 경우 -> 4MB 만큼 내부 단편화 발생

### 외부 단편화
+ 메모리가 할당되고 해제되는 작업이 반복적으로 일어날 때, 할당된 메모리와 메모리 사이에 중간중간 사용하지 않은 작은 메모리가 생김
+ 총 메모리 공간은 충분하지만, 실제로는 할당할 수 없는 상황 발생

<br>

## 페이징 (Paging)

<br>

![image](https://user-images.githubusercontent.com/49611158/147461065-6cab9bcc-a15c-4077-aee7-601016e7b33c.png)

<br>


+ 프로세스의 주소 공간을 동일한(고정된) 사이즈의 페이지 단위로 나누어 물리적 메모리에 불연속적으로 저장하는 방식
+ 외부 단편와의 압축 작업을 해소하기 위함이다.
+ 메모리는 Frame 이라는 고정 크기로 분할되고, 프로세스는 Page라 불리는 고정 크기로 분할된다.
+ 메모리 상에서 여러 곳에 흩어진 프로세스 수행을 위해 MMU를 통해 논리 주소와 물리 주소를 나눠 사용하는 방식으로 CPU를 속인다.
    - 실제 메모리는 연속적이지 않지만, CPU는 연속적으로 사용하고 있다는 것을 보장받으며 정상적으로 수행한다.
+ 프로세스의 정상적인 사용을 위해 MMU의 재배치 레지스터를 여러 개 사용하여 각 페이지의 실제 주소로 변경한다.
    - 이러한 재배치 레지스터를 페이지 테이블(Page Table) 이라 한다.
+ 페이징은 내부 단편화 문제의 비중이 늘어난다는 단점이 존재한다. 

<br>

## 세그멘테이션 (Segmentation)

<br>

![image](https://user-images.githubusercontent.com/49611158/147462306-d15daf2f-06d3-415d-8307-14152aa355c5.png)

<br>


+ 프로세스를 서로 크기가 다른 논리적인 블록 단위인 '세그먼트'로 분할하고 메모리에 배치하는 것을 말한다. 세그먼트의 크기는 일정하지 않다.
    - 프로세스를 **논리적 내용을 기반**으로 나눈다.
    - 프로세스를 Code, Data, Stack 으로 나누는 방식도 세그멘테이션이라고 할 수 있다.
+ 세그먼트를 메모리에 할당할 때는 페이지를 할당하는 것과 비슷하지만, 세그먼트 테이블을 사용한다는 점이 다르다.
    - 세그먼트 테이블은 세그먼트 번호와 시작 주소, 세그먼트 크기를 엔트리로 가진다.
+ 세그먼트의 주소 변환도 페이징과 유사하지만, 세그먼트는 크기가 일정하지 않기 때문에 테이블에 세그먼트 크기에 대한 정보가 주어진다.
    - CPU에서 해당 세그먼트의 크기를 넘어서는 주소가 들어오면, 인터럽트가 발생해서 해당 프로세스를 강제로 종료시킨다.

<br>

## 보호와 공유

### 보호
+ 모든 주소는 테이블을 경유하므로, 테이블을 이용하여 보호 기능을 수행할 수 있다.
+ 테이블마다 r(read), w(write), x(excute) 비트를 두어 해당 비트가 켜져있을 때만 그 수행이 가능하도록 한다.

### 공유
+ 메모리 낭비를 방지하기 위하여, 같은 프로그램을 쓰는 복수 개의 프로세스가 있다면 하나의 code 영역을 공유하여 메모리 낭비를 줄이는 것이다.



<br>

## 페이징과 세그멘테이션의 차이
+ 페이징은 고정 크기를 가진다.
+ 세그멘테이션은 가변 크기를 가진다.
+ 페이징은 내부 단편화 발생 가능성이 있다.
+ 세그멘테이션은 외부 단편화 발생 가능성이 있다.
+ 세그멘테이션과 페이징은 유사하고 보호와 공유 측면에서는 더 나은 측면을 보이지만, 현재는 대부분 페이징 기법을 사용한다고 한다.
    - 메모리 할당을 처음 시작할 때, 다중 프로그래밍에서는 서로 다른 크기의 프로세스로 인해 여러 크기의 hole 이 발생한다. 이는 외부 단편화로 인해 메모리 낭비를 발생시킨다.
    - 세그멘테이션은 세그먼트의 크기가 다양하기 때문에 다양한 크기의 hole 이 발생하게 된다.
+ 세그멘테이션은 '보호와 공유'에서 효율적이고, 페이징은 외부 단편화 문제를 해결할 수 있다.
    - 두 장점을 합치기 위해 세그먼트를 페이징 기법으로 나누는 방법도 있다. (Paged Segmentation)
