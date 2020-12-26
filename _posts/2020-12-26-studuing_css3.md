---
title: '[CSS] CSS 정리 - 3'
author: Bandito
date: 2020-12-26 22:10:00 +0900
categories: [Study, CSS]
tags: [CSS, HTML, FrontEnd]
toc: false
comment: true
---

# CSS 정리 - 3

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [inline & block](#inline--block)


<br/>
## inline & block
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
## Box Model
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
    



내일 추가작성 예정...


<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/4>_   
