---
title: '[HTML] HTML 태그들 - 3'
author: Bandito
date: 2020-12-23 22:20:00 +0900
categories: [Study, HTML]
tags: [HTML, Inflearn, FrontEnd]
toc: false
comment: true
---

# HTML 태그들 - 3

프론트엔드를 공부하면서 햇갈리거나 자주 까먹는 태그들을 정리

+ 이 문서에 있는 태그 목록
    - [abbr & acronym](#abbr-acronym)
    - [address](#address)
    - [map, area](#map-area)
    - [base](#base)
    

<br/>

## abbr acronym
***
```html
<abbr title="출력할 메시지"> 텍스트 </abbr>
<acronym title="출력할 메시지"> 텍스트 </acronym>
```
<abbr title="Hyper Text Mark Language"> HTML </abbr>

<acronym title="Random Access Memory"> RAM </acronym>

지정된 텍스트에 마우스를 올리면 title 속성의 내용이 툴팁으로 출력된다.

abbr 은 한 글자씩 읽는 약어일 경우,    
acronym 은 한 단어로 읽는 약어일 경우 사용한다.   

HTML 을 '에이치.티.엠.엘' 이라고 읽고    
RAM 을 '램' 이라고 읽는 차이라고 보면 된다.   

하지만 두 태그가 큰 차이가 없고, acronym은 퇴화되어 HTML5에서 더이상 지원하지 않는다.

<br/>

## address
***
```html
<address>
    E-Mail : xxx@xxx.xxx <br/>
    Address : blabla
    TEL : 123-123-123
</address>
```

페이지의 소유자 또는 작성자의 연락처를 나타내는 태그이다. 기본적으로 기울임 꼴로 출력된다.    
그냥 &lt;p&gt; 를 사용하여도 되지만, 검색 엔진은 주소에 대한 검색을 수행할 때 address 태그를 먼저 탐색하므로 제대로 활용하는 것이 좋다.   

<br/>

## map area
***
```html
<img src="이미지 주소" alt="이미지 설명" usemap="#이름">
    <map name="이름" id="아이디" >
        <area chape="rect" coords="x1, y1, x2, y2" alt="설명1" href="링크1" target="_blank">
        <area chape="circle" coords="x, y, radius" alt="설명2" href="링크2" target="_blank">
    </map>
```
<img src="https://drive.google.com/uc?export=view&id=1GLsbT8TbtMLK03HVzBJmnUpWx3aypaF5" alt="표지판" usemap="#sign" style="width:320px; height:240px">
<map name="sign" id="sign" >
    <area shape="rect" coords="210,200,70,130" alt="진실" href="https://ko.wikipedia.org/wiki/%EC%A7%84%EC%8B%A4">
    <area shape="rect" coords="90,60,180,130" alt="거짓" href="https://ko.wikipedia.org/wiki/%EA%B1%B0%EC%A7%93%EB%A7%90">
</map>

위 이미지를 map 태그로 연결하고, area로 지정된 Lie, Truth 두 구역을 클릭하면 서로 다른 링크로 연결되는 것을 볼 수 있다.


<br/>

## base
***
```html
<head>
    <base href="주소" target="속성">
</head>
```

해당 문서의 모든 상대 주소에 대한 기본 URL과 target 의 속성 값을 정의할 때 사용한다.   
하나의 문서에 최대 하나의 base 요소만 존재할 수 있고, 반드시 head 태그 내에 존재해야 한다.



<br/> <br/>

추후 추가 작성할 예정..



<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/2039>_   
_<https://www.inflearn.com/course/html-%EA%B8%B0%EC%B4%88>_
