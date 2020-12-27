---
title: '[CSS] CSS 정리 - 3'
author: Bandito
date: 2020-12-26 22:10:00 +0900
categories: [Study, CSS]
tags: [CSS, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# CSS 정리 - 3

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [Inline & Block](#inline--block)
    - [Box Model](#box-model)
    - [Box Sizing](#box-sizing)
    - [Margin Overlap](#margin-overlap)
    - [Position](#position)
    - [Flex](#flex)

<br/>

## Inline & Block
```html
<style>
    h1,a{
        border:1px solid red;
    }
    h1{
        display:inline;
    }
    a{
        display:block;
    }

</style>
...
<h1>Hello World</h1>
<a>World Hellow</a>
```

태그를 사용할 때 각 태그들은 자신만의 영역이 있다.   
&lt;a&gt;, &lt;span&gt; 등 특정 문자열을 선택하는 태그는 inline
&lt;h1&gt;, &lt;p&gt;, &lt;div&gt; 등 범위를 선택하는 태그는 block이다.    

이는 CSS 에서 display 속성을 직접 지정하여 변경해줄 수 있다.

+ inline : 요소를 inline 으로 표현
+ block : 요소를 block 으로 표현
+ none : 박스가 생성되지 않음. 출력되지 않음
+ inline-block : block처럼 한 줄을 차지하지는 않지만, 자신의 영역을 유지하며 inline처럼 표현


<br/>

## Box Model
```html
<style>
    #p1, a{
            border-width: 10px;
            border-style: solid;
            border-color: gray;
            padding:20px;
            margin:40px;  
            width:120px;  
    }
    #p2{
            border:10px solid gray;
            padding:20px;
            margin:40px;
            width:120px; 
    }
</style>
...
<p id="p1">Lorem ipsum dolor, sit amet consectetur</p>
<p id="p2">Lorem ipsum dolor, sit amet consectetur</p>
<a>Hello World</a>
```
![margin-padding](https://drive.google.com/uc?export=view&id=1M4ijppKu_3nNMIrvTLU7Qkpn2Xs-eo8t)

어떠한 영역을 지정하여 표시하거나 구분할 때 사용할 수 있는 CSS 속성들이다.   

+ border : 요소의 경계 지정에 사용.      
  width(두께), style(테두리 형태), color(색) 을 순서대로 작성함
    - border-width : 테두리의 두께 지정
    - border-sytle : 테두리의 형태 지정       
        (none, solid, dotted, double, inset, dashed, groove, ridge, inset, outset, hidden)
    - border-color : 테두리의 색 지정
+ padding : 내부의 content와 border 사이의 간격 지정
    - padding-left, right, top, bottom 으로 방향 지정 가능
+ margin : border 와 바깥쪽 프레임 사이의 간격 지정
    - margin-left, right, top, bottom 으로 방향 지정 가능 
+ width : 영역의 가로 길이 설정 
    + max-width, min-width : 반응형 웹에서 요소의 최대, 최소 가로길이 제한
+ height : 영역의 세로 길이 설정 
    + max-height, min-height : 반응형 웹에서 요소의 최대, 최소 가로길이 제한

max, min 옵션은 width나 height 를 무시한다.

+ border-width, style, color와 padding, margin은 여러 개의 값을 지정 가능
    + 한 개의 값 : 모든 면
    + 두 개의 값 : 세로방향 &#124; 가로방향
    + 세 개의 값 : 위 &#124; 가로방향 &#124; 아래
    + 네 개의 값 : 위 &#124; 오른쪽 &#124; 아래 &#124; 왼쪽 

인라인 요소는 width, height 속성을 완전히 무시한다.    


<br/>

## Box Sizing
```html
<style>
    #p1, #p2{
        margin:40px;
        width:200px;
        box-sizing:border-box;
    }
    #p1{border:10px solid gray;}
    #p2{border:30px solid gray;}
</style>
...
<div id="p1"> Hello</div>
<div id="p2"> Hello</div>
```

위 코드에서 p1과 p2 는 서로 같은 content 영역을 갖고 있지만, content 영역과 border 영역을 합친다면 서로 다른 박스의 크기를 갖게 된다.   

이를 하나하나 조절하여 같은 크기로 만드는 것은 힘든 일이므로, box-sizing 속성을 이용한다.   

+ box-sizing: 해당 요소를 지정된 옵션에 맞게 조절한다.
    - content-box : 기본 크기 결정법을 사용함. content 영역만 고려함
    - border-box : 테두리와 안쪽 여백의 크기도 요소의 크기로 고려함

<br/>

## Margin Overlap
```html
<style>
    h1{
        border:1px solid red;
        margin:100px;
    }
    #parent{
            border:1px solid tomato;
            margin-top:100px;
        }
    #child{
            background-color:red;
            margin-top:50px;
    }
</style>
...
<h1>Hello 1</h1>
<h1>Hello 2</h1>

<div id="parent">
    <div id="child"> Hello World</div>
</div>
```

마진 곂침이란 두 요소에 주어진 마진 값이 위치에 따라 합산되어 더 큰 마진이 일어나지 않는 현상을 의미한다.     

![marginoverlap1](https://drive.google.com/uc?export=view&id=1gOvcvODImH8-mn8LdrVATZSM0f2ID5tl)

두 &lt;h1&gt; 태그에는 margin이 40px 들어가 있지만, Hello1과 Hello2의 사이 크기는 40+40px 이 아닌 40px 으로 유지된다. 여기서 둘 중 하나에 40px 이상의 마진을 설정하게 되면 두 Hello 사이는 더 멀어진다.   

![marginoverlap2](https://drive.google.com/uc?export=view&id=1Lf0U-PRBmTmNYh5LL9972llLsT4_MsCp)     

id가 parent인 &lt;div&gt;는 현재 100px 의 상단 마진을 갖고 있지만, 이는 parent의 border 속성을 지워버리면 더 이상 적용되지 않고 오직 child의 50px 마진만 적용될 것이다.   

<br/>

## Position
```html
<style>
    div{border:1px solid red;}

    #parent{ position:relative;}

    #static, #relative, #absolute, #fixed{
         background-color: black;
        color:white;
    }

    #staitc{ left:10px; top:50px;}

    #relative{
        position: relative;
        left:10px; top:50px;
    }

    #absolute{
        position: absolute;
        left:15px; top:150px;
    }

    #fixed{
        position:fixed;
        left:20px; top:150px;      
    }
</style>
...
    <div id="grand">
        grand
        <div id="parent">
            parent (position=relative)
            <div id="static">static (left=10px, top=50px)</div>
            <div id="relative">relative (left=10px, top=50px)</div>
            <div id="absolute">absolute (left=15px, top=150px)</div>
            <div id="fixed">fixed (left=20px, top=150px)</div>
        </div>
    </div>
```

![position](https://drive.google.com/uc?export=view&id=19bAeC2vC7xagCai15PpbtUZXJddSp1oR)

position 속성은 해당 요소의 위치를 어떻게 계산할 것인지를 지정한다.

+ static : 부모 요소를 기준으로 위치하며 left, top 등의 오프셋 값 변경 영향을 받지 않는다. default 값
+ relative : 부모 요소를 기준으로 오프셋 값에 영향을 받아 위치가 변경된다.    
 위치가 변경되어도 기존 위치에서 차지하는 공간은 유지된다.
+ absolute : 부모의 요소 중 static이 아닌 요소가 있다면 해당 요소를 기준으로 오프셋 값에 영향을 받아 위치가 변경된다.    
 모든 부모 요소가 static이라면 전체 페이지를 기준으로 위치가 정해진다.   
 absolute로 설정되는 순간부터 부모는 해당 요소의 자리를 고려하지 않는다.   
+ fixed : 페이지 전체를 기준으로 오프셋의 영향을 받아 위치가 변경되지만, 스크롤을 내리는 등으로 위치가 바뀌어도 지정된 위치에 고정된다.   
  오프셋 값을 지정해주지 않으면 처음 정해진 위치에 있지만,    
  오프셋 값을 변경하면 페이지 전체를 기준으로 위치가 변경된다.   


<br/>

## Flex
```html
<style>
    #container{
            background-color: powderblue;
            height:300px;
            display: flex;
            flex-direction:row;
            
    }
    .item{
        background-color: tomato;
        color: white;
        border:1px solid black;
        flex-grow:1;
    }
    .item:nth-child(2){
        flex-grow:2;
    }
</style>
...
    <div id="container">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
    </div>
```

![flex](https://drive.google.com/uc?export=view&id=1ebrZrlT_L2z2opd1EKuh-C223j2uUurE)

flex는 요소들을 배치하는 방향이나 순서, 차지하는 자리의 크기를 배정하기 위해 사용하는 속성이다.   
여러 속성이 있지만 이 속성을 div들을 담는 컨테이너에 넣을지, div에 직접 삽입할지에 대한 구분이 필요하다.    

+ display:flex : flex를 사용하기 위해 display 값을 flex로 지정한다.
+ flex-direction : 요소들의 배치 방향, 순서를 결정한다
    - row : 영역의 좌측에서 요소들을 좌측부터 순서대로 배열한다.
    - row-reverse : 영역의 우측에서 요소들을 우측부터 순서대로 배열한다.
    - column : 영역의 상단에서 요소들을 상단부터 순서대로 배열한다.
    - column-reverse : 영역의 하단에서 요소들을 하단부터 순서대로 배열한다.
+ flex-basis : 해당 요소의 크기를 지정한다. 이 크기는 flex-direction의 방향 지정에 따라 가로 혹은 세로의 길이를 결정하게 된다.   
+ flex-grow : 지정된 값 만큼의 비율을 가져간다.   
나열된 요소들 중 하나의 요소만 flex-grow 값이 지정됬다면 혼자서 큰 비중을 차지한다.   
나열된 요소들 중 두개 이상의 요소가 flex-grow 값을 가진다면,    
각 요소는 (자신의 flex-gorw값/전체 flex-grow값 합) 만큼의 크기를 가진다.
+ flex-shrink : 지정된 값 만큼의 감소 비율을 결정한다.   
이 속성은 페이지의 크기가 감소할 때 요소의 영역 크기 감소에 관련된 것이다.       
기본 값은 1이고, grow와 마찬가지로 여러 요소들에게 부여한 값을 합산하여 해당 비율만큼의 변화량을 갖는다.   
높은 flex-shrink 값을 가질수록 페이지가 작아질 때 해당 요소가 담당하는 공간 감소율도 늘어난다.   

+ flex-wrap : 요소들의 크기가 지정된 칸을 넘어가면 다음 줄로 넘어가도록 할 수 있다.
    - nowrap : 지정된 칸에 맞게 요소들의 크기가 변경된다.
    - wrap : 지정된 칸을 벗어나면 다음줄로 이동한다.
    - wrap-reverse : wrap과 유사하지만 아랫줄이 아닌 윗줄로 이동한다.

+ align-items : 요소들의 정렬 상태를 지정할 수 있다. 
    - strech : 가장 긴 요소를 기준으로 높이를 맞춘 뒤 정렬한다. 기본값
    - flex-start : 최상단에 맞춰 요소들을 정렬한다.
    - flex-end : 최하단에 맞춰 요소들을 정렬한다.
    - center : 요소들을 공간의 중앙에 맞춰 정렬한다.
    - baseline : 요소들의 텍스트를 기준으로 중앙에 맞춰 정렬한다.

+ justify-content : 요소의 가로 길이가 정해져 있을 때, 가로 기준의 정렬 상태를 지정할 수 있다.
    - flex-start : 좌측으로 붙여서 정렬한다.
    - flex-end : 우측으로 붙여서 정렬한다.
    - space-between : 첫 아이템은 좌측 끝, 마지막 아이템은 우측 끝에 붙고 나머지 요수들은 고르게 정렬된다.
    - space-around : 요소들 사이에 균등한 여백이 생긴 상태로 정렬된다.
    - center : 요소들을 중앙에 정렬한다. 

위의 설명 및 작성하지 않은 속성들의 예시를 볼 수 있는 예시이다 : 
<br/>

<iframe allowfullscreen="true" allowtransparency="true" frameborder="no" height="865" scrolling="no" src="//codepen.io/enxaneta/embed/preview/adLPwv/?height=865&amp;theme-id=light&amp;default-tab=result&amp;embed-version=2" style="width: 100%;">See the Pen &amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;lt;a data-cke-saved-href=&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;#39;http://codepen.io/enxaneta/pen/adLPwv/&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;#39; href=&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;#39;http://codepen.io/enxaneta/pen/adLPwv/&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;#39;&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;gt;Flexbox playground&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;lt;/a&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;gt; by Gabi (&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;lt;a data-cke-saved-href=&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;#39;http://codepen.io/enxaneta&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;#39; href=&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;#39;http://codepen.io/enxaneta&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;#39;&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;gt;@enxaneta&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;lt;/a&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;gt;) on &amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;lt;a data-cke-saved-href=&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;#39;http://codepen.io&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;#39; href=&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;#39;http://codepen.io&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;#39;&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;gt;CodePen&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;lt;/a&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;gt;.</iframe>



<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/4>_   
