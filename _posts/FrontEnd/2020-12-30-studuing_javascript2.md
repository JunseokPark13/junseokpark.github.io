---
title: '[Javascript] Javascript 정리 - 2'
author: Bandito
date: 2020-12-30 20:40:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# Javascript 정리 - 2

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [Arguments](#arguments)



<br/>

## Arguments
***
```html
<script>
 function sum(){
    var i, _sum = 0;    
    for(i = 0; i < arguments.length; i++){
        document.write(i+' : '+arguments[i]+'<br />');
        _sum += arguments[i];
    }   
    return _sum;
}
document.write('result : ' + sum(1,2,3,4));   
</script>
```

자바스크립트는 함수의 매개변수를 받는 측면에서 관대한 편이다.   
위 코드에서 sum 함수는 지정된 매개변수가 없지만, 인자를 받는다고 해서 오류가 발생하지는 않는다.   

자바스크립트의 함수에는 arguments 라는 특수한 배열에 존재한다. 사실은 배열이 아니고 객체이지만, 이는 배열과 유사하게 사용된다.     

arguments 는 함수가 인자로 받은 값들을 저장하는 역할을 수행한다.   
이를 통해 매개변수의 수가 정확하게 정해지지 않은 함수를 구현하거나, 전달된 인자의 개수에 따라 서로 다른 처리를 하는 함수를 구현할 수 있다.   

```html
<script>
function func(arg1, arg2){
    console.log(
        'func.length', func.length,
        'arguments', arguments.length
    );
}
</script>
```

위와 같은 코드에서 함수명.length 는 함수가 받기로 한 인자의 수, arguments.length 는 함수가 실제로 받은 인자의 수를 구할 수 있다.


<br/><br/><br/>
추후 추가 포스팅 예정 

<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/1375>_   
