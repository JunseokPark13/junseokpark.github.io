---
title: '[Javascript] Javascript 정리 - 1'
author: Bandito
date: 2020-12-29 14:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# Javascript 정리 - 1

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [배열 함수](#배열-함수)




<br/>

## 배열 함수 
***
```html
<script>
    var arr = ['a', 'b', 'c', 'd', 'e'];
    arr.push('f'); // 배열의 끝에 f 추가
    arr = arr.concat(['f', 'g']) // arr과 ['f', 'g'] 결합
    arr.unshift('z') // 배열의 시작점에 z 추가 
    arr.splice(2,0,'B') // 위치 2 이후부터 0개 만큼의 원소를 지우고 B를 2번째 이후에 추가함
    arr.shift() // 첫번째 원소를 제거함
    arr.pop() // 마지막 원소를 제거함
    arr.sort() // 정렬
    arr.reverse() // 역순으로 정렬 
</script>
```

+ push : 배열의 끝에 원소 추가. 
+ concat : 기존의 배열과 인자를 결합
    - 기존의 배열을 대체하는 것이 아니므로 영구적인 변경을 원하면 예시처럼 대입을 해주어야 함
+ unshift : 배열의 시작점에 원소 추가
+ splice : 2개 혹은 3개의 인자를 받는다.
    - 2개 : 첫 번째 인자의 위치 이후부터 두 번째 인자만큼 원소를 지움
    - 3개 : 첫 번째 인자의 위치 이후부터 두 번째 인자만큼 원소를 지우고 세번째 인자를 첫 번째 인자 이후의 위치부터 추가
+ shift : 첫 번째 원소를 제거함
+ pop : 마지막 원소를 제거함
+ sort : 정렬
+ reverse : 역순으로 정렬함 

push, concat, unshift, splice 는 여러 개의 원소나 배열에 대해 수행될 수 있음 



추후 추가 포스팅 예정....


<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/1375>_   
