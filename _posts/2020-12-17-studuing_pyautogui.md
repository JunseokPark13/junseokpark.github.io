---
title: '[Python] PyAutoGui로 키보드와 마우스 제어하기'
author: Bandito
date: 2020-12-17 13:40:00 +0900
categories: [Study, Python]
tags: [Python, Inflearn]
comment: true
---

![Alt text](/assets/img/posting/17_pyautogui.jpg)

# PyAutoGui

파이썬을 사용하여 키보드와 마우스를 조작할 수 있는 모듈
이를 통해 간단한 메크로를 제작할 수 있다

## ○ 설치 방법

명령 프롬프트(cmd) 를 열고 다음 코드를 입력한다 :
```console
pip install pyautogui
```

이후 cmd 에서 python 을 입력하고 직접 코드를 입력할 수도 있지만
파이썬 파일을 만들어 직접 코드들을 실행하는 프로그램을 만들 수도 있다.

단, cmd와 파이썬 파일 모두 다음 코드를 입력하거나 작성해두어야 사용이 가능하다
```console
import pyautogui
```


## ○ 사용할 수 있는 함수

### - 마우스의 현재 위치 알아내기
```python
pyautogui.position()
# 마우스의 현재 위치를 알림
```

### - 해당 좌표로 마우스 이동시키기
```python
pyautogui.moveTo(123, 456, 2)
# x=123, y=456 인 좌표로 마우스를 2초동안 이동시킴
```
지정된 x, y 좌표로 마우스를 이동시킨다.  
이동시간을 입력하면 해당 위치로 입력된 시간동안 이동하며, 입력하지 않으면 즉시 이동한다.


### - 현재 위치에서 마우스 이동시키기
```python
pyautogui.moveRel(123, 456, 2)
# 마우스를 현재 위치에서 x=123, y=456 만큼 2초동안 이동시킴
```
마우스를 현재 위치에서 입력한 x, y 좌표만큼 이동시킨다.  
이동시간을 입력하면 해당 위치로 입력된 시간동안 이동하며, 입력하지 않으면 즉시 이동한다.


### - 마우스 클릭하기
```python
pyautogui.click(123, 456, clicks = 2, interval = 0.5, button = 'left')
# x=123, y=456 에서 마우스 왼쪽 버튼을 2번 0.5초 간격으로 클릭한다
pyautogui.doubleClick(123, 456, interval = 0.5, button = 'right')
# x=123, y=456 에서 마우스 오른쪽 버튼을 2번 0.5초 간격으로 클릭한다
```
지정된 x, y 좌표에서 마우스를 지정된 클릭 횟수, 간격, 버튼 종류만큼 누른다.
더블클릭은 doublClick 함수로 진행할 수 있다.   
아무 매개변수도 없으면 현재 마우스의 위치에서 클릭을 수행하며, 매개변수 순서대로 입력하거나, 직접 변수명으로 값을 지정할 수도 있다.  
button 은 left, right, middle, primary, secondary 를 사용 가능하며, 기본 값은 left 이다.


### - 마우스 클릭하기 2
```python
pyautogui.mouseDown(123, 456)
# x=123, y=456 에서 마우스 좌 다운
pyautogui.mouseUp(123, 456)
# x=123, y=456 에서 마우스 좌 업
```
지정된 x, y 좌표에서 마우스를 누르고 떼는 함수이다.  
클릭을 하지 않고 동작을 나누어 사용할 때 쓴다.


### - 드래그&드롭, 스크롤
```python
pyautogui.dragTo(123,456, duration=2)
# x=123, y=456 으로 2초동안 드래그
pyautogui.dragRel(123,456, duration=2)
# 현재 위치에서 x=123, y=456 만큼 2초동안 드래그
pyautogui.scroll(100, 123, 456)
# x=123, y=456 위치에서 100 만큼 스크롤
```
마우스의 드래그 기능을 사용하는 함수이다. 지정된 좌표까지 드래그하면서 이동하거나,  
현재 위치에서 일정 거리 이동할 때 사용 가능하다.  
스크롤 함수는 첫 번째 매개변수가 스크롤로 이동할 거리이고, 이후가 x, y 좌표를 의미한다.


### - 키보드 입력하기
```python
pyautogui.typewrite('Hello!')
# Hello! 라고 입력하기
pyautogui.typewrite(['Enter'])
# Enter 버튼 누르기
pyautogui.typewrite(['a', 'Enter', 'b'])
# a 라고 입력 후 Enter 버튼을 누르고 b 입력
```
직접 문자열을 입력하거나, 키보드 버튼을 지정해서 누를 수 있다.  
여러 버튼을 순차적으로 누르고 싶다면 리스트를 활용한다.


### - 화면에서 지정된 그림 찾기
```python
i = pyautogui.locateOnScreen('img.png')
#img.png 파일과 동일한 부분을 찾아 해당 이미지의 위치와 이미지의 크기를 i에 저장
i = pyautogui.locateCenterOnScreen('img.png')
#img.png 파일과 동일한 부분을 찾아 해당 이미지의 중앙 위치와 이미지의 크기를 i에 저장
```
지정된 이미지를 화면에서 찾아 위치를 출력한다. 아래 함수는 중앙의 위치를 출력한다는 점에서 차이가 있다.  
해당 이미지가 없다면 None 을 출력한다.
저장된 값은 (x좌표, y좌표, 너비, 높이) 형식으로 저장된다.


### - 화면을 캡처하여 저장하기
```python
pyautogui.screenshot('1.png', region = (123,456,30,30))
# x=123, y=456 위치에서 가로 30, 세로 30의 크기로 캡처한 사진을 '1.png' 라는 이름으로 저장
```
원하는 좌표에서 원하는 크기만큼 화면을 캡처하여 이미지 파일로 저장한다.


***

이미 사용하기 간편한 여러가지 매크로 프로그램들이 많지만, PyAutoGui로 매크로 프로그램을 만드는 연습을 해두면 언젠가 쓸모가 있지 않을까 싶다   
<br/><br/>






_참고한 글이나 영상 :_   
_<https://inf.run/r7BD>_   
_<https://blog.naver.com/htblog/221510551432>_
