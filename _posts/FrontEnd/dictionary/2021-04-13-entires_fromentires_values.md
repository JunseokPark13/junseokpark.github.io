---
title: '[Javascript] entries, fromEntries, values'
author: Bandito
date: 2021-04-13 18:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

+ 이 문서에 있는 내용들
    - [entries](#entries)
    - [fromEntries](#fromentries)
    - [values](#values)

<br/>

# entries
***

entries 메서드는 for...in와 같은 순서로 주어진 객체 자체의 enumerable 속성 [key, value] 쌍의 배열을 반환한다.   
즉, 객체의 {key : value} 를 배열의 [key, value] 형태로 반환한다.    

<br/>

### 구문 
> Object.entires(obj)

+ ojb : 객체 자체의 열거 가능한 문자열 키를 가진 속성 쌍이 반환되는 객체
+ 반환값 : 열거 가능한 문자 속성의 쌍 배열

<br/>

### 예시 

#### 일반적인 사용 
```javascript
var obj = {
    "A" : "Apple",
    "B" : "Butter",
    "C" : "Cheese"
}

var ary = Object.entries(obj);

console.log(ary[0], ary[1], ary[2]);
// ["A", "Apple"] ["B", "Butter"] ["C", "Cheese"]
```

#### 순서가 바뀌는 경우
```javascript
var obj = {
    10 : "Ten",
    "B" : "Butter",
    7 : "Seven"
}

var ary = Object.entries(obj);

console.log(ary[0], ary[1], ary[2]);
// ["7", "Seven"] ["10", "Ten"] ["B", "Butter"]
```

**key 에 숫자와 문자가 섞여있는 경우**, 숫자와 문자 순서로 구분되어 순서가 변경될 수 있다.


#### 문자열에 대한 사용
```javascript
var ary = Object.entries("ABC");

console.log(ary[0], ary[1], ary[2]);
// ["0", "A"] ["1", "B"] ["2", "C"]
```

<br/>

# fromEntries
***

fromEntires 메서드는 키값 쌍의 목록을 객체로 바꿉니다. 
즉, 객체의 [key, value] 를 배열의 {key : value} 형태로 반환한다.    

<br/>

### 구문 
> Object.fromEntires(ary)

+ obj : 반복 가능한 객체, 즉 Array, Map 또는 반복 규약을 구현한 기타 객체
+ 반환값 : 속성의 키와 값을 반복 가능한 객체에서 가져온 새로운 객체

<br/>

### 예시 

#### 일반적인 사용
```javascript
var ary = [
    ["A", "Apple"],
    ["B", "Butter"],
    ["C", "Cheese"]
];
var obj = Object.fromEntries(ary);

console.log(obj);   // {A: "Apple", B: "Butter", C: "Cheese"}
```

#### 프로퍼티의 키 값이 같을 경우
```javascript
var ary = [
    ["A", "Apple"],
    ["B", "Butter"],
    ["B", "Beef"]
];
var obj = Object.fromEntries(ary);

console.log(obj);   // {A: "Apple", B: "Beef"}
```

<br/>

# values
***

values 소드는 전달된 파라미터 객체가 가지는 (열거 가능한) 속성의 값들로 이루어진 배열을 반환한다.
즉, 객체의 {key1 : value1}, {key2 : value2}, ... 를 배열의 [value1, value2, ...] 형태로 반환한다.

<br/>

### 구문 
> Object.values(obj))

+ obj : 배열로 반환할 열거 가능한 속성을 가지는 객체
+ 반환값 : 전달된 객체의 속성 값들을 포함하는 배열

<br/>

### 예시 

#### 일반적인 사용
```javascript
var obj = {
    "A" : "Apple",
    "B" : "Butter",
    "C" : "Cheese"
}

var ary = Object.values(obj);

console.log(ary);  // ["Apple", "Butter", "Cheese"]
```

#### 순서가 바뀌는 경우
```javascript
var obj = {
    10 : "Ten",
    "B" : "Butter",
    7 : "Seven"
}

var ary = Object.values(obj);

console.log(ary); // ["Seven", "Ten", "Butter"]
```

**key 에 숫자와 문자가 섞여있는 경우**, 숫자와 문자 순서로 구분되어 순서가 변경될 수 있다.


#### 문자열에 대한 사용
```javascript
var ary = Object.values("ABC");

console.log(ary);   // ["A", "B", "C"]
```

<br/><br/>

### 참고 자료
+ [MDN - Object.entries()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/entries){:target="_blank"}
+ [MDN - Object.fromEntries()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries){:target="_blank"}
+ [MDN - Object.values()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/values){:target="_blank"}

