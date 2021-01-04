---
title: '[Javascript] Javascript 정리 - 4'
author: Bandito
date: 2021-01-04 15:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# Javascript 정리 - 4

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [HTMLElement & HTMLCollection](#HTMLElement--HTMLCollection)
    - [Element API](#element-api)
        + [식별 API](#식별-api)
        + [조회 API](#조회-api)
        + [속성 API](#속성-api)
        + [Attribute vs Property](#attribute-vs-property)



<br/>

## HTMLElement & HTMLCollection
***
```html
<a id="anchor" href="../index.html">index</a>
<ul>
    <li>A</li>
    <li>B</li>
    <li id="list">C</li>
</ul>
<input type="button" id="button" value="button"/>

<script>
    var target = document.getElementsByTagName('li');
    console.log(target.constructor.name); // HTMLCollection

    var target = document.getElementById('list');
    console.log(target.constructor.name); // HTMLLIElement

    var target = document.getElementById('button');
    console.log(target.constructor.name); // HTMLInputElement

    var target = document.getElementById('anchor');
    console.log(target.constructor.name); // HTMLAchorElement
</script>
```

객체를 조회했을 때 이에 대한 구체적인 작업을 위해서는 조회한 객체가 무엇인지를 알아내고, 이에 적절한 메소드나 프로퍼티를 사용해야한다.

getElement~ 와 같은 메소드로 요소를 찾을 때, 단일 대상에 대한 결과는 HTML**Element, 복수 대상에 대한 결과는 HTMLCollection 으로 반환된다.   

단일 대상의 결과 엘리먼트 객체들은 서로 프로퍼티가 다르지만, 모두 HTMLElement의 상속을 받고 있다. 

<br/>

## Element API
***

### 식별자 API
```html
<ul>
    <li>A</li>
    <li>B</li>
    <li id="active" class="classA">C</li>
</ul>
<script>
    console.log(document.getElementById('active').tagName);

    var active = document.getElementById('active');
    console.log(active.id);
    active.id = 'deactive';
    active.id += 'abc';

    active.className = "activeC";
    active.className += "ABC";
    active.className = "active";

    console.log(active.classList.add("A"));
    console.log(active.classList.remove("A"));
    console.log(active.classList.toggle("A"));
</script>
```

Element 객체를 다루기 위한 각종 메소드들 중 식별자에 관련된 API이다.  

 + tagName : 지정한 요소의 태그 명을 반환한다. 읽기 전용 값이므로 출력만 가능하고 변경은 불가능하다.
 + id : 지정한 요소의 id 값을 반환한다. 출력이나 직접 값을 지정하여 변경, 문자열 형태를 추가할 수도 있다.
 + className : 지정한 요소의 class 값을 반환한다. id와 동일하게 출력, 변경, 추가가 가능하다.    
 여러 개의 클래스가 있다면 한번에 출력한다.
 + classList : 지정한 요소의 class 값들을 반환한다. 유사 배열 형태로 사용된다.
    - add : 원하는 class 를 추가할 수 있다.
    - remove : 원하는 class 를 삭제할 수 있다.
    - toggle : 작성한 class 가 존재한다면 삭제하고, 존재하지 않는다면 추가한다.

<br/>

### 조회 API
```html
<ul>
    <li class="marked">A</li>
    <li>B</li>
    <li id="active" class="classA">
        C
        <ul>
            <li class="marked">C-1</li>
            <li class="marked">C-2</li>
        </ul>
    </li>
</ul>
<script>
    var list = document.getElementsByClassName('marked');
    console.group('document');
    for(var i = 0; i<list.length; i++){
        console.log(list[i].textContent);
    }
    console.groupEnd();

    var list = document.getElementById('active');
    list = list.getElementsByClassName('marked');
    console.group('element');
    for(var i = 0; i<list.length; i++){
        console.log(list[i].textContent);
    }
    console.groupEnd();
</script>
```

Element 객체를 다루기 위한 각종 메소드들 중 조회에 관련된 API이다.   
document 객체에도 존재하는 getElementBy* 메소드들은 element 객체에도 존재한다.   

위 코드에서 document 를 대상으로 하는 조회 메소드는 페이지에서 해당하는 모든 요소를 지목하지만, element를 대상으로 하는 조회 메소드는 해당 대상의 하위에 있는 요소만 지목하는 차이점이 있다.   

<br/>

### 속성 API
***
```html
<a id="target" href="../index.html">Index</a>
<script>
    var t = document.getElementById('target');
    t.getAttribute('href');
    t.setAttribute('href', 'wjs_10.html');
    t.setAttribute('title','Go to Index');
    t.hasAttribute('title');
    t.removeAttribute('title');
</script>
```

Element 객체를 다루기 위한 각종 메소드들 중 속성에 관련된 API이다.   
지정된 요소의 속성을 다루기 위해 사용하는 메소드들이다.

+ getAttribute : 지정한 속성의 값을 반환한다.
+ setAttribute : 지정한 속성의 값을 변경한다. 새로운 속성과 값을 추가할 수도 있다.
+ hasAttribute : 지정한 속성을 가지고 있는지 확인한다. true, false 로 반환된다.
+ remove.Attribute : 지정한 속성을 지운다.

<br/>

### Attribute vs Property

모든 element의 HTML은 속성과 프로퍼티로 제어가 가능하다. 하지만 각 방식에 따른 차이점이 존재한다.
```html
<script>
    var target = document.getElementById('target');
    target.setAttribute('class', 'important'); // attribute 방식
    target.className = 'important'; // property 방식
</script>
```

위의 target 의 클래스를 변경하는 두 방식은 모두 같은 결과를 만든다. 프로퍼티 방식이 좀 더 간편하고 속도도 빠르지만, 실제 html 속성의 이름과 다른 이름의 메소드를 가지는 경우도 있으므로 주의해야 한다.

```html
<a id="target" href="./demo1.html">ot</a>
<script>
    var target = document.getElementById('target');
    
    console.log('target.href', target.href);
    // http://localhost/webjs/Element/attribute_api/demo1.html   
    console.log('target.getAttribute("href")', target.getAttribute("href"));
    // ./demo1.html 
</script>
```

또한 위의 코드처럼 같은 속성의 값을 가져온다 하더라도 실제 출력 값은 다를 수도 있다.    
때문에 속성과 프로퍼티의 사용법 및 반환값을 제대로 파악하고 사용하여야 한다.




<br/>

## X
***
```html
<script>
</script>
```


<br/><br/><br/>
추후 추가 포스팅 예정 

<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/1375>_   
