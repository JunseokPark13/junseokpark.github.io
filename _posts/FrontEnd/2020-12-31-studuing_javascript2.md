---
title: '[Javascript] Javascript 정리 - 2'
author: Bandito
date: 2020-12-31 16:40:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# Javascript 정리 - 2

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [Arguments](#arguments)
    - [Call & Apply](#call--apply)
    - [Inheritance & Prototype](#inheritance--prototype)



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

<br/>

## Call & Apply
***
```html
<script>
    function sum(arg1, arg2){
        return arg1 + arg2;
    }
    console.log(sum(3,5));
    console.log(sum.call(null, 3, 5));
    console.log(sum.apply(null, [3,5]));   
</script>
```

call 과 apply 는 함수를 호출하는 방법 중 하나이다.   

위의 코드와 같이 sum 이라는 함수에 대해서 아래의 세 방식은 모두 8을 로그로 출력한다.    

call 과 apply는 첫 번째 인자로 객체를 받고, 이후에는 함수에서 지정된 매개변수에 대한 값을 전달한다.    
전달된 객체는 함수 내에서 this 를 사용할 때 효과를 발휘한다.   


```html
<script>
    o1 = {val:1, val2:2, val3:3}

    function sum(arg1, arg2){
        var _sum = 0;
        for(name in this){
            _sum += this[name];
        }
        return _sum + arg1 + arg2;
    }

    console.log(sum.call(o1, 3, 5));
    console.log(sum.apply(o1, [3,5]));   
</script>
```

위 코드에서 함수 sum은 this의 값을 모두 더하는 반복문을 수행한다.   
call 과 apply 에서 첫 번째 인자로 전달된 o1이 함수 내에서 this의 값들로 사용될 수 있다.   
즉 call 이나 apply 를 사용하면 해당 함수가 전달된 객체(o1)의 메서드인 것 처럼 사용이 가능하다는 뜻이다.    

둘의 유일한 차이점은 매개변수를 넘길 때 call 은 단일 값으로 넘겨야 하고 apply는 배열 형태로 넘겨야 한다는 것이다. 


<br/>

## Inheritance & Prototype
***
```html
<script>
function Person(name){
    this.name = name;
    this.introduce = function(){
        return 'My name is '+this.name; 
    }   
}
</script>
```

```html
<script>
function Person(name){
    this.name = name;
}
Person.prototype.name=null;
Person.prototype.introduce = function(){
    return 'My name is '+this.name; 
}
</script>
```

위 두 코드의 함수 선언 방식은 같은 결과를 내는 함수를 만들지만, Person 이라는 객체를 여러개 만들어낸다고 가정하면 아래의 코드가 메모리 관점에서 훨씬 유리하다.   

위의 코드는 객체마다 속성을 만들어 내겠지만, 아래의 코드에서는 Person의 생성자를 통해 만들어지는 객체들이 prototype 이라는 object를 공유할 것이다.    

이와 같이 자바 스크립트에서 함수가 정의되면 기본적으로 생성자가 부여되고, new 를 통해 객체를 생성할 수 있게 됨과 동시에 Prototype Object 라는 것을 가지게 된다.    
이는 새로운 객체가 생성될 때 Prototype Object를 참조하여 값들을 지니게 한다.     

결국 Prototype 에 속성을 추가한다는 것은 해당 함수를 통해 만들어질 객체의 틀을 구성하는 것과 같다고 할 수 있을 것 같다.   

```html
<script>
    function Ultra(){}
    Ultra.prototype.ultraProp = true;
    
    function Super(){}
    Super.prototype = new Ultra();
    
    function Sub(){}
    Sub.prototype = new Super();
    
    var o = new Sub();
    console.log(o.ultraProp);
</script>
```

위 코드에서는 property 를 통해 상속이 이루어지는 것을 볼 수 있다.   
Sub() 은 Super() 를 상속받고, Super() 는 Ultra()를 상속받는다.    
그리고 마지막에 Sub() 을 통해 생성된 객체 o 는 true 를 콘솔에 출력한다.   

이처럼 o 가 Ultra() 의 ultraProp 에 접근 가능한 이유는 Sub() 와 Ultra() 가 prototype chain 으로 연결되어 있기 때문이다.  

1. 객체 o 에서 UltraProp 을 찾는다.
2. 없다면 Sub.prototype.ultraProp 을 찾는다.
3. 없다면 Super.prototype.ultraProp 을 찾는다.
4. 없다면 Ultra.prototype.ultraProp 을 찾는다.

이러한 관계를 prototype chain 이라고 한다.    







<br/><br/><br/>
추후 추가 포스팅 예정 

<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/1375>_   
