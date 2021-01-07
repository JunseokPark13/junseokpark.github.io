---
title: '[Javascript] Javascript 정리 - 7'
author: Bandito
date: 2021-01-07 12:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# Javascript 정리 - 7

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [이벤트 타입 - Form](#이벤트-타입--form)
        + [submit](#submit)
        + [change](#change)
        + [blur, focus](#blurfocus)
    - [문서 로딩](#문서-로딩)
    - [마우스 이벤트](#마우스-이벤트)



<br/>

## 이벤트 타입 - Form
***

&lt;form&gt; 태그는 웹 페이지에서 입력 양식을 의미한다. 태그 하위에 존재하는 &lt;input&gt; 태그들에 입력된 값들을 form 태그의 action 속성의 링크로 전달할 수 있다.     

javascript 에서는 form 태그 내의 input 태그에 대한 동작을 구분하여 이벤트를 부여할 수 있다.   

### submit 
```html
<form id="target" action="wjs_17.html">
    <label for="name">name</label>
    <input id="name" type="text" name="name" />
    <input type="submit" />
</form>
<script>
var t = document.getElementById('target');
    t.addEventListener('submit', function (event) {
        if (document.getElementById('name').value.length === 0) {
            alert('Name 필드 값이 누락되었습니다');
            event.preventDefault();
         }
    })
</script>
```

위 코드는 form 내에 텍스트를 적는 input과 제출하는 버튼 input이 존재한다. 자바 스크립트에서는 텍스트를 적는 input의 id를 조회하여 값의 길이가 0, 즉 아무 것도 적혀있지 않으면 경고 메시지를 출력하고 실행을 막게 하였다.   
여기서 addEventListener 의 첫번째 인자인 'submit' 은 form 태그에서 제출 동작이 일어났을 때 수행한다는 것을 의미한다.   

### change
```html
<p id="result"></p>
<input id="target" type="text">
<script>
    var t = document.getElementById('target');
    t.addEventListener('change', function (event) {
        document.getElementById('result').innerHTML = event.target.value;
    });
</script>
```

위 코드는 텍스트를 적는 input에 대해 첫번째 인자로 'change' 를 넣은 addEventListener 의 동작을 구현한 것이다.   
'change' 는 지정된 입력용 태그의 값이 변경되었을 때 동작하도록 하는 이벤트 타입으로, 코드에서는 input 태그에 입력된 값을 위에 존재하는 p 태그의 텍스트가 출력하도록 되어있다.   

### blur, focus
```html
<input id="target" type="text">
<script>
    var t = document.getElementById('target');
    t.addEventListener('focus', function (event) {
        alert('focus');
    });
    t.addEventListener('blur', function (event) {
        alert('blur');
    });
</script>
```

'blur' 와 'focus' 는 지정된 태그의 포커스에 따라 동작하는 이벤트 타입이다.   
지정된 요소인 input 태그를 눌러 포커스가 'focus' 의 동작이 수행되고, 다른 곳을 눌러 포커스가 사라진다면 'blur' 의 동작이 수행된다. 


<br/>

## 문서 로딩
***
```html
<head>
    <script>
        var t = document.getElementById('target');
        console.log(t);     // case 1
        window.onload = function(){
            var t = document.getElementById('target');
            console.log(t); // case 2
        }
        window.addEventListener('load',function(){
            var t = document.getElementById('target');
            console.log(t); // case 3
        });
        window.addEventListener('DOMContentLoaded',function(){
            var t = document.getElementById('target');
            console.log(t); // case 4
        }); 
    </script>
</head>
<body>
    <p id="target">Hello World</p>
</body>
```

javascript를 통하여 웹 페이지를 제어하기 위해서는 웹 페이지의 모든 요소에 대한 처리가 끝나야 한다. 그렇기에 보통 &lt;script&gt; 는 문서의 하단에 존재하지만, 이를 상단에 작성해야할 경우도 있을 수 있다.   

위 코드에서 case 1 의 경우, 문서가 완전히 로드 되기 전에 target 을 탐색하므로 t 에 대한 로그는 null로 출력되게 된다.   

case 2 와 같이 window.onload 에 삽입된 함수로 문서의 로딩이 끝난 후 로그를 출력시키면 정상적으로 출력이 가능하다. 하지만 이보다 addEventListenr를 사용하는 것이 더 좋은 방법이다.   

case 3 에서는 addEventListener 의 첫번째 인자로 'load' 를 부여하고 있다. 이는 문서 내의 모든 리소스(이미지, 스크립트)의 다운로드가 끝난 후 실행된다. 정상적으로 동작하기는 하지만, 이는 애플리케이션 구동이 너무 느려지는 부작용이 일어날 수 있다.   

case 4 에서는 addEventListener 의 첫번째 인자로 'DOMContentLoaded' 를 부여하고 있다. 이는 DOM 에 해당하는 컨텐츠가 모두 로드가 끝나면 수행하겠다는 것으로, 스크립트 작업을 할 수 있을 때 실행되기 때문에 이미지와 같은 큰 용량의 다운로드를 기다릴 필요가 없다.   
하지만 DOMContentLoaded 이벤트는 IE8 이하의 브라우저에서는 동작하지 않을 수 있다.   

<br/>

## 마우스 이벤트
***

웹 브라우저에서는 마우스와 관련한 다양한 이벤트 타입을 지원한다. 이 타입들은 addEventListener 의 첫번째 인자로 부여되어 동작을 구분할 수 있다.   

+ click : 마우스로 클릭 했을 때 발생
+ dblclick : 마우스로 더블클릭을 했을 때 발생
+ mousedown : 마우스 버튼을 누를 때 발생
+ mouseup : 마우스 버튼을 땔 때 발생
+ mousemove : 마우스를 움직일 때 발생
+ mouseover : 마우스가 요소에 진입할 때 발생
+ mouseout : 마우스가 요소에서 빠져나갈 때 발생
+ contextmenu : 컨텍스트 메뉴가 실행될 때 발생   

***

+ event.shiftKey : Shift 가 눌러진 상태인지 감지
+ event.altKey : Alt 가 눌러진 상태인지 감지
+ event.crtlKey : Ctrl 이 눌러진 상태인지 감지 

***


+ event.clientX : 마우스의 X 좌표를 반환
+ event.clientY : 마우스의 Y 좌표를 반환







<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/1375>_   
