---
title: '[Javascript] Javascript 정리 - 1'
author: Bandito
date: 2020-12-29 20:35:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# Javascript 정리 - 1

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [정규 표현식](#정규-표현식)
    - [배열 함수](#배열-함수)
    - [Callback 함수](#callback-함수)
    - [클로저](#클로저)


<br/>

## 정규 표현식
***

정규 표현식은 자바스크립트 외에서도 사용할 수 있다.   

모든 정규 표현식은 &#47;정규표현식&#47; 과 같이 표현한다.   

+ <span style="color:red">^</span>word : 'word' 로 시작하는 문장을 찾음
+ word<span style="color:red">$</span> : 'word' 로 끝나는 문장을 찾음 
+ <span style="color:red">\\</span>$ : 특수문자인 $에 대해 지목함 
+ <span style="color:red">.</span> : 어떠한 문자던 지목함
    - A. : A와 한 문자가 붙어있는 단어를 지목함 (AB, AC, Ak, ....)
    - .. : 아무런 문자 2개가 붙어있는 단어를 지목함 
+ <span style="color:red">\[</span>abc<span style="color:red">\]</span> : a, b, c 를 찾음. 연결된 abc를 찾는 것이 아닌 개별 문자로 지목함
    - "ak bc ea c" 라면 a, b, c, a, c 를 찾아낸다는 것
+ \[A<span style="color:red">-</span>Z\] : A부터 Z 사이의 문자를 지목함. [] 안에 있으므로 개별 문자로 지목함 
+ \[<span style="color:red">^</span>efgk\] : e, f, g, k 를 제외한 문제를 지목함. [] 안의 ^는 부정(not)의 의미로 사용됨
    - \[^W-Z\] 라면 W, X, Y, Z 를 제외하고 지목한다는 것
+ <span style="color:red">(</span>AB\|CD\|EF<span style="color:red">)</span> : AB, CD, EF 단어를 지목함. \| 으로 단어를 구분함 
+ 수량자
    - a<span style="color:red">*</span>b : a가 0개~여러개 붙고 b로 끝나는 단어 지목
        + .* : 단어 전체를 지목하게 됨 
    - a<span style="color:red">+</span>b : a가 1개~여러개 붙고 b로 끝나는 단어 지목
        + [^ ]+ : 공백을 제외한 모든 단어 및 문자를 선택하게 됨 
    - a<span style="color:red">?</span>b : a가 0개~1개 붙고 b로 끝나는 단어 지목 
    - .<span style="color:red">{</span>5<span style="color:red">}</span> : 아무런 문자를 연속으로 5개 지목함
        + [els]{1,3} : e, l, s가 1개 이상 3개 이하로 연속 등장한 단어를 찾음
        + [a-z]{3,} : 알파벳 소문자가 3개 이상 연속으로 등장한 단어를 찾음
    - 수량자에 ? 가 붙는 경우 : ?의 의미가 달라진다. 
        + a.*? : a로 시작하지만 그 뒤엔 아무 것도 붙지 않는 단어를 지목
        + a.+? : a로 시작하지만 그 위에 단 하나의 문자만 붙는 단어를 지목
        + a.?? : a로 시작하지만 그 뒤엔 아무 것도 붙지 않는 단어를 지목
        + 이 수량자의 사용은 다음의 예시로 알 수 있다.

![greedylazy](https://drive.google.com/uc?export=view&id=1cASyILoazBPQCzQmjLI6QdkvWntABB3A)

첫 번째 케이스 처럼 div 내의 단어를 선택하고 싶을 때 ? 을 사용하지 않으면 첫 &lt;div&gt; 와 마지막 &lt;/div&gt; 를 선택하게 된다. 이러한 케이스를 Greedy Quantifier, 즉 탐욕적인 선택자라 한다.   

두 번째 케이스처럼 ?를 붙인다면 두 부분으로 나뉘어 지목되는 것을 볼 수 있다. 이러한 케이스를 Lazy Quantifier, 즉 게으른 선택자라고 한다.    

즉 수량자에 ? 를 붙인다는 것은 Greedy 혹은 Lazy의 케이스를 나눌 때라는 것을 알 수 있다.   

+ <span style="color:red">\w</span> : \[A-z0-9_\] 과 같은 의미를 가진다. 이는 즉 모든 알파벳과 숫자, _ 을 지목한다는 뜻이다. 단, 공백은 포함하지 않는다.
    - \w* : 모든 단어를 지목한다.
    - \w{5} : 문자 5개로 이루어진 단어를 지목한다.
+ <span style="color:red">\W</span> : \w의 반대 버전으로, \[^A-z0-9_\] 과 같은 의미를 가진다. 모든 공백과 \w에 속하지 않는 특수문자를 지목한다. 

+ <span style="color:red">\s</span> : 여백만을 지목한다.
+ <span style="color:red">\S</span> : 여백이 아닌 문자를 지목한다.
+ <span style="color:red">\d</span> : \[0-9\] 와 같이 모든 숫자를 지목한다.
+ <span style="color:red">\D</span> : \d와 반대로 숫자가 아닌 문자를 지목한다.
+ <span style="color:red">\b</span> : boundary, 즉 단어의 경계를 지목한다.
    - \b. : 모든 단어의 시작 문자를 지목한다.
    - .\b : 모든 단어의 종료 문자를 지목한다. 
    - \b\w+\b : 모든 단어를 지목할 수 있다. 
+ <span style="color:red">\B</span> : \b와 반대로 경계가 아닌 부분을 지목한다. 
+ \w+<span style="color:red">(?=X)</span> : 마지막에 X가 포함된 문자를 선택하되, X는 제외함

[gskinner-RegExr](https://regexr.com/){:target="_blank"} : 정규 표현식을 작성하면서 실시간으로 그 결과를 테스트 가능함    
[regexper](https://regexper.com/){:target="_blank"} : 정규 표현식을 시각화하여 보여주는 도구    


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

<br/>

## Callback 함수 
***

자바스크립트에서는 함수도 객체로 취급한다. 즉 함수도 일종의 값이라는 것이다. 
```html
<script>
    function a(){}
    var a = function(){}
</script>
```
위의 두 방식은 선언하는 방식은 다르지만 같은 함수를 생성할 수 있다. 

```html
<script>
    function cal(func, num){
        return func(num)
    }
    function increase(num){
        return num+1
    }
    function decrease(num){
        return num-1
    }
    alert(cal(increase, 1));
    alert(cal(decrease, 1));
</script>
```
또한 함수는 값이기 때문에 위와 같이 함수를 인자로 전달하는 것도 가능하다.   
이러한 자바스크립트에서의 함수의 성질을 이용하여 callback 함수라는 것을 활용이 가능하다. 

<br/>

sort 메소드는 정수 값에 대해서 제대로 정렬을 하지 못하는 문제가 있다.    

sort 는 array.sort(sortfunc) 라는 방식으로 사용하고, 여기서 sortfunc는 배열의 정렬 설정을 하는 인자이다.   

sort 메소드 내에서는 배열의 두 값에 대한 return 값에 의하여 정렬이 수행된다.   
a ,b 를 비교한다고 했을 때 a-b 가 음수이면 a&gt;b, 양수이면 a&lt;b, 0 이면 같다고 판단한다.   

```html
<script>
    function sortNumber(a,b){
        return a-b;
    }

    arr.sort(sortNumber);
</script>
```
위와 같이 수행한다면 오름차순 정렬이 되고, return 을 b-a 로 바꾸면 내림차순 정렬이 가능하다.   

이렇게 sort 메소드의 매개변수에 sortNumber와 같은 함수를 전달하여 sortNumber가 수행되는 것을 callback 이라고 한다. 
 
<br/>

## 클로저  
***

callback 함수에서도 언급했듯이 javascript 에서는 함수 안에 또 다른 함수를 선언할 수 있다. 

```html
<script>
function outter(){
    var title = 'Wow'; 
    return function(){
        alert(title);
    }
}
inner = outter();
inner();
</script>
```

위 코드를 실행시키면 경고창으로 'Wow' 라고 출력된다.   
   
5번째 줄의 alter(title)은 자신이 속한 중괄호 내에 title이라는 변수가 없다는 것을 확인하고 외부함수인 outter에서 title을 찾아 사용한다.   

일반적으로 생각하면 return 시 outter 함수의 title 변수는 함수가 종료되었으므로 이미 사라졌다고 생각할 수 있다. 이는 클로저의 독특한 특성이라고 할 수 있다.   

각 함수들은 자신이 사용할 수 변수를 체크하는 scope 라는 개념을 갖고 있다. 
1. alert이 속한 중괄호 scope 에는 사용할 수 있는 변수가 없고   
2. 외부 함수인 outter의 scope 에는 var 자료형의 title 변수가 존재한다.

내부에 있는 함수들은 자신이 사용할려는 변수가 자신의 scope에 존재하지 않는다면 바깥 외부함수로 탐지 scope 를 변경하면서 사용할려는 변수가 있는지를 확인하는 과정을 거친다.   

이러한 scope 는 함수가 종료되어도 참조할 수 있는 상태로 남아있기 때문에 outter의 return 이후에 실행되는 alert 이라 하더라도 outter의 title을 찾아 사용할 수 있는 것이다.   

```html
<script>
function factory_movie(title){
    return {
        get_title : function (){
            return title;
        },
        set_title : function(_title){
            title = _title
        }
    }
}
ghost = factory_movie('Ghost in the shell');
matrix = factory_movie('Matrix');
</script>
```

클로저는 위와 같은 코드로 사용할 수도 있다.   

factory_movie 의 메소드인 get_title은 title을 반환, set_title은 인자를 통해 title을 변경하는 역할을 수행한다.   

ghost와 matrix 는 서로 다른 인자를 가진 factory_movie가 지정되었고, 이는 두 변수가 서로 다른 scope 를 만들었다고 할 수 있다.   

또한 사용자는 factory_movive를 통해 만들어진 객체의 set_title이나 get_title을 통하지 않고서는 임의로 title을 확인하거나 변경할 수 없는 상태가 된다. 이는 일종의 Private 변수를 사용하는 것 처럼 활용할 수 있다.    

```html
<script>
var arr = []
    for(var i = 0; i < 5; i++){     // 1
        arr[i] = function(){
            return i;
        }
    }
    for(var index in arr) {         // 2
        console.log(arr[index]());
    }
</script>
```

위 코드에서 우리는 log에 0, 1, 2, 3, 4 가 출력될 것으로 예상할 수 있다.  
하지만 코드에서는 5, 5, 5, 5, 5 가 출력되게 된다. 그 이유는 scope에 있다.   

반복문이 진행되면 각 arr[i]에 대입되는 function에 대한 scope가 생성된다.    하지만 이 scope 는 빈 상태로, return i를 위해서는 바깥에 있는 1번 for문에 대한 scope를 확인해야 한다.   

문제는 arr[i]의 scope가 생성되는 동시에 console.log(arr[index]()); 가 수행되지 않는다는 점이다.   

반복문이 종료됨에 따라 1번 for문 scope 내의 i는 5가 되어있는 상태이다.   
이 상황에서 2번 for문이 arr을 참조하게 되면 arr의 scope 는 1번 for문 scope의 i를 참조하게 되고, 결국 5만 출력되는 것이다.    

이를 해결하기 위해선 i를 var 가 아닌 let 으로 선언하면 된다. 

let은 for문의 내부 함수에 대해서 각 경우의 scope를 생성하기 때문에 증가하는 i값에 따른 scope로 0, 1, 2, 3, 4 가 출력되는 것을 알 수 있다. 




<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/743>_   
