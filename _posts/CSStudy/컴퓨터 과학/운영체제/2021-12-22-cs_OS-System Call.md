---
title: '[CS] 운영체제 - 시스템 호출'
author: Bandito
date: 2021-12-22 23:26:00 +0900
categories: [Study, CS]
tags: [CS, Computer Sceince]
comment: true
---

# 시스템 호출 (System Calls)

## 시스템 호출이란
+ 운영체제는 커널 모드(Kernel Mode)와 사용자 모드(User Mode)로 나뉘어 구동된다.
+ 커널 모드(Kernel Mode)는 입출력 디바이스를 포함하여 모든 주소 영역이 접근 가능하다.
+ 사용자 모드(User Mode)는 명령어의 일부와 하드웨어 기능의 일부만 사용 가능하다.
+ 운영체제에서 프로그램이 구동되는데 있어 파일을 읽어오거나, 파일을 쓰거나, 화면에 메시지를 출력하는 등의 많은 부분이 커널 모드를 사용한다.
+ Protected Instruction 은 프로세스의 실행, 종료나 I/O 작업 등의 사용자가 함부로 사용하면 문제가 될 만한 명령들을 뜻한다. 이는 커널 모드만 사용이 가능하다.
+ 시스템 호출은 이러한 커널 영역의 기능을 사용자 모드가 사용 가능하게 한다.
    - 프로세스가 하드웨어에 직접 접근하여 필요한 기능을 사용할 수 있게 해준다.

<br>

## 시스템 호출의 수행 과정
1. 프로세스가 System Call 호출
2. Trap 이 발생하여 Kernel Mode 로 진입 -> 이 때 현재 상태를 저장함
    - Trap : S/W가 요청하거나 오류로 인해 발생된 인터럽트
3. 요청받은 System Call 수행
4. User Mode 로 돌아감 

<br>

## 시스템 콜의 유형

### 프로세스 제어 (Process Control)
+ 끝내기(end), 중지(abort)
+ 적재(load), 실행(execute)
+ 프로세스 생성(create process)
+ 프로세스 속성 획득과 설정
+ 시간 대기(wait time)
+ 사건 대기(wait event)
+ 사건을 알림(signal event)
+ 메모리 할당 및 해제(malloc, free)

### 파일 조작 (File Manipulcation)
+ 파일 생성(create file), 파일 삭제(delete file)
+ 열기(open), 닫기(close)
+ 읽기(read), 쓰기(write), 위치 변경(reposition)
+ 파일 속성 획등 및 설정


### 장치 관리 (Devide Management)
+ 장치를 요구(request devices), 장치를 방출(release device)
+ 읽기, 쓰기, 위치 변경
+ 장치 속성 획득, 장치 속성 설정
+ 장치의 논리적 부착(attach) 또는 분리(detach)

### 정보 유지 (Information Maintenance)
+ 시간과 날짜의 설정과 획득(time)
+ 시스템 데이터의 설정과 획득(date)
+ 프로세스 파일, 장치 속성의 획득 및 설정


### 통신 (Communication)
+ 통신 연결의 생성, 제거
+ 메시지의 송신, 수신
+ 상태 정보 전달
+ 원격 장치의 부착 및 분리



