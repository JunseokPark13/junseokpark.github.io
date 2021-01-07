---
title: '[Javascript] Javascript 정리 - 6'
author: Bandito
date: 2021-01-06 12:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# Javascript 정리 - 6

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [이벤트 - 등록](#이벤트---등록)
        + [Inline](#inline)
        + [Property Listener](#property-listener)
        + [addEventListener](#addeventlistener)
    - [이벤트 전파 (버블링&캡처링)](#이벤트-전파-버블링캡처링)


<br/>

## 이벤트 - 등록
***

이벤트를 등록하는 방법에는 여러가지가 있다.

### Inline

```html
<input type="button" onclick="alert('Hello World ' + this.value)" value="Inline(this)" />
<input type="button" id="target" onclick="alert('Hello World ' + document.getElementById('target').value)" value="Inline(id)" />  
```

&lt;script&gt; 부분을 사용하지 않고 태그의 속성에 직접 사용하고자 하는 이벤트를 입력하는 방식이다. 자기 자신의 id를 지정하고 이를 지목하여 값을 받아올 수도 있지만, 간편하게 this 를 활용하는 것이 좋다.   

인라인 방식은 이벤트의 소재를 파악하는 것은 편리하지만, HTML와 javascript가 혼재된 방식이므로 바람직하지 않고, 이벤트의 코드가 길어지면 코드가 난잡해질 수 있다.   


### Property Listener

```html
<input type="button" id="target" value="Property Listner" />
<script>
    var t = document.getElementById('target');
    t.onclick = function (event) {
        var event = event || window.event;
        var target = event.target || event.srcElement;
        alert('Hello world, ' + target.value)
    }
</script>
```

프로퍼티 리스너 방식은 이벤트 대상에 해당하는 객체의 프로퍼티로 이벤트를 등록하는 방식이다. HTML과 javascript를 분리할 수 있다.   

객체를 지정하고 타겟 객체가 어떠한 동작(onclick 등)을 실행했을 때 어떤 이벤트가 발생할 것인지를 작성한다. 또한 event 인자를 통해 객체의 값을 받아올 수 있다.   

ie8 이하 버전에서는 이벤트 객체를 핸들러의 인자가 아닌 전역객체의 event 프로퍼티로 제공하고 target 프로퍼티도 제공하지 않으므로 event 인자는 window.event, event.target 은 event.srcElement 로 대신해주어야 정상적으로 동작한다.    


### addEventListener 

```html
<input type="button" id="target" value="button" />
<script>
    var t = document.getElementById('target');
    if(t.addEventListener){
        t.addEventListener('click', function(event){
        alert('Hello world, '+event.target.value);
    });
    } else if(t.attachEvent){
        t.attachEvent('onclick', function(event){
        alert('Hello world, '+event.target.value);
    });
    }
    
</script>
```

addEventListenr 는 이벤트를 등록하는 가장 권장되는 방식이다. 여러 개의 이벤트를 하나의 객체에 등록하거나, 하나의 이벤트를 여러 객체에 등록할 수 있다는 점이 중요한 장점으로 작용한다.

이 또한 ie8 이하 버전에서는 호환되지 않으므로 attachEvent 라는 메소드를 사용하여야 한다. 


<br/>

## 이벤트 전파 (버블링&캡처링)
***
```html
<html>
    <body>
        <fieldset>
            <legend>Event Propagation</legend>
            <input type="button" id="target" value="target" />
        </fieldset>
    </body>

    <script>
        function handler(event){
            var phases = ['capturing', 'target', 'bubbling'];
            console.log(event.target.nodeName, this.nodeName, phases[event.eventPhase-1]);
        }
        document.getElementById('target').addEventListener('click', handler, true);
        document.querySelector('fieldset').addEventListener('click', handler, true);
        document.querySelector('body').addEventListener('click', handler, true);
        document.querySelector('html').addEventListener('click', handler, true);
    </script>
</html>
```

![capturebubble](https://drive.google.com/uc?export=view&id=1HccouNeqv-nKhys0YtPknY01sc6olaYj)

CSS 를 적용한 코드는 위의 사진과 같다.   

우리는 &lt;input&gt; 의 버튼을 눌렀다고 생각할 수 있지만, input 은 fieldset, body, html 내부에 있는 태그이다. input을 눌렀다는 것은 상위의 모든 부모 태그를 누른 것과 같다고 할 수 있다.   

위 코드에서는 input 부터 시작하여 html 까지 모두 이벤트 리스너가 부착되어 있다. 이렇게 중첩된 태그들에 이벤트가 등록되어 있을 때 이벤트가 동작하는 순서에 따라 Capturing 과 Bubbling 으로 나뉘게 된다. 

위 코드는 태그를 눌렀을 때 이벤트가 처음 눌린 태그, 발생하고 있는 태그, 방식 구분 의 형태로 로그를 출력한다.   

```console
INPUT HTML capturing
INPUT BODY capturing
INPUT FIELDSET capturing
INPUT INPUT target
```

이벤트 리스너의 마지막 인자를 true 로 했을 때는 capturing 방식으로 동작한다.    
capturing 의 경우, 가장 바깥쪽 요소부터 이벤트를 발생시켜 마지막에는 처음 이벤트가 눌린 태그로 향하는 부모-&gt;자식 순서 방식이다. 이 방식은 낮은 버전의 ie 에서는 작동하지 않아 많이 사용되지 않는다.   


```console
INPUT INPUT target
INPUT FIELDSET bubbling
INPUT BODY bubbling
INPUT HTML bubbling
```

이벤트 리스너의 마지막 인자를 false 로 했을 때는 bubbling 방식으로 동작한다. 
bubbling의 경우 처음 이벤트가 눌린 요소부터 이벤트를 발생시켜 마지막에는 가장 바깥쪽의 태그로 향하는 자식-&gt;부모 순서 방식이다. 

```html
<script>
    function stophandler(event){
        var phases = ['capturing', 'target', 'bubbling'];
        console.log(event.target.nodeName, this.nodeName, phases[event.eventPhase-1]);
        event.stopPropagation();
    }    
</script>
```

만약 계속 이벤트가 전파되는 것이 아닌 특정 위치에서 멈추게 하고 싶다면 위 코드와 같이 event.stopPropagation() 이 포함된 함수를 작성하고 멈출 태그의 이벤트 리스너에서 handler 대신 사용하면 된다.

<br/>

## 기본 동작 취소
***
```html
<label>prevent event on</label><input type="checkbox" id="prevent" , name="eventprevent">
<a href="../index.html" onclick="if(document.getElementById('prevent').checked) return false;">Go to index</a>  
<a href="../index.html" id="a">Go to index</a>
<a href="../index.html" id="a2">Go to index</a>
<script>
    document.querySelector('#a').onclick = function(event){
        if(document.getElementById('prevent').checked) 
            return false;
    }
    function evenTOff(event){
        if(document.getElementById('prevent').checked){
            event.preventDefault();
        }
    }
    document.querySelector('#a2').addEventListener('click', evenTOff)
</script>
```

웹 브라우저의 구성요소들은 각각 기본적인 동작 방법을 갖고있다. a 태그를 누르면 href 속성의 url로 이동하거나, 폼에서 submit을 누르면 데이터가 전송되는 등의 동작이 이것이다.    

이는 위의 코드처럼 특정 방법으로 동작하지 않게 할 수 있다.  
위의 코드는 체크박스를 체크(true)하면 아래의 a 태그들을 눌러도 동작하지 않게 작성되었다.   

Inline 방식의 경우 onclick의 값을 false 로 하여 동작을 취소할 수 있다.      
Property 방식의 경우 Inline과 유사하지만 동작 코드를 분리하여 작성할 수 있다.   
addEventListener 방식의 경우 해당 객체의 event 메소드 중 preventDefualt()를 사용하여 동작을 취소할 수 있다.   



<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/1375>_   
