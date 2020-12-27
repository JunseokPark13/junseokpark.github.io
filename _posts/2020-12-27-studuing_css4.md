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





<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/4>_   
