---
title: '[HTML] HTML 태그들 - 2'
author: Bandito
date: 2020-12-23 20:40:00 +0900
categories: [Study, HTML]
tags: [HTML, Inflearn, FrontEnd]
toc: false
comment: true
---

# HTML 태그들 - 2

프론트엔드를 공부하면서 햇갈리거나 자주 까먹는 태그들을 정리

+ 이 문서에 있는 태그 목록
    - [select](#select)
    - [form](#form)
    - [input](#input)
    - [video](#video)
    - [이스케이핑](#이스케이핑)
    - [의미론적 태그](#의미론적-태그)
    - [Can I use](#캔아이유즈)

<br/>

## select
***
```html
<form action="값을 넘길 주소">
    <select name="넘어갈 데이터 이름">
        <option value="넘어갈 데이터1"> 값1 </option>
        <option value="넘어갈 데이터2" selected="selected"> 값2 </option>
        <option value="넘어갈 데이터3"> 값3 </option>
        <optgroup label="그룹 이름">
            <option value="넘어갈 데이터4-1"> 값4-1 </option>
            <option value="넘어갈 데이터4-2"> 값4-2 </option>
        </optgroup>  
    </select>
    <input type="submit">
</form>
```
<form action="값을 넘길 주소">
    <select name="넘어갈 데이터 이름">
        <option value="넘어갈 데이터1"> 값1 </option>
        <option value="넘어갈 데이터2" selected="selected"> 값2 </option>
        <option value="넘어갈 데이터3"> 값3 </option>
        <optgroup label="그룹 이름">
            <option value="넘어갈 데이터4-1"> 값4-1 </option>
            <option value="넘어갈 데이터4-2"> 값4-2 </option>
        </optgroup>       
    </select>
    <input type="submit">
</form>

셀렉트 박스 요소를 위한 코드

+ form : select, input과 같은 태그들의 값을 넘길 때의 목표 주소 및 범위 지정
+ select : option 태그들을 묶어 셀렉트 박스를 생성
    - form : 값을 보낼 form id를 지정
    - multiple : 여러 옵션을 선택 가능 (ctrl 키로 다중선택)
    - name : 이 요소의 이름 지정
    - required : 반드시 목록 중 하나를 선택해야 함
    - size : 한번에 보일 옵션의 개수
+ option : 셀렉트 박스에서 선택될 요소들
    - value : 선택 시 실질적으로 넘어가는 데이터
    - selected : 해당 요소가 기본값으로 설정됨
+ optgroup : 하위 요소로 구분하기 위한 분류 태그


<br />

## form
***
```html
<form action="목적지 주소" method="http방식 지정" enctype="넘기는 content 타입 지정">
    <p> 아이디 : <input type="text" name="id"></p>
    <p> 비밀번호 : <input type="password" name="pw"></p>
    <p><input type="submit" value="Submit"></p>
</form>
```
<form action="url" method="post" enctype="multipart/form-data">
    <p> 아이디 : <input type="text" name="id"></p>
    <p> 비밀번호 : <input type="password" name="pw"></p>
    <p><input type="file" name="profile"></p>
</form>
<br/>

+ form : 웹 페이지의 정보를 다른 페이지로 전송하는 역할. input 태그의 정보를 넘김
    - action : 데이터를 보내는 목적지 주소
    - enctype : 넘기는 Content 타입 지정. 주로 파일을 넘길때 multipart/form-data 으로 지정
    - method : 폼을 서버로 전송하는 http 방식 지정. POST, GET 존재함
        + get : url 뒤에 input 박스 내용이 노출됨
        + post : input 박스 내용이 노출되지 않음 
    - name : 폼을 식별하기 위한 이름 지정
    - target : action 에서 지정한 페이지를 여는 방식
        + _self : 현재 페이지에서 작동
        + _blank : 새로운 페이지에서 작동

<br />

## input
***
```html
<form action="목적지 주소" method="http방식 지정" enctype="넘기는 content 타입 지정">
    <input type="input 타입 지정" id="아이디" name="이름" value="기본값">
</form>
```
+ input : 사용자로부터 입력 값을 받기 위해 사용하는 태그 
    - id : 주로 스크립트에서 다루기 위한 이름 지정. 페이지 내 중복지정 불가능
    - name : action의 주소로 전달하기 위한 이름 지정. 중복사용 가능 
    - value : 입력하지 않았을 때의 기본 값 
    - type : 보내는 값의 형식 
        + **text** : 기본 텍스트
            - minlength, maxlength : 최소, 최대길이
              password, tel, url 등에도 사용 가능
            - pattern : 값이 유효하기 위해 일치해야 하는 패턴 (정규표현식 사용)   
              ex) [a-zA-z].+[0-9] : 알파벳 하나와 어떠한 문자건 1개 이상 오고 마지막에는 숫자로 끝나야 함   
              -> 가능 : a1, a22, abc4, ab333     
                 불가능 : a, 1, b, ab, a4b        
              password, tel 에도 사용 가능
        + **number** : 숫자만 입력 가능 
            - min, max : 최소, 최대값 지정
        + email : 이메일 주소 지정. 이메일인지 체크하는 유효성 검증 수행
        + **file** : 업로드 파일 지정
            - accept : 허용하는 파일 유형 지정. 허용하는 파일만 선택가능
        + hidden : 보이지 않지만 값은 서버로 전송. value로 값 지정 가능
        + **password** : 값이 가려진 텍스트 필드 지정
        + **radio** : 라디오 버튼 지정
        + **checkbox** : 체크 박스 버튼 지정
        + range : 값이 가려진 숫자를 입력하는 컨트롤
            - min, max : 최소, 최대값 지정
        + reset : 폼 내의 input 값들을 기본값으로 초기화. 비권장됨
        + tel : 전화번호 입력 지정
        + url : URL 입력 지정. URL인지 체크하는 유효성 검증 수행
        + date : 날짜(연월일)을 지정
        + **datetime-local** : 날짜(연월일)과 시간(시분초) 지정. 시간대는 지정 불가
        + month : 연, 월을 지정        
        + week : 시간대가 없는 주-년 값, 주의 값 지정
        + time : 시간대 없는 시간값 지정 
        + **submit** : 양식을 전송하는 버튼
    - autocomplete : 자동 완성 기능 사용 여부를 명시
      on 으로 명시하면 사용자가 이전에 입력했던 값들을 기반으로 비슷한 값들을 보여줌
      form 에도 속성으로 삽입 가능
    - placeholder : 입력 박스에 입력해야 할 값을 알려줄 때 사용 
    - autofocus : 페이지 로드 시 해당 input 요소로 시점이 이동됨
    - required : 필수적으로 입력해야 하는 요소로 지정 


특수한 경우가 아닐 시 text 타입으로 모두 처리할 수도 있으나, 값을 제한해야 하는 상황이나, 사용자에게 적절한 값을 입력할 수 있는 제안이 가능하다.   
특히 모바일 환경에서는 해당 input 타입에 적절한 터치 키보드로 적용될 수 있다.   

하지만 이렇게 제한을 하더라도 악의적인 공격으로 입력할 수 없는 값을 전송하는 것도 가능함           



## video
***
```html
<video width="가로길이" height="세로길이" contorls>
    <source src="비디오 경로">
    video 태그 미지원 시 출력 텍스트
</video>

<video source src="비디오 경로" width="가로길이" height="세로길이" controls>
    video 태그 미지원 시 출력 텍스트
</video>
```

+ video : 웹 페이지에서 영상파일을 재생할 때 사용하는 태그
    - src : 비디오 파일의 주소
    - controls : 컨트롤러 표시
    - autoplay : 자동 재생
    - loop : 반복 재생
    - width : 영상의 가로 길이
    - height : 영상의 세로 길이
    - muted : 음소거 
    - poster : 동영상 재생 전에 보여줄 이미지 주소
    - preload : 페이지를 열 때 무엇을 로드할지 결정   
        autoplay 설정 시 무시됨 
        + auto : 동영상, 메타데이타 모두 로드함
        + metadata : 메타데이타만 로드함
        + none : 로드하지 않음 
+ soucre : video 태그 내에서 source 태그로 따로 지정도 가능함
    - src : 비디오 파일의 주소
    - type : 동영상 타입 

이와 비슷하게 오디오 파일을 재생하는 audio 태그도 존재한다.

<br />

## 이스케이핑
***
```html
<html>
    <body>
        <br />은 줄바꿈을 의미하는 태그입니다.
        &lt;br /&gt;은 줄바꿈을 의미하는 태그입니다.
    </body>
</html>
```
html과 관련된 코드를 직접 출력하기 위한 방식

+ &amp;amp; &nbsp; -> &nbsp; & 
+ &amp;lt; &nbsp; -> &nbsp; <
+ &amp;gt; &nbsp; -> &nbsp; >
+ &amp;quot; &nbsp; -> &nbsp; "
+ &amp;apos; &nbsp; -> &nbsp; '

- <http://www.htmlescape.net/htmlescape_tool.html>    
  원하는 코드에 대한 이스케이핑을 쉽게 알려주는 사이트

<br />

## 의미론적 태그 
***
```html
<html>
  <head>
    <title>My Blog</title>
  </head>

  <body>
    <header> Header </header>
    <nav>
      <ul>
        <li> nav 1</li>
        <li> nav 2</li>
        <li> nav 3</li>
      </ul>
    </nav>
    <section>
      <aritcle>
        의미론적 태그는 실제로 코드에 어떠한 작용을 하진 않는다.
      </aritcle>
      <aritcle>
        문서의 정보를 보다 잘 표현하기 위해 의미에 맞는 태그를 사용할 뿐이다.
      </aritcle>
    </section>
    <footer> footer </footer>
  </body>
</html>
```

의미론적 태그는 실제로 어떠한 기능을 하는 것은 아니지만, html 코드들을 좀 더 잘 분류하고 분명한 의미 부여를 위해 사용한다.

+ article : 본문
+ aside : 광고와 같은, 페이지에 내용과 관계가 적은 내용들
+ details : 기본적으로 화면에 표시되지 않는 정보들
+ header : 화면 상단에 위치하는 사이트나 문서의 전체적 정보
+ footer : 화면 하단에 위치하는 사이트나 문서의 전체적 정보
+ nave : 문서의 네비게이션 항목들 정의
+ section : 문서의 구획들을 정의

<br/>

## 캔아이유즈
***
![CanIUse](https://drive.google.com/uc?export=view&id=11-IbJdD2mFduvgdczmTQ3g2nCNWzxkdj)

HTML 언어는 시간이 지날수록 새로운 태그가 등장하거나, 과거의 태그들의 사용이 비권장되기도 한다. 각종 브라우저의 버전이 변경되면서 기존의 태그들이 사용 불가능하게 될 수도 있다.   

[caniuse.com](https://caniuse.com/) 이란 사이트에서 자신이 사용하고자 하는 태그가 각 브라우저의 버전에서 제대로 동작하는지에 대한 여부를 알 수 있다.   



<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/2039>_   
_<https://www.inflearn.com/course/html-%EA%B8%B0%EC%B4%88>_
