---
title: '[HTML] HTML 태그들 - 1'
author: Bandito
date: 2020-12-21 20:40:00 +0900
categories: [Study, HTML]
tags: [HTML, Inflearn, FrontEnd]
toc: false
comment: true
---

# HTML 태그들 - 1

프론트엔드를 공부하면서 햇갈리거나 자주 까먹는 태그들을 정리

+ 이 문서에 있는 태그 목록
    - [img](#img)
    - [ul, ol, li](#ul-ol-li)
    - [iframe](#iframe)
    - [table](#table)
    - [label](#label)
    - [meta](#meta)

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

## ul ol li
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
<iframe src="불러올 페이지 주소" scrolling="스크롤링 허용여부" sandbox>
     iframe 미지원 시 출력될 텍스트
</iframe>
```
+ src : 불러올 페이지의 주소
+ scrolling : 아이프레임 안에서 스크롤링을 허용할 것인지를 지정함
    - auto : 스크롤이 필요한 경우에만 스크롤 바 노출 (defualt)
    - yes : 스크롤링 허용. 스크롤 바 무조건 노출
    - no : 스크롤 하지 않음 
+ sandbox : iframe에서 폼이나 자바스크립트가 실행되지 못하게 함
    - allow-forms : 폼 실행 허용
    - allow-same : origin이 같은 도메인의 리소스 이용 가능
    - allow-scripts : 스크립트 실행 어용 

width, height, framborder(프레임 테두리 사용 여부) 등의 속성이 있지만, CSS 를 사용하는 것이 권장됨

iframe은 외부의 페이지를 불러오는 태그이므로 신뢰할 수 없는 소스를 가져올 경우 위험할 수 있다.


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

## meta
***
```html
<head>
    <meta charset="utf-8">
    <meta name="속성명" content="내용">
    <meta http-equiv="속성명" content="내용">

    <meta property="og:type" content="website">
    <meta property="og:title" content="페이지 제목">
    <meta property="og:description" content="페이지 설명">
    <meta property="og:image" content="이미지 주소">
    <meta property="og:url" content="페이지 주소">
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
+ property : 오픈그래프 설정 값 작성. 오픈그래프란 웹페이지가 소셜 미디어 또는 오픈그래프 활용 사이트로 공유 시 사용되어지는 정보
    - og:type : 해당 페이지의 유형 
    - og:title : 페이지 제목
    - og:description : 페이지 설명
    - og:image : 보여줄 이미지
    - ig:url : 페이지 주소 


오픈 그래프는 다음과 같이 적용된다 :          
![open_graph](https://drive.google.com/uc?export=view&id=17WT-alPPS_cRYNTkoVcQ8R7GbMHPMICE){: width="500" height="350"}




<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/2039>_   
_<https://www.inflearn.com/course/html-%EA%B8%B0%EC%B4%88>_
