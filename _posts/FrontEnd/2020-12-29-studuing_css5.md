---
title: '[CSS] CSS 정리 - 5'
author: Bandito
date: 2020-12-29 14:00:00 +0900
categories: [Study, CSS]
tags: [CSS, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# CSS 정리 - 5

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [Link Import](#link-import)
    - [코드 경량화](#코드-경량화-minify)
    - [Preprocessor](#preprocessor)



<br/>

## Link Import
***
```html
<link rel="stylesheet" href="파일명.css">
<style>
    @import "파일명.css";
    @import url("파일명.css");
</style>
```

그 동안 태그에 직접 삽입하거나 &lt;style&gt; 태그 내에 작성하던 css 속성들을 별도의 css명 확장자를 가진 파일에 작성하고 이를 불러오는 방식으로 적용하는 것을 의미한다.   

&lt;link&gt; 태그를 활용하거나 &lt;style&gt; 태그 내에 @import 를 통해 원하는 css 파일을 불러올 수 있다.   

또한 css 파일에서 @import "파일명.css"로 다른 css 파일의 내용을 가져올 수도 있다.   

이러한 link import는 동일한 css 양식을 가지는 html 코드에서 중복성을 줄이고 하나의 css 파일 수정으로 여러 html에 같은 수정 효과를 줄 수 있으며, 페이지 제공자와 사용자의 재사용성을 높이는데 기여한다.  


<br/>

## 코드 경량화 (minify)
***
css 코드의 크기가 커질수록 전송하고 받는 시간이 길어지기 때문에 이를 경량화할 필요성이 있다.    
웹 페이지는 수많은 사람들이 사용하므로 조금만 경량화를 하더라도 큰 이득을 볼 수 있는 경우가 많을 것이다.   

[clean-css online](http://adamburgess.github.io/clean-css-online/){:target="_blank"}에서 자신이 경량화하고자 하는 코드를 넣으면 불필요한 부분을 삭제하고 띄어쓰기 밎 줄맞춤을 삭제하여 전체적인 코드 길이를 줄여준다.    

또한 Node.js를 사용하여 [clean-css github](https://github.com/jakubpawlowicz/clean-css){:target="_blank"}를 설치하고 원하는 css 파일을 경량화된 버전의 파일로 만들어주는 명령어를 사용할 수도 있다.   

css 파일을 보면 파일명.css 와 파일명.min.css 파일로 나뉘어 있는 경우가 있는데, min이 들어간 파일은 경량화를 마친 css 파일이라고 보면 된다.   

<br/>

## Preprocessor
***

CSS 는 필수적이지만 CSS의 코드 작성 방식이 때로는 비효율적일 수 있다.    
이를 어느정도 해소하기 위하여 별도로 만들어진 언어를 사용하여 코드를 작성하면 이를 CSS로 변환시켜주는 도구들이 생겨났다.   

[less](http://lesscss.org/){:target="_blank"},    
[Sass](https://sass-lang.com/){:target="_blank"},     
[stylus](https://stylus-lang.com/){:target="_blank"}   

위 사이트들은 CSS preprocessor 에 대해 소개하고 설명하는 사이트들이다.   대부분 Node.js의 설치를 필요로 하며, 각 언어에 대한 프로그램을 설치하고 문법에 맞게 코드를 작성하면 이를 손쉽게 CSS 코드로 변경시켜 저장해준다.   

이는 보다 효율적으로 CSS 를 작성할 수 있게 만들어 주는 좋은 도구들이다.   



<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/4>_   
