---
title: '[Javascript] Javascript 정리 - 8'
author: Bandito
date: 2021-01-08 12:00:00 +0900
categories: [Study, Javascript]
tags: [Javascript, HTML, FrontEnd]
comment: true
description: 'asdsadasd'
---

# Javascript 정리 - 8

공부하면서 생소하거나 잘 모르던 내용들을 정리

+ 이 문서에 있는 내용들
    - [Ajax](#ajax)
    - [JSON](#json)



<br/>

## Ajax
***

Ajax 는 Asynchronous Javascript and XML의 약자로 비동기적 자바스크립트와 XML 이라고 할 수 있다. Ajax 는 웹브라우저와 웹서버가 내부적으로 데이터통신을 하게 한다. 그리고 변경된 결과를 웹페이지에 프로그래밍적으로 반영하여 웹페이지의 로딩 없이 서비스를 사용 가능하게 해준다.    

자바스크립트를 통하여 비동기적으로 서버와 브라우저가 데이터를 주고받을 수 있으며, 이 때 XMLHttpRequest 라는 API 를 사용하게 된다. 

```php
// time.php
<?php
$d1 = new Datetime;
$d1->setTimezone(new DateTimezone("asia/seoul"));
echo $d1->format('H:i:s');
?>
```
```html
<p>time : <span id="time"></span></p>
<input type="button" id="execute" value="execute" />
<script>
    var exe = document.getElementById('execute');
    function handler(event) {
        var xhr = new XMLHttpRequest();
        xhr.open('GET', './time.php');
        xhr.onreadystatechange = function () {
            if (xhr.readyState === 4 && xhr.status === 200) {
                document.getElementById('time').innerHTML = xhr.responseText;
            }
        }
        xhr.send();
    }
    exe.addEventListener('click', handler);
</script>
```

위 코드는 time.php 파일과 이를 실행시킬 html 파일의 코드이다.     
execute 라는 id를 가진 버튼을 클릭하면 이에 연결된 이벤트 리스너가 작동하게 된다.    

XMLHttpRequest 를 사용하여 객체를 생성하고 open 메소드를 통해 접속하려는 대상인 파일을 지정한다.  첫번째 인자는 form 태그의 method에 대응하는 GET/POST 방식을 선택하고 두번째 인자는 action, 즉 접속하고자 하는 서버쪽의 리소스이다.   

onreadystatechange 이벤트는 서버와의 통신이 끝났을 때 호출되는 이벤트이다.   
readyState는 통신의 현재 상태로, 4는 통신이 완료되었음을 의미한다.    
status는 HTTP 통신의 결과로, 200은 통신이 성공하였음을 의미한다.   
여기서 xhr.responseText 를 사용하여 서버에서 전송한 데이터를 가져올 수 있다.   

마지막에 send 메소드를 사용하면 위에서 정했던 방식으로 XMLHttpRequest 객체가 통신을 수행하게 된다.   
<br/>

```php
// time.php
<?php
$d1 = new DateTime;
$d1->setTimezone(new DateTimezone($_POST['timezone']));
echo $d1->format($_POST['format']);
?>
```

```html
<p>time : <span id="time2"></span></p>
    <select id="timezone">
        <option value="Asia/Seoul">asia/seoul</option>
        <option value="America/New_York">America/New_York</option>
    </select>
    <select id="format">
        <option value="Y-m-d H:i:s">Y-m-d H:i:s</option>
        <option value="Y-m-d">Y-m-d</option>
    </select>
    <input type="button" id="execute2" value="execute" />
<script>
    document.getElementById('execute2').addEventListener('click', function (event) {
        var xhr = new XMLHttpRequest();
        xhr.open('POST', './time2.php');
        xhr.onreadystatechange = function () {
            document.querySelector('#time2').innerHTML = xhr.responseText;
        }
        xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
        var data = '';
        data += 'timezone=' + document.getElementById('timezone').value;
        data += '&format=' + document.getElementById('format').value;
        xhr.send(data);
        });
</script>
```

이번 코드에서는 Timezone 과 format 을 지정하여 값을 받아오는 형식이다.   
대부분의 코드가 이전 코드와 유사하지만 이번에는 POST 방식을 통해 데이터를 전송하는 점에서 차이가 있다.   
setRequestHeader 메소드를 사용하여 전송할 데이터 타입의 형식(MIME)을 지정하고 서버로 전송할 데이터를 형식에 맞게 만든다. 형식은 이름=값&이름=값&.. 의 형식을 따른다.   

이후 send 메소드의 인자로 만든 형식을 삽입하면 데이터가 전송된다.   

## JSON
***

JSON 은 Javascript Object Notion의 약자로, 자바스크립트에서 객체를 만들 때 사용하는 표현식을 의미한다. 이는 사람과 기계가 이해하기 쉽고 데이터의 용량이 작다.   

![json_obj](https://drive.google.com/uc?export=view&id=16EackveCLRcEnkvEiPPTcA-1XtJlyL12)   
![json_ary](https://drive.google.com/uc?export=view&id=1FcX06mbA_5o9G0eaJ79bKUkdbEl1P3Kf)


위 두 사진은 [JSON 공식 홈페이지](http://www.json.org/json-ko.html){:target="_blank"} 에서 제공하는 JSON 의 Object 와 Array 의 형태이다. 

위 사진에서 Object 는 { 로 시작하고 } 로 끝나며, 내부의 값들은 'string:value' 의 형태로 저장되고 ',' 로 구분됨을 알 수 있다.   

Array 는 \[ 로 시작되고 \] 로 끝나며, 내부의 값들은 'value' 의 형태로 저장되고 ',' 으로 구분됨을 알 수 있다.   

이는 실제 코드에서 다음과 같이 작성된다.   

```html
<script>
    var person = {"name":"Park", "age":26, "job":"programmer"}
    var alphabet = ["A", "B", "C", "D"];
</script>
```

이러한 JSON 형태의 데이터는 설정의 저장이나 데이터의 전송 등에 효율적으로 사용될 수 있다. 

+ JSON.parse() : 인자로 전달된 문자열을 자바스크립트의 데이터로 변환
+ JSON.stringify() : 인자로 전달된 자바스크립트의 데이터를 문자열로 변환
+ json_encode() : PHP의 데이터를 JOSN 형식으로 전환해주는 php 내장 함수
+ json_decode() : JSON 형식의 문자열을 PHP 변수로 전환해주는 php 내장 함수

```html
<script>
    var data = new Object();
    data.timezone = document.getElementById('timezone').value;
    data.format = document.getElementById('format').value;
    xhr.setRequestHeader("Content-Type", "application/json");
    xhr.send(JSON.stringify(data));
</script>
```

또한 데이터를 전송하기 위해 JSON 을 사용하려면 Object 형태로 생성하고 setRequestHeader 의 인자를 "application/json" 으로 설정해야 한다.





## X
***
```html
<script>
</script>
```



<br/><br/><br/>
추후 추가 포스팅 예정...

<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/1375>_   
