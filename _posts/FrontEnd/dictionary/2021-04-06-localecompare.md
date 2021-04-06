---
title: '[Javascript] localeCompare'
author: Bandito
date: 2021-04-06 22:30:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# localeCompare
***

localeCompare 메서드는 기준 문자열과 비교했을 때 비교 대상 문자열이 정렬상 전에 오는지, 후에 오는지 혹은 같은 순서에 배치되는지를 알려주는 숫자를 리턴한다.

<br/>

### 구문 
> referenceStr.localeCompare(compareString[, locales[, options]])

+ referenceStr : 비교 대상 문자열 a
+ compareString : 비교 대상 문자열 b

<br/>

### 예시 

```javascript
var str1 = "ABC";
var str2 = "ACD";

console.log(str1.localeCompare(str2)); // -1
console.log(str1.localeCompare(str1)); // 0
console.log(str2.localeCompare(str1)); // 1
```



### 참고 자료
+ [MDN - String.prototype.localeCompare()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare){:target="_blank"}

