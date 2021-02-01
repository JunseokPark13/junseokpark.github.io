---
title: '[Javascript] Some & Every'
author: Bandito
date: 2021-01-31 18:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, FrontEnd, dictionary]
comment: true
description: 'asdsadasd'
---

# some
***

from 메서드는 배열 안의 어떤 요소라도 주어진 판별 함수를 통과하는지 테스트한다.
빈 배열에서 호출하면 무조건 false 를 반환한다.

<br/>

### 구문 
> arr.some(callback[, thisArg])


+ callback : 각 요소를 시험할 함수
    - currentValeu : 처리할 현재 요소
    - index : 처리할 현재 요소의 인덱스
    - array : some 을 호출한 배열

<br/>

### 예시 

```javascript
let res = [2, 5, 8, 1, 4].some(function (item) {
  return item > 10;
});
console.log(res); // false

res = [12, 5, 8, 1, 4].some(function (item) {
  return item > 10;
});
console.log(res); // true
```

<br/>

# every
***

from 메서드는 배열 안의 모든 요소가 주어진 판별 함수를 통과하는지 테스트한다.
빈 배열에서 호출하면 무조건 true 를 반환한다.

<br/>

### 구문 
> arr.every(callback[, thisArg])



+ callback : 각 요소를 시험할 함수
    - currentValeu : 처리할 현재 요소
    - index : 처리할 현재 요소의 인덱스
    - array : some 을 호출한 배열

<br/>

### 예시 

```javascript
let res = [21, 15, 89, 1, 44].every(function (item) {
  return item > 10;
});
console.log(res); // false

res = [21, 15, 89, 100, 44].every(function (item) {
  return item > 10;
});
console.log(res); // true
```



<br/><br/>

### 참고 자료
+ [MDN - Array.prototype.some()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/some){:target="_blank"}
+ [MDN - Array.prototype.every()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/every){:target="_blank"}
+ [Poiemaweb - High Order Functions](https://poiemaweb.com/js-array-higher-order-function){:target="_blank"}