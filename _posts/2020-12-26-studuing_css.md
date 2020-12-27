---
title: '[CSS] CSS 정리 - 1'
author: Bandito
date: 2020-12-26 15:40:00 +0900
categories: [Study, CSS]
tags: [CSS, HTML, FrontEnd]
comment: true
---

# CSS 정리 

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [선택자 (id,class)](#선택자-idclass)
    - [선택자 (부모자식) - 1](#선택자-부모자식---1)
    - [선택자 (부모자식) - 2](#선택자-부모자식---2)
    - [가상 클래스 선택자](#가상-클래스-선택자)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

## 선택자 (id,class)
```html
<style>
    #아이디명{
        color:blue;
    }
    .클래스명{
        color:red;
    }

</style>
...

<a id="아이디명"> blue text</a>
<a class="클래스명"> red text</a>
```

아이디에 대한 css 는 #아이디명 으로 지정    
클래스에 대한 css 는 .클래스명 으로 지정     

아이디는 하나의 태그에만 적용하고 중복사용하지 않는다.   
클래스는 여러 태그에 적용하거나, 다른 태그에도 중복 사용이 가능하다.   

<br/>

## 선택자 (부모자식) - 1
```html
<style>
    ul li{
        color:red;
    }
    #아이디명>li{
        color:blue;
    }
    ol.클래스명{
        color:pink;
    }
    h1, h2{
        color:green;
    }
    h3+h4{
        color:yellow;
    }
    a~h4{
        color:purple;
    }

</style>
```

- A B : A 하위에 있는 B 태그들에 적용
- A>B : A의 바로 하위에 있는 직계 자식 B 태그들에 적용.    
        보통 아이디나 클래스를 지정하여 사용함
- A.B : A이면서 B 클래스인 태그들에 적용. . 대신 #으로 아이디 지정 가능
- A, B : A와 B 태그에 적용 
- A+B : A 다음에 오는 B 태그에 적용. 다른 B 태그에는 적용되지 않음 
- A~B : A 다음에 오는 B 태그들에 적용. 
        다른 태그의 하위에 있는 B에는 미적용

<br/>

## 선택자 (부모자식) - 2
```html
<style>
    h1:first-child{
        color:red;
    }
    h2:only-child{
        color:blue;
    }
    h2:only-of-type{
        color:blue;
    }
    h3:nth-child(2){
        color:green;
    }
    h4:first-of-type{
        color:yellow;
    }
    h4:last-of-type{
        color:yellow;
    }
    h5:nth-of-type(odd){
        color:white;
    }
    :not(#아이디명 or .클래스명)

</style>
```

+ A:first-child : 자식인 A 태그 중 맨 처음 A에만 적용
+ A:only-child : 자식 태그가 A 하나뿐인 경우 적용. 다른 종류도 없어야 함
+ A:only-of-type : 자식 태그가 A 하나뿐인 경우 적용. 다른 종류는 있어도 무관함 
+ A:nth-child(n) : A 태그 중 n 번째에 적용  
    거꾸로 카운트하는 nth-last-child(n) 도 있음
    꼭 어떠한 태그에 대해 하는 것이 아닌, :nth-child(n)으로도 사용 가능
+ A:first-of-type : 등장하는 A 태그 중 맨 처음에 적용
+ A:last-of-type : 등장하는 A 태그 중 맨 마지막에 적용
+ A:nth-of-type(odd,even) : A 태그 중 홀수(odd), 짝수(even)번째에 적용   
    odd, even 외에도 i*n+j 형태로도 사용 가능  
+ :not(#아이디명 or .클래스명) : 아이디명, 클래스명을 가지지 않은 태그 적용

<br/>

## 가상 클래스 선택자
```html
<style>
    a:link{
        color:red;
    }
    a:visited{
        color:blue;
    }
    a:hover{
        color:green;
    }
    a:active{
        color:purple;
    }
    a:focus{
        color:yellow;
    }
</style>
```

위 예시에서는 &lt;a&gt; 태그에 달린 하이퍼링크에 대한 css 처리를 의미한다.

- link : 방문한 적이 없는 링크
- visited : 방문한 적이 있는 링크
- hover : 마우스를 위에 올렸을 때
- active : 마우스를 클릭했을 때
- focus : tab 키 등으로 선택되었을 때 

위 가상 클래스 선택자들은 위에서 아래 순서로 적용되므로 적절한 순서로 배치되지 않으면 무시될 수 있다. 





<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/4>_   
