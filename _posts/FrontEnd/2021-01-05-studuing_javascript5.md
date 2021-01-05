---
title: '[Javascript] Javascript 정리 - 5'
author: Bandito
date: 2021-01-05 12:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# Javascript 정리 - 5

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [Node API](#node-api)
        + [관계 관련 API](#관계-관련-api)
        + [종류 관련 API](#종류-관련-api)
        + [변경 관련 API](#변경-관련-api)



<br/>

## Node API
***

![nodetree](https://drive.google.com/uc?export=view&id=1AqjnvIYUlJbu7AeeOZkiSiRL0SZfWVSb)   

Node 는 DOM 에서 가장 상위의 객체이므로 모든 DOM 객체는 Node 객체를 상속받는다. 때문에 Node 객체가 가진 property 는 모든 객체가 갖게 된다.    


### 관계 관련 API

각 node 간의 관계 정보를 담고 있는 프로퍼티들이다. 

+ childNodes : 자식 노드들을 유사 배열 형태로 반환한다.
+ firstChild : 첫번째 자식 노드를 반환한다.
+ lastChild : 마지막 자식 노드를 반환한다.
+ nextSibling : 현재 노드의 다음 형제 노드를 반환한다.
+ previousSilbing : 현재 노드의 이전 형제 노드를 반환한다.
+ contains() : 주어진 인자가 노드의 자손인지 아닌지를 bool 로 반환한다.
+ parentNode : 현재 노드의 상위 부모 노드를 반환한다.

여기서 firstChild, lastChild의 경우 줄 맞춤을 위한 여백 또한 노드로 판단하므로 이를 구분하거나 다음 형제 노드를 찾아가는 식으로 명확하게 구분해야할 필요성이 있다.   

<br/>

### 종류 관련 API

각 node의 타입이나 이름에 대한 정보를 담고 있는 프로퍼티들이다.

+ nodeType : 노드의 타입을 반환한다.
+ nodeName : 노드의 이름(태그명)을 반환한다. 

```html
<script>
    for(var name in Node){
        console.Log(name, Node[name]);
    }
</script>
```
```console
ELEMENT_NODE 1 
ATTRIBUTE_NODE 2 
TEXT_NODE 3 
CDATA_SECTION_NODE 4 
ENTITY_REFERENCE_NODE 5 
ENTITY_NODE 6 
PROCESSING_INSTRUCTION_NODE 7 
COMMENT_NODE 8 
DOCUMENT_NODE 9 
DOCUMENT_TYPE_NODE 10 
DOCUMENT_FRAGMENT_NODE 11 
NOTATION_NODE 12 
DOCUMENT_POSITION_DISCONNECTED 1 
DOCUMENT_POSITION_PRECEDING 2 
DOCUMENT_POSITION_FOLLOWING 4 
DOCUMENT_POSITION_CONTAINS 8 
DOCUMENT_POSITION_CONTAINED_BY 16 
DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC 32
```

위 코드를 실행하면 이와 같은 결과가 나온다. 각 노드들인 자신만의 이름과 번호를 갖고 있으며, 이를 통해 노드를 구분할 수 있다. 

```html
<h1 id="h1">Hello World</h1>
<script>
    var h1 = document.getElementById('h1');
    console.log(h1); // <h1 id="h1">Hello World</h1>
    console.log(h1.nodeName); // "H1"
    console.log(h1.nodeType); // 1;
    console.log(h1.nodeType === Node.ELEMENT_NODE); // true;
    console.log(h1.firstChild.nodeType) // 3;
    console.log(h1.firstChild.nodeType === Node.TEXT_NODE) // true;
</script>
```

각 노드들의 이름은 대문자로 출력되며 nodeType에 대한 출력은 기본적으로 정수형이지만, 노드의 이름과 비교하여도 문제는 없다.   

<br/>

### 변경 관련 API

```html
<ul id="target">
    <li id="target2">C-1</li>
    <li>C-2</li>
    <li>C-3</li>
</ul>
<script>
    function appendNode(){
        var target = document.getElementById('target');
        var li = document.createElement('li');
        var text = document.createTextNode('C-4');
        li.appendChild(text);
        target.appendChild(li);
    }

    function insertBeforeNode(){
        var target = document.getElementById('target');
        var li = document.createElement('li');
        var text = document.createTextNode('C-0');
        li.appendChild(text);
        target.insertBefore(li, target.firstChild);
    }

    function removeNode(){
        var target=document.getElementById('target2');
        target.parentNode.removeChild(target);
    }

    function replaceNode(){
        var target = document.getElementById('target2');
        var a = document.createElement('a');
        a.setAttribute('href', '../index.html');
        a.appendChild(document.createTextNode('Go to Home'));
        target.replaceChild(a, target.firstChild);
    }
</script>
```

노드를 추가하거나 기존의 노드를 삭제, 변경하는 프로퍼티들이다. 

+ appendChild() : 인자로 받은 노드를 타겟 노드의 가장 마지막에 추가한다.
+ insertBefore() : 첫번째 인자로 받은 노드를 두번째 인자로 받은 타겟의 위치 앞에 추가한다. 두번째 인자가 null 이라면 appendChild() 처럼 동작한다.
+ removeChild() : 인자로 받은 노드를 삭제한다. 특이하게도 인자로 받은 노드의 부모 노드를 통하여 removeChild() 를 사용해주어야 한다.
+ replaceChild() : 첫번째 인자로 받은 노드를 두번째 인자로 받은 타겟을 대신하여 교체한다. 

새로운 노드를 추가할 때는 createElement를 통하여 빈 노드를 생성하고 이에 필요한 속성을 추가하거나 텍스트를 추가하는 방식으로 작성한 뒤 appendChild, insertBefore, replaceChild 등을 사용하여 적절한 위치에 배치하여야한다.   

<br/>

### 문자열 노드 제어

문자열로 자식 노드를 읽어오거나 변경할 수 있는 프로퍼티들이다.

+ innerHTML : 타겟의 내부에 대하여 태그를 포함한 HTML 값을 반환한다. 대입을 통해 값을 변경할 수도 있다.
+ outerHTML : innerHTML 처럼 태그를 포함한 HTML 값을 반환 및 변경 가능하지만, 타겟을 포함하여 처리한다.
+ innerText : HTML 코드를 제외한 문자열을 반환한다. 변경 시에는 HTML의 태그 부분을 적용하는 것이 아닌 문자열로 출력시킨다.
+ outerText : innerText와 비슷하지만, 타겟을 포함하여 처리한다.
+ insertAdjacentHTML : 타겟에 대하여 노드를 추가하되, 위치를 지정할 수 있다. HTML 태그가 포함된다면 적용된다. 인자에 따른 위치 지정은 다음 코드와 같다. 

```html
 // beforebegin
<ul id="target">
    // afterbegin
    <li>CSS</li>
    // beforeend
</ul>
// afterend
<script>
    var target = docuemnt.getElementById('target');
    target.insertAdjacentHTML(위치, '문자열');
</script>
```


<br/>

## Text 객체 
***

![texttree](https://drive.google.com/uc?export=view&id=1FL-N3xqy9LQLI2_9gN-n1VIdxx-CZmtJ)

Text 객체는 텍스트 노드에 대한 DOM 객체로, CharacterData 를 상속받는다.   
이전에도 언급했듯이, DOM 에서는 공백이나 줄바꿈 또한 텍스트 노드 취급을 한다는 점을 꼭 기억해야 한다.

+ nodeValue : 해당 노드의 값을 반환한다. 대입하여 값을 변경할 수도 있다.
+ data : nodeValue와 동일하다.
+ appendData(value) : 타겟 노드에 value 값을 추가한다.
+ deleteData(start, end) : 타겟 노드의 start 부터 end 까지의 값을 지운다.
+ insertData(start, value) : 타겟 노드의 start 부터 value 값을 추가한다.
+ replaceData(start, end, value) : 타겟 노드의 start 부터 end 까지의 값 대신 value 를 추가한다.
+ substringData(strat, end) : 타겟 노드의 start 부터 end 까지의 값을 추출하여 반환한다.





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
