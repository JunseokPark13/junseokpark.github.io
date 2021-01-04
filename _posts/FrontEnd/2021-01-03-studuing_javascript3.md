---
title: '[Javascript] Javascript 정리 - 3'
author: Bandito
date: 2021-01-03 15:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# Javascript 정리 - 3

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [alert, confirm, prompt](#alert-confirm-prompt)
    - [Location](#location)
    - [Navigator](#navigator)
    - [창 제어](#창-제어)
    - [제어 대상 탐색](#제어-대상-탐색)
    


<br/>

## alert, confirm, prompt
***
```html
<script>
    function func(){
        if('Do you want to login?'){
            if(prompt('id : ') === 'ok'){
            alert('Success');
        }
            else{
            alert('Fail');
            }
        }
        else{
            alert('quit');
        }    
    }
</script>
```

웹 페이지에서 알림 창을 띄워 사용자와 상호작용 하는 기능이다.   

+ alert : 인자에 주어진 문자열을 출력한다.
+ confirm : 인자에 주어진 문자열을 출력하고 확인, 취소 버튼이 존재한다.    
    확인을 누르면 true, 취소를 누르면 false 가 반환된다.
+ prompt : 인자에 주어진 문자열을 출력하고 input 박스와 확인, 취소 버튼이 존재한다.    
    지정한 값을 올바르게 입력하고 확인을 누르면 true, 지정되지 않은 값을 입력하고 확인 버튼을 누르거나 취소를 누르면 false 가 반환된다.

<br/>

## Location
***

Location 객체는 문서의 주소와 관련된 Window 객체의 프로퍼티이다. 이를 이용하여 URL을 변경하거나, 문서의 위치와 관련된 다양한 정보를 얻을 수 있다. 

+ location.href : 현재 페이지의 주소를 반환한다. 다른 주소 값을 대입하면 해당 주소로 이동하는 코드가 된다.
    - location.toString() : 현재 페이지의 주소를 출력할 수 있다.
    - location.href = location.href 으로 새로고침을 수행할 수 있다.   
    하지만 location.reload가 더 간단한 방법이다. 
+ location.protocol : url의 프로토콜 부분을 반환한다.
+ location.host : url의 호스트 부분을 반환한다.
+ location.hostname : url의 도메인 부분을 반환한다.
+ location.port : url의 포트 번호를 반환한다.
+ location.pathname : '/' 문자 뒤의 url 경로를 반환한다.
+ location.search : '?'문자 뒤 url의 쿼리스트링을 반환한다.
+ location.hash : '#' 문자 뒤 url의 프래그먼트 식별자를 반환한다.


<br/>

## Navigator
***

Navigator 객체는 브라우저와 관련된 정보를 담고있다. 브라우저의 버전, 정보, 종류 등에 관한 정보를 제공한다. 주로 호환성 문제를 위해 사용한다.   

+ navigator.appCodeName	: 브라우저의 코드명을 반환한다.
+ navigator.appName	: 브라우저의 이름을 반환한다.   
    Microsoft Internet Explorer 는 IE   
    파이어폭스, 크롬 등은 Nescape 로 반환된다.
+ navigator.appVersion : 브라우저의 버전을 반환한다.
+ navigator.cookieEnabled : 브라우저의 쿠키 사용 가능 여부를 반환한다.
+ navigator.language : 브라우저에서 사용되는 언어를 반환한다.
+ navigator.onLine : 브라우저가 온라인인지 여부를 반환한다.
+ navigator.platform : 브라우저가 실행되는 플랫폼 정보를 반환한다.
+ navigator.userAgent : 브라우저와 운영체제 정보를 반환한다.


<br/>

## 창 제어
***
```html
<script>
    window.open("../index.html");
    window.open("../index.html", '_self');
    window.open("../index.html", '_blank');
    window.open("../index.html", 'ot');
    window.open("../index.html", '_blank', 'width=300, height=300');
</script>
```

window.open 메소드를 통해 새로운 창을 생성할 수 있다. 
첫 번째 인자에 접속하고자 하는 주소를 적고, 그 뒤의 인자에 새로 열릴 창에 대한 옵션을 적을 수 있다.  
+ _self : 현재 창에서 새로운 페이지를 로드한다.
+ _blank : 새로운 창에서 페이지를 로드한다.
+ ot : 새로운 창에서 페이지를 로드하지만, 이미 같은 이름의 페이지가 열려있다면 해당 페이지 창으로 이동한다.
+ 마지막 인자로 창의 width, height 를 지정할 수 있다. reasizable 이라는 값으로 창 크기 조절을 막을 수도 있지만, 현재는 제대로 작동하지 않는 경우가 더 많다.   

보통은 위와 같은 페이지 오픈 동작은 버튼이나 링크를 통해 수행하는 것이 일반적이지만, 페이지 진입 시 자동으로 창을 여는 것을 팝업이라고 한다. 버튼을 누르는 등의 사용자 인터렉션이 없이 동작하는 것은 사용자에게 보안상의 위험이 있을 수 있다.   
최근 대부분의 브라우저는 이러한 팝업을 자동으로 차단하는 기능을 가지고 있다.


```html
<input type="button" value="open" onclick="winopen();" />
<input type="text" onkeypress="winmessage(this.value)" />
<input type="button" value="close" onclick="winclose()" />
<script>
function winopen(){
    win = window.open('page.html', 'ot', 'width=300px, height=500px');
}
function winmessage(msg){
    win.document.getElementById('message').innerText=msg;
}
function winclose(){
    win.close();
}
</script>
```

위 코드에서처럼 새로 생성한 페이지에 대한 정보를 변수에 담을 수 있다.
페이지에 대한 정보를 변수에 담은 뒤, 이를 통해 새로 열린 페이지를 제어할 수 있다.


<br/>

## 제어 대상 탐색
***
```html
<ol>
    <li>A</li>
    <li>B</li>
    <li class="qclass">C</li>
    <li class="qaclass">D</li>
    <li class="qaclass">E</li>
</ol>

<ul>
    <li class="eclass">D</li>
    <li class="eclass">E</li>
    <li id="eId">F</li>
</ul>
...
<script>
    var ol = document.getElementsByTagName('ol')[0];
    var lis1 = ol.getElementsByTagName('li');
    for(var i=0; i<lis1.length; i++){
        lis1[i].style.color = 'red';
    }

    var lis2 = document.getElementsByClassName('eclass');
    for(var i=0; i<lis2.length; i++){
        lis2[i].style.color='blue';
    }
            
    var lis3 = document.getElementById('eId');
    lis3.style.color='green';

    var lis4 = document.querySelector('.qclass');
    lis4.style.color = 'white';

    var lis4 = document.querySelector('.qclass');
    lis4.style.color = 'white';

    var lis5 = document.querySelectorAll('.qaclass');
    for(var i in lis5){
        lis5[i].style.color = 'yellow';
    }
</script>
```

javascript 에서는 html의 요소를 선택하여 값을 변경할 수 있다. 이러한 제어 대상을 선택하는 것은 다음과 같은 방법들이 있다.   

+ getElementsByTagName : html 요소의 태그로 대상을 선택한다. 같은 태그가 여러개 있을 수 있으므로 이를 저장하는 변수는 NodeList 라는 유사 배열이 된다.   
+ getElementsByClassName : html 요소의 클래스로 대상을 선택한다. 이 또한 유사 배열로 저장된다.
+ getElementById : html 요소의 아이디로 대상을 선택한다. 하나의 아이디는 유일하게 사용되어야 하므로 배열이 아닌 단일 대상으로 저장된다.
+ querySelector : 특정 대상을 선택하지만 css의 선택자를 사용할 수 있다. 단일 객체를 저장한다.
+ querySelectorAll : css의 선택자를 사용하여 여러 객체를 저장할 수 있다.

어떠한 태그 내에 위치하는 내부 태그들을 선택하고 싶을때는 순서대로 메서드를 사용하여 찾아나갈 수 있다.     

jQuery 에서도 querySelector 와 유사한 사용법이 가능하다. 

```html
<script>
    $('li').css('color','red');
    $('#eId').css('color','red');
    $('.eclass').css('color','red').css('textDecoration','underline');
</script>
```

css 선택자를 사용하여 대상을 선택 가능하고, 여러 개의 옵션을 순차적으로 부여할 수도 있다.   








<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/1375>_   
