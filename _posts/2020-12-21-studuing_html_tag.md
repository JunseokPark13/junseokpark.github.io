---
title: '[HTML] HTML 태그들'
author: Bandito
date: 2020-12-21 20:40:00 +0900
categories: [Study, HTML]
tags: [HTML, Inflearn, FrontEnd]
toc: false
comment: true
---

# HTML 태그들

프론트엔드를 공부하면서 햇갈리거나 자주 까먹는 태그들을 정리
<br />

## img
***
```html
<img src="이미지 주소" alt="대체 텍스트" width='폭' height='높이' longdesc="링크" title="이미지 설명">
```
+ src : 이미지가 위치하는 url
+ alt : 이미지 로딩 중 혹은 로딩 실패 시 표시되는 텍스트
+ width, height : 이미지 크기
+ longdesc : 이미지와 관련된 링크 
+ title : 이미지에 마우스를 올렸을 때 나오는 내용 

<br />

## ul, ol 
***
```html
<ul> <!-- 순서가 없는 리스트 -->
    <li>A</li>
    <li>B</li>
    <li>C</li>
</ul>
<ol> <!-- 순서가 있는 리스트 -->
    <li>A</li>
    <li>B</li>
    <li>C</li>
</ol>
```
+ ul : 순서가 없는 리스트
+ ol : 순서가 있는 리스트 (숫자로 표기)
+ li : 리스트 항목들

<br />

## iframe
***
```html
<iframe src="불러올 페이지 주소" scrolling="스크롤링 허용여부">
     iframe 미지원 시 출력될 텍스트
</iframe>
```
+ src : 불러올 페이지의 주소
+ scrolling : 아이프레임 안에서 스크롤링을 허용할 것인지를 지정함
 - auto : 스크롤이 필요한 경우에만 스크롤 바 노출 (defualt)
 - yes : 스크롤링 허용. 스크롤 바 무조건 노출
 - no : 스크롤 하지 않음 

width, height, framborder(프레임 테두리 사용 여부) 등의 속성이 있지만, CSS 를 사용하는 것이 권장됨

<br />

## 이스케이핑
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

## table
***
```html
<table border="경계선 굵기" cellpadding="셀-경계선 여백 크기" 
            cellspacing="셀-셀 여백 크기" bordercolor="경계선 색">    
    <thead>
        <th> 테이블 </th>
        <tr>
            <td colspan="가로 병합 칸 수" align="가로 정렬 상태" >개인정보</td>
        </tr>
    </thead>
    <tfoot>
        <tr>
            <td colspan="가로 병합 칸 수" align="가로 정렬 상태" >출력완료</td>
        </tr>
    </tfoot>
    <tbody>
        <tr>
            <td rowspan="세로 병합 칸 수" valign="세로 정렬 상태" 
            bgcolor="셀 배경 색">1반</td> 
            <td>이름</td> <td>성별</td> <td>나이</td>
        </tr>
        <tr>
            <td>Name 1</td> <td>남</td> <td>16</td>
        </tr>
        <tr>
            <td>Name 2</td> <td>여</td> <td>18</td>
        </tr>
    <tbody>
</table>
```
<table border="2" cellpadding="5" cellspacing="5" bordercolor="green">    
    <thead>
        <th> 테이블 </th>
        <tr>
            <td colspan="4" align="center" >개인정보</td>
        </tr>
    </thead>
    <tfoot>
        <tr>
            <td colspan="4" align="center" >출력완료</td>
        </tr>
    </tfoot>
    <tbody>
        <tr>
            <td rowspan="3" valign="top" bgcolor="#7B7E7E">1반</td> 
            <td>이름</td> <td>성별</td> <td>나이</td>
        </tr>
        <tr>
            <td>Name 1</td> <td>남</td> <td>16</td>
        </tr>
        <tr>
            <td>Name 2</td> <td>여</td> <td>18</td>
        </tr>
    </tbody>
</table>

<br />

+ thead : 테이블의 최상단에 위치하는 내용들
+ tbody : 테이블의 가운데(몸체)에 위치하는 내용들
+ tfoot : 테이블의 최하단에 위치하는 내용들   
-> 이 요소들은 굳이 지정해주지 않아도 괜찮음 

***

+ th : 테이블 이름
+ tr : table row, 행 (가로줄)
+ td : table data, 열 (세로줄)

***

- border : 테이블 경계선 굵기
- colspan : 셀(가로줄)을 합치는 갯수 지정
- rowspan : 셀(세로줄)을 합치는 갯수 지정
- align : 셀(가로줄) 정렬 (left, center, right)
- valign : 셀(세로줄) 정렬 (top, middle, bottom)
- bgcolor : 셀 배경색 지정
- bordercolor : 셀 경계선 색 지정
- cellpadding : 셀-경계선 사이 여백
- cellspacing : 셀-셀 사이 여백

<br />

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

## label
***
```html
<h2>
    <label for="아이디 지정">ID :</label> 
    <input id="아이디 지정" type="text" name="id" value="default value">

    <label> PW :
        <input id="아이디 지정" type="text" name="pw" value="default value">
    </label>

    <label>
        <input type="checkbox" name="checkbox" value="v"> 체크박스
    </label>
</h2>
```
<label for="id_ID">ID :</label> 
<input id="id_ID" type="text" name="id" value="default value">

<label> PW :
    <input id="id_PW" type="text" name="pw" value="default value">
</label>


다른 태그와 연결시키기 위한 태그   
연결된 양식에 입력하거나 체크, 체크 해제가 가능함 

&lt;label&gt; 내의 for와 input 내의 id를 일치 시키거나 &lt;label&gt; 로 태그를 감싸주면 적용됨

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

## meta
***
```html
<head>
    <meta charset="utf-8">
    <meta name="속성명" content="내용">
    <meta http-equiv="속성명" content="내용">
</head>
```

+ charset : html 문서의 문자 부호화 방식 지정 (utf-8을 자주 쓰게 될 것)
+ name : 메타 정보에 대한 이름. content 와 쌍을 이룸. http-equiv 설정 시 미사용
    - keywords : 문서의 핵심어를 쉼표로 분리하여 표시. 검색엔진에 정보 제공
    - description : 문서에 대한 설명. 검색엔진이 검색 결과와 이를 가져감
    - author : 저자 이름
    - generator : 해당 문서를 생성하기 위하 사용된 소프트웨어
    - application-name : 문서를 표시하는 웹 애플리케이션 이름 
+ content : name, http-equiv와 연관된 값을 작성
+ http-equiv : content 속성 값을 위한 http header 를 제공
    - content-type : 문서에 대한 문자 부호화 방식 지정
    - refresh : 문서 새로고침 간격 (사용이 권장되지 않음)
    - default-style : 사용할 선호된 스타일 시트 

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



<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/2039>_   
_<https://www.inflearn.com/course/html-%EA%B8%B0%EC%B4%88>_
