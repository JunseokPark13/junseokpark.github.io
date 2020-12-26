---
title: '[CSS] CSS 정리 - 2'
author: Bandito
date: 2020-12-26 18:40:00 +0900
categories: [Study, CSS]
tags: [CSS, HTML, FrontEnd]
toc: false
comment: true
---

# CSS 정리 - 2

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [font-size](#font-size)
    - [text-align](#text-align)
    - [font](#font)
    - [Inheritance](#Inheritance)
    - [Selecter-Cascading](#Selecter-Cascading)


<br/>

## font-size
```html
<style>
    #forpx{
        font-size:16px;
    }
    .forrem{
        font-size:1rem;
    }
</style>
...
<div id="forpx"> PX </div>
<div id="forrem"> REM </div>
```


font-size 를 px 로 맞추게 되면 해당 텍스트는 고정적인 크기를 갖게 된다.
rem 은 브라우저 설정의 font-size 설정을 따라 상대적으로 변화하는 크기를 갖게 된다. 

이는 단순히 브라우저의 확대, 축소 정도에 따른 변화가 아닌 글꼴 크기 설정에 따라 달라진다.

브라우저의 폰트 크기가 16px로 설정되어있다면 1rem은 16px, 2rem은 32px의 크기를 갖게되는 식 


<br/>

## text-align
```html
<style>
    #a1{ text-align:left;}
    #a2{ text-align:center;}
    #a3{ text-align:right;}
    #a3{ text-align:justify;}
</style>
```

+ text-align : 텍스트의 정렬 방향을 지정함
    - left : 왼쪽 정렬
    - center : 가운데 정렬
    - right : 오른쪽 정렬
    - justify : 양쪽 정렬 (줄바꿈 시 양측의 경계선 부분을 정리해줌)


<br/>

## font
```html
<style>
    #a1{ 
        font-size: 폰트크기;
        font-family: 폰트1, 폰트2, 폰트3, generic-family;
        font-weight: 굵기;
        line-height: 높이;
    }
    #a2{ 
        font: 굵기 폰트크기/높이 폰트1, 폰트2, 폰트3, generic-family;
    }

</style>
```

+ font-size : 폰트의 크기 값을 지정. px, em, rem
+ font-family : 사용하고자 하는 폰트 작성. 처음 적은 폰트가 없다면 다음에 적힌 폰트를 사용하고, 마지막 폰트는 다른 폰트들이 모두 미지원일 경우를 대비하여 generic-family(포괄적 폰트 패밀리 그룹)을 작성해준다. 
    - serif : 장식이 있는 명조계열 폰트
    - sans-serif : 장식이 없는 고딕계열 폰트
    - monospace : 글자 폭과 간격이 일정한 고정폭 폰트
    - cursive : 필기체, 흘림체
    - fantasy : 화려한 글꼴 
+ font-weight : blod, bloder 혹은 값을 입력하여 폰트의 두께를 설정
+ line-height : 줄 간격 
+ font-style : 이탤릭체 등의 글꼴 스타일 지정 
+ font-variant : 글꼴 변형 
+ font : 위 속성들을 한 줄로 적을 수 있음. 순서에 맞추어 적어야 한다.    
    - font : font-style font-variant font-weight **font-size**/line-height **font-family**    
    이 중 font-size와 font-family 는 필수이다.   


#### + 웹 폰트 사용하는 방법 
[Google fonts](https://fonts.google.com/){: target="_blank"} 를 사용하면 무료로 쉽게 웹 폰트를 사용이 가능하다.    

원하는 폰트를 고르고 사이트에서 제공하는 코드 (&lt;link&gt; or @import)를 &lt;head&gt; 내에 포함시킨다.   

그 후 font-family에 사이트에서 제공하는 값을 적어주면 폰트를 적용 가능하다.

<br/>

참고 : [네이버 폰트 자료실](https://software.naver.com/software/fontList.nhn?categoryId=I0000000#brandId=){: target="_blank"}


<br/>

## Inheritance

CSS 에서 어떠한 태그에 설정을 할 때, 상위 태그에 설정한 옵션이 하위 태그까지 영향을 미치는 경우가 있다. 이를 상속이라고 한다.    

이러한 상속을 사용하여 더 큰 범위에 CSS 속성을 적용하고 구분을 하고 싶은 태그들은 class 나 id 설정을 통하여 세부적으로 변화를 줄 수 있다.   

하지만 모든 CSS 속성에 대해 상속이 이루어지는 것은 아니다.    

[W3 Full property table](#https://www.w3.org/TR/CSS21/propidx.html){: target="_blank"}에 나오는 표 중 Inherited? 열을 보면 해당 속성이 하위 태그에 상속되는지 여부를 알 수 있다.


<br/>

## Selecter Cascading
```html
<style>
    li{color:red;}
    .classsel{color:blue !important;}
    #idsel{color:green;}
</style>
...
<ul>
    <li id="idsel" class="classsel" style="color:Cyan"> CSS TEXT </li>
</ul>
```

Cascade는 폭포라는 뜻이지만, CSS에서는 우선순위에 대한 이야기를 의미한다.    
CSS 에서 제작자는 여러 방식으로 텍스트에 영향을 끼칠 수 있다. 이에 대한 우선순위는 다음과 같다.    

0. !important : CSS 속성 삽입 시 !important 속성을 마지막에 넣는 것
1. Style Attribute : 태그에 직접 style 속성을 삽입하는 것
2. Id Selecter : id에 대한 CSS 속성을 삽입하는 것
3. Class Selecter : class에 대한 CSS 속성을 삽입하는 것
4. Tag Selecter : Tag에 대한 CSS 속성을 삽입하는 것

위 예시에서의 우선순위는 blue, cyan, green, red 순서가 된다.    
태그 선택자에서는 하위 태그의 속성에 우선적으로 적용된다.   

이를 재밌고 이해하기 쉽게 표현한 인포그래픽이 있다 : 
![Cascading_starwars](https://drive.google.com/uc?export=view&id=1Y4cR1vr9ofEgVOUyAbaPZX_wPYpeEE_b)
[출처](https://stuffandnonsense.co.uk/archives/css_specificity_wars.html){:target="_blank"}






<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/4>_   
