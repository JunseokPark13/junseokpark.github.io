---
title: '[CS] 운영체제 - PCB & Context Switching'
author: Bandito
date: 2021-12-22 23:59:00 +0900
categories: [Study, CS]
tags: [CS, Computer Sceince]
comment: true
---

# PCB & Context Switching

## PCB (Process Control Block)

<br>

![image](https://user-images.githubusercontent.com/49611158/147112679-76e06abf-893e-431d-b8c8-6830b293c521.png)

<br>

+ 프로세스가 여러 개일 때, CPU가 CPU 스케쥴링을 통해 관리하는 것을 Process Management 라고 한다. 이때 CPU는 각 프로세스들이 누군이 알아야 관리가 가능하다.
+ 이러한 프로세스의 특징을 갖고 있는 것을 Process Metadata 라고 하고, 다음과 같은 정보들을 포함하고 있다.
    - Process ID (PID)
    - Process State
    - Process Priority
    - CPU Registers
    - Owner
    - CPU Usage
    - Memory Usage
+ 이러한 Process Metadata 는 PCB 에 저장된다. 하나의 PCB 안에는 한 프로세스의 정보가 담긴다.
+ CPU에서는 프로세스의 상태에 따라 교체 작업이 이루어진다. 이 때 앞으로 다시 수행할 대기 중인 프로세스에 관한 저장 값을 PCB에 저장해둔다. 
    1. Interrupt 발생
    2. 할당 받은 프로세스 Waiting 상태로 변경
    3. 다른 프로세스를 Running 상태로 변경

<br>

## Context Switching 

<br>

![image](https://user-images.githubusercontent.com/49611158/147113648-f8d7dde8-6078-4ea7-9295-d321172c2022.png)

<br>

+ 컴퓨터는 수 많은 일들을 동시에 처리하는 것 처럼 보이지만, 사실 Time Sharing 방식으로 여러 프로세스들을 교체해가며 수행하는 것이다.
+ 이를 위해 이전에 수행되던 프로세스들의 정보를 기억할 필요성이 있고, 이를 저장하는 것이 위에서 언급한 PCB 이다.
+ Context Switching 은 이러한 CPU 가 이전 프로세스 상태를 PCB 에 보관하고, 또 다른 프로세스의 정보를 PCB 에서 읽어 레지스터에 적재하는 과정을 의미한다.
+ 인터럽트가 발생하거나, 실행 중인 CPU 사용 허가 시간을 모두 소모하거나, 입출력을 위해 대기해야 하는 경우 Context Switching 이 발생한다.

### Context Switching 의 오버헤드
+ Context Switching 에 걸린 시간과 메모리를 의미한다.
+ 이러한 오버헤드를 감수해야 할 때가 있다.
    - I/O 이벤트 발생 시, 디스크에 명령을 내리고 해당 명령이 종료될 때 까지 기다린다면 CPU 가 아무 일도 하지 않게되고, 이는 곧 CPU 의 낭비와 같다.
    - CPU 를 기다리게 하는 것 보다 다른 프로세스로 바꾸어 CPU를 사용하는 것이 훨씬 이익이다.