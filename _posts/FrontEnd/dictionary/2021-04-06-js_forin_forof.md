---
title: '[Javascript] for..in 과 for..of 의 차이'
author: Bandito
date: 2021-04-06 18:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# for..in 과 for..of 

![js_logo](https://drive.google.com/uc?export=view&id=1NEwhuE1d6XOGETj-36A1SGONtc9Byzh4){: width="40%" height="40%"}

<br/>

자바스크립트에서는 반복문을 위해 for 문을 사용할 수 있다. 일반적으로 사용되는 방식을 써도 문제는 없지만, ES6 에서는 다음과 같은 방법도 사용할 수 있다.

1. for...of : 반복 가능한 객체 (Array, Map, Set, String 등) 에 대해 사용할 수 있는 반복문
2. for...in : 열거 가능한 속성들에 대해 사용할 수 있는 반복문

이렇게만 보면 무슨 차이인지 제대로 감이 오지 않는다.. 몇 가지 예시를 들어 확인해보자.   

```javascript
let ary1 = [0, 1, 2];
let ary2 = [2, 4, 6];

let obj = {a : 0, b : 1, c : 2};
```

위와 같은 배열과 객체를 선언했다. 이를 콘솔에서 뜯어보면 다음과 같은 차이를 볼 수 있다.   

![ary_obj_diff](https://drive.google.com/uc?export=view&id=1EztwvygIF5v1A_pckNRP9dIEjoZtZpXr)


다음과 같이 ary1 에는 Symbol(Symbol.iterator) 라는 속성이 존재하지만, obj 에는 그런 속성이 없다. MDN 의 공식 문서를 보면 for...of 의 경우 Symbol.iterator 속성이 있는 컬렉션 요소만 반복이 가능하다고 한다.     

그럼 이번에는 직접 위 값들을 반복문으로 돌려보자    

<br/>

![forin_ary](https://drive.google.com/uc?export=view&id=1nJ_b8A-wPmnO-3RZPnxTe5VZMBXwsmlH)


배열의 인덱스와 해당 값을 출력하는 for...in 문을 사용하였다. 우리가 예상했던 것 처럼 인덱스와 해당 인덱스의 값을 정상적으로 출력하고 있다.    

![forin_obj](https://drive.google.com/uc?export=view&id=1tuAJ_oB7_x7egbr_U-1J8hwhaLWQ5KA3)


객체의 경우에도 for...in 문에서는 정상적인 출력이 이루어지고 있다.    


![forof_ary](https://drive.google.com/uc?export=view&id=1ijTgHqmWrjiZFDissp-f9ROEIaYWaWig)


배열을 for...of 문으로 이전과 똑같이 출력하려고 했으나, for...in 과는 다른 방식으로 출력된다.    
이는 for...of 문에서는 i 에 담기는 것이 인덱스가 아닌 컬렉션의 값이기 때문이다.   

![forof_obj](https://drive.google.com/uc?export=view&id=1mwpGpBQgwwzjH8rR8cTOegIGgwC36LGc)


Symbol.iterator 속성이 존재하지 않는 obj 는 for...of 문으로 출력할 수 없는 것을 볼 수 있다.   

<br/>

이 부분까지만 본다면 굳이 for...of 문을 사용할 필요가 있을까 싶다. 하지만 for...in 과 for...of 는 "반복하는 대상에 대한 차이점" 이 있다.   

for...in 은 iterable object 라면 모두 반복할 수 있는 대상이 되고,
for...of 는 iterable object 이지만, prototype chain 에 의한 iterable 은 반복 대상이 되지 않는다. 다음 예시를 보자.    

![protochain_iter](https://drive.google.com/uc?export=view&id=1Z7HYKAdiwTHyxC-xBQJo8ArVhN-xZZtf)


임의로 Array 의 프로토타입에 fc 라는 함수를 추가하였다.    

이를 for...in 으로 ary1 를 출력한다면 Array 에는 fc 라는 함수가 모든 Array 에 추가되었기 때문에 fc 까지도 출력한다.    

하지만 for...of 로 ary1 를 출력한다면, 여기서는 prototype chain 에 의한 itrable 은 고려하지 않기 때문에 순수하게 ary1 의 값들만 나오게 된다.    

<br/>

***

뭔가 수박 겉핥기 식으로 알고 넘어가는 것 같긴 한데.. 당장 궁금했던 for...in 과 for...of 의 차이는 잘 알 수 있었다. 이렇게 궁금한 것은 바로 찾아보고 기록을 남겨야 기억에 잘 남는 것 같다.



### 참고 자료
+ [MDN - for...of](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of){:target="_blank"}
+ [MDN - for...in](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...in){:target="_blank"}
