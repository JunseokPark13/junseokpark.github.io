---
title: '[Javascript] Call & Apply & Bind'
author: Bandito
date: 2021-02-01 15:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, FrontEnd, dictionary]
comment: true
description: 'asdsadasd'
---

# 함수를 호출하는 방법
***

함수를 호출하는 방법은 다음과 같은 방법들이 있다.

```javascript
 function printLog(a,b,c){
   console.log(a + b + c);
 }
 
 printLog(1,2,3);
 printLog.call(null, 1,2,3);
 printLog.apply(null, [1,2,3]);
 let a = printLog.bind(null);
 a(1,2,3);

```

위 방법들은 서로 다른 호출 방식을 사용하지만 같은 결과를 보여준다.     

단순히 함수 명 뒤에 () 을 붙여 인자를 넘겨주는 방법이 일반적이지만, 다른 방법들은 어떤 차이가 있는지 알아보자.




<br/>

# call
***

call 메서드는 주어진 this 값 및 각각 전달된 인수와 함께 함수를 호출한다.

<br/>

### 구문 
***
> func.call(thisArg[, arg1[, arg2[, ...]]])


+ thisArg : func 호출에 제공되는 this의 값
  - arg1, arg2, ... : 객체를 위한 인수 

<br/>

### 예시 

```javascript
let user1 = { name : 'A' };
let user2 = {
  name : 'B',
  work : function() { 
    console.log(this.name + ' is working');
  }
};

user2.work(); // B is working
user2.work.call(user1); // A is working
```

위 예제에서 user2.work() 은 자신의 name 인 B 를 갖고 로그를 출력하지만    
user2.work.call(user1) 은 user1 의 name 인 A 를 출력하는 것을 볼 수 있다.   

이는 call 메서드를 통해 첫 번째 인자로 넣은 객체인 user1 을 this 로 사용한 것이다. 

<br/>

# apply
***

apply 메서드는 주어진 thus 값과 배열 (또는 유사 배열 객체) 로 제공되는 arguments 로 함수를 호출한다.

<br/>

### 구문 
***
> func.apply(thisArg, [argsArray])


+ thisArg : func 호출에 제공되는 this의 값
  - argsArray : func 이 호출되어야 하는 인수를 지정하는 유사 배열 객체

<br/>

### 예시 

```javascript
let ary1 = {
  name : 'Array1'
}
let ary2 = {
  name : 'Array2',
  count : function(a,b,c){
    console.log(this.name +' sum is ', a+b+c);
  }
}
ary2.count(1,2,3);               // Array2 sum is  6
ary2.count.call(ary1,1,2,3);     // Array1 sum is  6
ary2.count.apply(ary1, [1,2,3]); // Array2 sum is  6
```

위 코드에서 ary2 객체가 가진 count 함수는 a, b, c 3가지의 매개변수를 받는다.    
call 을 사용하면 ary1 의 name 을 통해 값을 출력하고, apply 또한 같은 결과를 보여주고 있다.   

이처럼 call 과 apply 의 차이는 thisArg 외의 func 에 삽입할 인자에 대해서 단일 값으로 삽입하는지와 배열(혹은 유사 배열 객체)로 삽입하는지의 차이라고 할 수 있다.

<br/>

# bind
***

bind 메서드가 호출되면 새로운 함수를 생성한다. 첫 번째 인자로 this 키워드를 설정하고, 이어지는 인자들은 바인드된 함수의 인수에 제공된다.

<br/>

### 구문 
***
> func.bind(thisArg[, arg1[, arg2[, ...]]])


+ thisArg : func 호출에 제공되는 this의 값
  - arg1, arg2, ... : 객체를 위한 인수 

<br/>

### 예시 

```javascript
let user1 = { name : 'A' };
let user2 = {
  name : 'B',
  work : function() { 
    console.log(this.name + ' is working');
  }
};

user2.work(); // B is working
let user1Work = user2.work.bind(user1);
user1Work();  // A is working
```

bind 또한 call 과 apply 와 유사하게 인자로 this 를 바꾸지만, 호출하지는 않고 해당 값을 반환한다.


<br/>

***

call, apply, bind 모두 첫 번째 인자로 받는 thisArg 를 통해 객체의 this 를 변경하지만, 이 값을 받지 않는다면 this 는 자동으로 전역 객체를 지정하게 된다.    

이는 arguments 객체를 배열처럼 사용하는 방법에 사용될 수 있다.    

arguments 는 각 함수들이 갖고 있는 유사 배열로, 함수가 받은 인자들을 저장한다.   

배열이 아닌 만큼 arguments 에 대해서는 join, slice 등의 배열 메서드를 사용할 수 없다. 이는 다음과 같이 해결이 가능하다.

```javascript
function joinArray(a, b, c){
  console.log(arguments);
  // -> Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
  //console.log(arguments.join());
  // -> Uncaught TypeError: arguments.join is not a function
  console.log(Array.prototype.join.call(arguments));
  // -> 1,2,3
}

joinArray(1,2,3);
```

단순히 arguments 에 join 메서드를 사용하면 오류를 출력하지만, call 을 사용하면 해결할 수 있는 것을 볼 수 있다.


<br/><br/>

### 참고 자료
+ [MDN - Function.prototype.call()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/call){:target="_blank"}
+ [MDN - Function.prototype.apply()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/apply){:target="_blank"}
+ [MDN - Function.prototype.bind()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind){:target="_blank"}
+ [Poiemaweb - this](https://poiemaweb.com/js-this){:target="_blank"}