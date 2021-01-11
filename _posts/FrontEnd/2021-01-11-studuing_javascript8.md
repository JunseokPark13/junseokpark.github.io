---
title: '[Javascript] Javascript 정리 - 8'
author: Bandito
date: 2021-01-11 12:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# Javascript 정리 - 8

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [Constructor](#constructor)
    - [Prototype](#prototype)
    - [Class](#class)
    - [\_\_proto\_\_](#proto)
    - [Call & Bind](#call--bind)
        + [Call](#call)
        + [Bind](#bind)
    - [Prototype vs \_\_proto\_\_](#prototype-vs-proto)


<br/>

## Constructor
***

같은 형태를 가진 객체를 여러개 생성할 때 사용할 수 있는 방식이다.   
어떠한 함수에 대하여 새로운 객체를 생성할 때 <code>var i = new function()</code> 과 같은 형태를 쓰게 되고, 이를 생성자라 부른다. 

```javascript
function alphabet(name, first, second, third){
    this.name=name,
    this.first=first,
    this.second=second,
    this.third=third,
    this.sum = function(){
        return this.first + this.second + this.third;
    }
}

var a = new alphabet('a',30,30,30);
var b = new alphabet('b',40,40,40);
```

이러한 방법을 사용하여 일종의 객체를 찍어내는 공장과 같은 형태를 구현할 수 있게 된다.

<br/>

## Prototype
***

프로토타입에 대한 설명은 이전에도 진행했던 적이 있다. 하지만 중요한 내용이므로 한번 더 정리하고 넘어가려고 한다. 


```javascript
//case 1
function Alphabet(name, first, second, third){
    this.name=name,
    this.first=first,
    this.second=second,
    this.sum = function(){
        return this.first + this.second;
    }
}
```
```javascript
// case 2
function Alphabet(name, first, second, third){
    this.name=name,
    this.first=first,
    this.second=second
}
Alphabet.prototype.sum = function(){
    return this.first + this.second;
}
```

위 두 코드를 사용하여 객체 A 를 생성하고 A.sum() 을 진행한다면 완전히 똑같은 결과를 출력할 것이다. 하지만 두 방식에는 큰 차이점이 있다.   

생성자를 통해 객체를 만드는 작업을 수행할 때, 객체는 내부의 요소들을 객체를 만들 때 마다 새롭게 만드는 과정을 진행한다.   

각 객체의 내부 변수들은 차이가 있을 수 있지만, 객체가 사용하는 기본 메소드들은 특별한 경우가 아니면 같은 내용을 갖는다.   

case 1 처럼 같은 메소드들을 객체의 수 만큼 만들어낸다는 것은 대단히 비효율적인 행동이다. 때문에 우리는 여기서 **prototype** 이라는 것을 사용한다.    

case 2 에서는 함수 내부에서 메소드를 구현하지 않고 prototype을 사용하여 메소드를 구현하였다.     
Alphabet 이라는 함수에 대하여 Alphabet.prototype 이라는 빈 객체가 어딘가에 존재하고, 모든 Alphabet 객체는 이 객체에 값을 모두 가져다 쓸 수 있다.    

그렇기 때문에 Alphabet.prototype.sum 에서만 메서드가 단 한번 생성되고, 그 이후에 몇개의 객체가 생성되던 그 객체들은 prototype 객체의 메서드를 사용하게 된다는 것이므로 기존의 방식보다 훨씬 효율적이다.   

```javascript
// case 2
function Alphabet(name, first, second, third){
    this.name=name,
    this.first=first,
    this.second=second
}
Alphabet.prototype.sum = function(){
    return this.first + this.second;
}
var a = new alphabet('a',30,30);
a.sum = function(){
    return "A : " + (this.first + this.second);
}
var b = new alphabet('b',40,40);

console.log("a.sum()", a.sum());
console.log("b.sum()", b.sum());
```
```console
a.sum() A : 60
b.sum() 80
```

또한 위 코드에서 나온 결과와 같이 특정 객체의 메소드를 수정하여 적용할 수도 있다. 이는 객체가 메소드를 사용하는 방식과 관계가 있다.   

1. 객체에 대한 sum 메소드가 호출됨
2. 객체는 자신에게 주어진 sum 메소드가 있는지 확인. 있다면 자신의 것을 사용
3. 없다면 상위 객체의 메소드를 탐색하여 사용
4. 없다면 prototype의 메소드를 탐색하여 사용 

이와 같은 순서로 진행되기 때문에, 자신에게 정의된 메소드나 변수가 있다면 자신의 것을 쓰고 없다면 prototype의 것을 사용한다.   

이러한 prototype 은 코드의 재사용성을 높이고 효율을 증가시킨다.


<br/>

## Class
***
```javascript
class Alphabet{
    constructor(name, first, second){
        this.name=name,
     this.first=first,
     this.second=second
    }
    sum(){
        return this.first + this.second;
    }
}
var a = new Alphabet('a', 10, 20);
a.sum = function(){
    return "A : " + (this.first + this.second);
}
```

ES6 에서 새롭게 추가된 class 는 객체를 만들 수 있는 일종의 틀이다.    
객체를 초기화 하기 위한 constructor 라는 메소드가 필수적으로 들어가야 한다.

외부에서 prototype 을 이용한 값을 지정해줄 수도 있지만 내부에서 선언하는 것으로 프로토타입과 같은 역할을 할 수 있다.   

기존의 방식과 마찬가지로 선언된 후 prototype 메소드를 변경하거나 추가하는 것도 가능하다.

```javascript
class AlphabetPlus extends Alphabet{
    avg(){
        return (this.first+this.second)/2;
    }
}
var b = new AlphabetPlus('b',30,40);
```

또한 자바스크립트의 class 도 다른 객체지향의 언어들 처럼 상속을 구현할 수 있다. 상속을 통하여 부모 클래스가 가진 속성들을 그대로 가져올 수 있고, 부모에서 가져온 값을 수정하거나 추가로 선언할 수도 있다. 

```javascript
class AlphabetPlus extends Alphabet{
    constructor(name, first, second, third){
        super(name,first,second);
        this.third = third;
    }
    sum(){
        return super.sum() + this.third);
    }
}
```

만약 상속받은 자식 클래스에서 새로운 매개변수를 추가로 받거나, 그에 따라 부모의 동작을 수정하고 싶다면 super 를 사용하여 부모의 생성자를 호출하거나 메서드, 변수 값을 가져올 수 있다. 

<br/>

## \_\_proto\_\_
***

prototype 은 함수만 가질 수 있었던 것과 달리 \_\_proto\_\_ 는 모든 객체가 갖고 있는 속성으로, 객체가 생성될 때 부모였던 함수의 prototype object 를 가리킨다. 

기본적으로 Object 객체를 가리키고 있으며, 이를 직접 변경하여 부모를 선택할 수도 있다.

```javascript
var superObj = {superVal:'super'};
var subObj = {subVal:'sub'};
subObj.__proto__ = superObj;

```
```javascript
var superObj = {superVal:'super'};
var subObj = Object.create(superObj);
subObj.subVal = 'sub';
```

위의 두 코드는 같은 subObj 객체를 만들어낸다. \_\_proto\_\_ 에 직접 부모가 될 대상을 지정할 수도 있지만, Object.create() 를 통해서도 생성과 동시에 지정이 가능하다. 

모든 객체들은 \_\_proto\_\_ 를 통해 연결되어 있고, 최종적으로는 최상위인 Object 객체에 도달하게 된다. 객체에서 어떠한 값을 찾기 위해 이러한 연결고리를 찾아 올라갈 수 있다.    

이렇게 \_\_proto\_\_ 속성을 통해 상위 프로토타입과 연결되어있는 형태를 프로토타입 체인이라고 한다. 


<br/>

## Call & Bind
***
```javascript
var a = {name:'Park', first:10, second:20}
var b = {name:'Kim', first:10, second:10}

function sum(){
    return this.first+this.second;
}
```

위 코드에서 a와 b, sum() 은 아무런 연관이 없다. 하지만 call 과 bind 를 사용하면 sum() 의 this 값을 변경하는 것과 같은 효과를 낼 수가 있다.      
 
<br/>

### Call
***

```javascript
console.log(sum.call(a));
console.log(sum.call(b));
```

call 메소드는 모든 함수 객체에 있는 메소드로, call 의 인자에 this 로 지정하고 싶은 객체를 넘겨서 this 를 변경 후 실행시킬 수 있다.    

```javascript
function sum(sum){
    return sum+this.first+this.second;
}
console.log(sum.call(a, 3));
console.log(sum.call(b, 5));
```

위 경우처럼 함수에 매개변수가 있는 경우에는 객체 다음의 인자에 순서대로 삽입하면 된다.   

<br/>

### Bind
***
```javascript
function sum(sum){
    return sum+this.first+this.second;
}

var aSum = sum.bind(a);
var aSum2 = sum.bind(a,9);

console.log(aSum(7));
console.log(aSum2());
```

bind 메소드 또한 모든 함수 객체에 있는 메소드로, this 로 지정하고 싶은 객체를 넘기는 것은 같지만, 이를 바로 실행하지 않고 반환하여 저장할 수 있다는 차이가 있다.   

함수에 매개변수가 있을 시 처음 bind 를 지정할 때 함께 값을 넘기거나, 이후 사용 시에 매개변수로 사용할 인자를 삽입하여 전달할 수 있다.   


<br/>

## Prototype vs \_\_proto\_\_
***

![protovproto](https://drive.google.com/uc?export=view&id=1mhS5idFZWKfD8Ukz7RayMQ-NA--1ipVv)

생활 코딩 강의에서 캡쳐한 사진이다.   

- <span style="color:#FA58D0">Person</span> 이라는 객체를 생성하면 <span style="color:#81F781">Person's prototype</span> 객체가 생겨난다. <span style="color:#FA58D0">Person</span> 프로퍼티인 prototype 은 <span style="color:#81F781">Person's prototype</span> 객체를 가리킨다.
- <span style="color:#81F781">Person's prototype</span> 의 프로퍼티인 constructor 는 <span style="color:#FA58D0">Person</span> 객체를 가리킨다.
- <code>Person.prototype.sum = function(){}</code> 으로 인해 생성된 메소드인 sum 은 <span style="color:#81F781">Person's prototype</span> 객체에 생성된다.
- <span style="color:#FA58D0">Person</span> 으로 생성한 새로운 객체인 <span style="color:#FACC2E">kim</span> 과 <span style="color:#FACC2E">lee</span> 는 <span style="color:#FA58D0">Person</span> 의 프로퍼티들을 상속받고 \_\_proto\_\_ 을 가지게 된다.
- <span style="color:#FACC2E">kim</span> 과 <span style="color:#FACC2E">lee</span> 의 \_\_proto\_\_ 은 자신을 생성한 객체인 <span style="color:#FA58D0">Person</span> prototype 이 가리키고 있는 <span style="color:#81F781">Person's prototype</span> 을 가리킨다.
- 만약 <code>kim.sum()</code> 이 호출된다면 <span style="color:#FACC2E">kim</span> 은 우선 자신이 sum 메소드를 갖고 있는지 확인하고, 없다면 \_\_proto\_\_ 이 가리키는 <span style="color:#81F781">Person's prototype</span> 이 이를 갖고있는지 확인하여 사용한다.




<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/1375>_   
_<https://opentutorials.org/module/4047>_   
