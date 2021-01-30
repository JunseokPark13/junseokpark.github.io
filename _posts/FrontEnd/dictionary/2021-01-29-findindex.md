---
title: '[Javascript] FindIndex'
author: Bandito
date: 2021-01-29 18:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd, dictionary]
comment: true
description: 'asdsadasd'
---

# findIndex
***

findIndex 메서드는 주어진 판별함수를 만족하는 배열의 첫 번째 요소에 대한 인덱스를 반환한다. 만족하는 요소가 없다면 -1을 반환한다.


<br/>

### 구문 
> arr.findIndex(callback(element[, index[, array]])[, thisArg])

+ callback : 3개의 인수를 취하여 배열의 각 값에 대해 실행할 함수이다.
    - element : 배열에서 처리중인 현재 요소
    - index : 배열에서 처리중인 현재 요소의 인덱스
    - array : findIndex 함수가 호출된 배열

<br/>

### 예시 

```javascript
const ary = [[1,2], [3,4], [5,6]];
const a = [3,4];
const b = [5,6];
ary.findIndex(x=>{
    for(let i = 0; i<x.length; i++){
        if(x[i]!==a[i]) return false;
    }
    return true;
});                                  // 1
ary.findIndex(x=>{
    for(let i = 0; i<x.length; i++){
        if(x[i]!==b[i]) return false;
    }
    return true;                     // 2
});
```





<br/><br/>

### 참고 자료
+ [MDN - Array.prototype.findIndex()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex){:target="_blank"}