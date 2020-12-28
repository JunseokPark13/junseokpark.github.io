---
title: '[CSS] CSS 정리 - 4'
author: Bandito
date: 2020-12-27 21:10:00 +0900
categories: [Study, CSS]
tags: [CSS, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# CSS 정리 - 4

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [Mediaquery](#mediaquery)
    - [Float & Clear](#float--clear)
    - [Multi Column](#multi-column)
    - [Background](#background)
    - [Transition](#transition)
    - [Filter](#filter)
    - [Blend](#blend)
    - [Transform](#transform)


<br/>

## Mediaquery
```html
<style>
    @media (max-width:600px){
        body{
            background-color: green;
        }
    }
    @media (max-width:320px){
        body{
            background-color: red;
        }
    }
    @media(min-width:601px){
        body{
            background-color: blue;
        }
    }
</style>
```

Mediaquery는 여러 휴대 기기의 환경에 따라 변화할 수 있는 옵션들을 지정해주는 속성이다. 핸드폰, 태블릿, 노트북, 데스크톱 등 기기들은 서로 다른 화면 크기를 갖고 있기 때문에 접근성과 편의성을 높이기 위해 필수로 고려해야하는 설정이다.   

간단한 예시로 최대 길이가 몇 이상, 이하일 때 속성들이 달라지는 옵션을 부여할 수 있다.

[w3s Media Rule](https://www.w3schools.com/cssref/css3_pr_mediaquery.asp){: target="_blank"}의 사이트를 통해 Mediaquery에서 사용할 수 있는 다양한 속성을 확인할 수 있다.

<br/>

## Float & Clear
```html
<style>
    img{
        height:300px;
        float:right;
        margin-left:20px;
        margin-right:20px;
        margin-bottom: 10px;
    }
    p{
        border:1px solid gray;
    }
</style>
<img src="../img/이미지이름.png" alt="이미지설명">
    <p>
       ~내용~
    </p>
    <p >
        ~내용~
    </p>
    <p style="clear:both;">
        ~내용~
    </p>
```
![float](https://drive.google.com/uc?export=view&id=13F-4M689_xHmB_RhrdUUPnnc4AvIe_gq)     


Float 은 지정된 요소가 보통의 영역 구분에서 빠져나와 텍스트 및 인라인 요소가 그 주위를 감싸 영역의 측면으로 배치될 수 있도록 하는 속성이다.   
값으로는 none(defualt), left, right 가 있다.    

Clear 는 float 으로 지정된 요소에 대하여 float 취급을 하지 않을 수 있게 설정하는 속성이다.   
left 는 float:left; 에 대해 회피하고, right는 float:right;에 대해 회피한다.   
both 는 left, right 구분 없이 float 취급을 회피한다.    

<br/>

## Multi Column
```html
<style>
    .column{
        text-align:justify;
        column-count:3;
        column-width: 200px;
        column-gap:50px;
        column-rule-style: dashed;
        column-rule-width: 5px;
        column-rule-color:tomato;
    }
    h1{
        column-span: all;
    }
</style>
...
<div id="column">
    ~글~
    <h1>This is the Title</h1>
    ~글~
</div>
```

![multicolumn](https://drive.google.com/uc?export=view&id=1-IhxvOYf5uDHidUmWeoZFStnkfdnYayC)

multi column 은 장문의 글에 신문처럼 텍스트를 열로 나누어 읽기 편하게 만들어 주는 속성이다. 

+ column-count : 최대로 생성될 열 수를 지정한다.
+ column-width : 열의 최대 가로 길이를 지정한다. 화면이 넓을 수록 지정된 크기 만큼의 열을 추가적으로 생성하고, 공간이 부족해지면 열이 줄어든다   
    - column-count와 column-width 를 함께 사용하면 최대 열의 수는 colum-count로 고정되지만, 최대 가로 길이를 보장하지 못하면 열의 수는 줄어든다.
+ column-gap : 열과 열 사이의 여백 길이를 지정한다.
+ column-rule-style : 여백에 넣을 줄의 종류를 지정한다.
+ column-rule-width : 여백에 들어갈 줄의 너비를 지정한다.
+ column-rule-color : 여백에 들어갈 줄의 색을 지정한다.
+ column-span : 본문 중간에 삽입된 요소가 열을 무시하고 자신만의 공간을 보장받게 한다.

<br/>

## Background
```html
<style>
    div{
        border:5px solid gray;
        height:200px;
        background-color:powderblue;
        background-image: url('이미지 주소');
        background-repeat : no-repeat;
        background-attachment:fixed;
        background-size : 300px 300px;
        background-poistion:left center;

        background:powderblue url('이미지 주소') no-repeat fixed left center/300px 300px;
    }
</style>
...
    <div>
        .
    </div>
```

background 는 영역의 배경에 색이나 이미지를 채우기 위해 사용하는 속성이다.    

+ background-color : 배경의 색을 지정한다. 
+ background-image : 배경에 넣을 이미지를 지정한다. 이미지에 가리거나, 이미지의 배경이 투명하지 않다면 background-color는 가려질 수 있다.
+ background-repeat : no-repeat 설정 시 이미지의 반복 등장을 막을 수 있다. repeat이 기본 값
+ background-attachment : fixed 설정 시 스크롤을 따라 이미지가 동일한 위치에서 이동한다. none이 기본 값
+ background-size : 배경 이미지의 크기를 지정한다.
    - contain : 영역에 맞도록 이미지 크기가 변경되지만, 공간에 여백이 생길 수 있다.
    - cover : 영역이 꽉 차도록 이미지 크기가 변경되지만, 이미지가 잘릴 수 있다.
+ background-position : 이미지의 위치를 지정할 수 있다.
    - top, center, bottom / left right
+ background : 위 속성들의 축약형
    - background: color image repeat attachment size/position

<br/>

## Transition
```html
<style>
    div{
    background-color: black;
    color:white;
    padding:10px;
    width:100px;
    height:100p
    transition:height 1s;
    transition-delay:0.1s;
    transition-timing-function: ease-in-out;
    }

    div:hover{
    height:400px
    }
</style>
```

transition은 요소들에 대한 효과가 변경되었을 때 이를 부드럽게 처리하기 위한 속성이다. 

+ transition-property : transition 을 적용할 속성들을 지정한다.
+ transition-duration : transition 처리가 몇초에 걸쳐서 적용될 것인지를 지정한다.
+ transition-delay : transition 처리가 일어나기 전에 어느정도 지연을 줄 지를 지정한다.
+ transition-timing-function : transition 처리가 일어날 때 요소가 변화하는 속도 옵션을 지정한다.
    - [Ceaser](https://matthewlein.com/tools/ceaser)사이트를 활용하면 자신이 원하는 옵션을 테스트하고 직접 적용할 수 있는 코드를 얻을 수 있다.   
+ transition : 위 속성들을 한 줄로 작성할 수 있다.
    - transition:property duration timing-fucntion delay
    - 한 줄에 여러 속성을 지정할 수도 있다.


<br/>

## Filter
```html
<style>
    img{
        transition: all 1s;
    }
    img:hover{
        -webkit-filter:grayscale(50%) blur(3px);
        -o-filter:grayscale(50%) blur(3px);
        filter:grayscale(50%) blur(3px);
    }
</style>
...
    <img src="이미지 주소" alt="이미지 설명">
```

filter는 이미지나 텍스트에 효과를 주기 위한 속성이다.   
여러 속성을 조합하여 여러가지 효과를 동시에 부여할 수 있다.    
-webkit-과 -o- 는 일부 구형 브라우저나 오페라에서는 사용되지 않을 수 있으므로 함께 적어주는 것이 좋다.   

+ blur : 픽셀 수를 지정하여 블러를 적용한다.
+ brightness : 밝기를 조절한다. 0%는 검은색, 100%는 기본 상태이며, 100%보다 큰 값도 허용된다.
+ contrast : 대비를 조절한다. 0%는 회색, 100%는 기본 상태이며, 100%보다 큰 값고 허용된다.
+ drop-shadow : 그림자 효과를 적용한다. 그림자의 위치, 반경, 색 선택이 가능하다.
    - drop-shadow(x, y, length, color)
+ grayscale : 흑백을 조절한다. 100%는 완전 흑백, 0%는 기본 상태이다.
+ hue-rotate : 색조회전을 조절한다. 0deg는 기본상태이고 360deg 이상의 값은 0~360deg 사이를 순환한다.
+ invert : 색을 반전한다. 100%는 정반대, 0%는 기본상태이다.
+ opacity : 불투명도를 조절한다. 0%는 완전히 투명, 100%는 기본 상태이다.
+ sepia : 세피아 필터를 사용한다. 100%는 완전히 세피아, 0%는 기본 상태이다.

transition : all 1s; 옵션은 예시에서 img:hover 가 마우스를 이미지에 올릴 때 적용되는 옵션이므로, 이 옵션이 적용되고 풀리는 것을 1초에 걸쳐 적용시킨다는 의미이다.

<br/>

## Blend
```html
<style>
    .blend_image{
        background-color:green;
        background-image: url('이미지 주소');
        background-blend-mode:옵션;
    }
    body{
        background-image:url('이미지 주소');
    }
    .blend_mix{
        color:red;
        mix-blend-mode:옵션;
    }
</style>
...
<body>
    <div class="blend_image"></div>
    <div class="blend_mix">TEXT</div>
</body>
```

blend는 배경과 배경색 혹은 배경과 텍스트간의 css적인 합성을 지정하는 속성이다. 

background-blend-mode는 하나의 요소에서 지정된 background-color와 background-image 간의 합성,     
mix-blend-mode는 전체 배경과 특정 요소의 텍스트 간의 합성을 지정한다.

<br/>

## Transform

transform 은 요소의 크기를 조절하거나 회전, 변형 등에 사용하는 속성이다.    

아래의 예시를 보고 어떤 옵션이 어떤 효과를 주는지 확인해볼 수 있다.   

각 옵션에서 요구하는 단위가 다르므로 이에 대해 제대로 [확인](https://developer.mozilla.org/ko/docs/Web/CSS/transform){:target="_blank"}해야 한다.    

<iframe height="639" style="width: 100%;" scrolling="no" title="Css3 Transform" src="https://codepen.io/vineethtrv/embed/XKKEgM?height=639&theme-id=dark&default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/vineethtrv/pen/XKKEgM'>Css3 Transform</a> by Vineeth.TR
  (<a href='https://codepen.io/vineethtrv'>@vineethtrv</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>




***

[Codepan](https://codepen.io/){:target="_blank"} 이라는 사이트에 가면 다른 사람들이 만들어 놓은 다양한 CSS 활용 작품들을 참고할 수 있다.      

[hover.css](http://ianlunn.github.io/Hover/), [CSShake](http://elrumordelaluz.github.io/csshake/#1), [Magic Animation](https://www.minimamente.com/project/magic/) 등에서 다양한 CSS 라이브러리를 다운받을 수 있다.   


<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/4>_   
