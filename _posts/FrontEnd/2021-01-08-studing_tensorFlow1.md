---
title: '[Machine Learning] TensorFlow 정리 - 1'
author: Bandito
date: 2021-01-08 20:35:00 +0900
categories: [Study, Javascript]
tags: [Machine Learning, Javascript, TensorFlow]
comment: true
description: 'asdsadasd'
---

# TensorFlow 정리 - 1

+ 이 문서에 있는 내용들
    - [머신 러닝이란?](#머신-러닝이란)
    - [지도학습](#지도학습)
    - [지도학습의 작업 순서](#지도학습의-작업-순서)
    - [모델](#모델)
    - [나의 모델 만들기](#나의-모델-만들기)
        + [라이브러리 설치](#라이브러리-설치)
        + [과거의 데이터 준비하기](#과거의-데이터-준비하기)
        + [모델의 모양 만들기](#모델의-모양-만들기)
        + [모델을 학습시키기](#모델을-학습시키기)
        + [모델의 이용과 학습](#모델의-이용과-학습)
        + [정확도 측정](#정확도-측정)
    - [가중치와 편향](#가중치와-편향)


Tensorflow.js 는 자바스크립트로 딥러닝을 이용할 수 있도록 돕는 라이브러리이다. 자바스크립트가 실행 가능한 모든 곳에서 실행이 가능하다. 

<br/>

## 머신 러닝이란? 
***

기계를 학습시켜서 인간의 판단능력을 기계에게 위임하는 기능을 Machine Learning, 즉 기계학습이라 한다.    

기계 학습에는 지도학습, 강화학습, 비지도 학습이 있다. 이 중 TensorFlow 를 통해 지도학습에 대해 공부하고자 한다.   

<br/>

## 지도학습 
***

지도학습을 통해 컴퓨터를 학습시킨다면 컴퓨터는 학습한 적이 없는 정보를 만났을 때 이에 대한 정보를 알 수 있다.   

지도학습은 두 가지 방식이 있다.
1. 회귀(Regression) : 맞추려는 정보가 숫자일 때
2. 분류(Classification) : 맞추려는 정보가 범주일 때 

이러한 문제를 해결하기 위한 알고리즘 방식으로는 Decision Tree, Random Forest, KNN, SVM, Neural Network 가 있으며, 이번 학습에서는 Neural Network 방식을 사용한다.    

Neural Network 는 사람의 두뇌가 동작하는 방법을 모방하여 기계가 사람처럼 학습을 할 수 있도록 고안된 알고리즘이다. 이는 Deep Learning 이라는 표현으로도 불린다.   

우리는 TensorFlow 라이브러리를 사용하여 이러한 Deep Learning 기술을 손쉽게 사용할 수 있다. 

<br/>

## 지도학습의 작업 순서
***

교육에서는 레모네이드 장사를 예시로 지도학습을 설명하고 있다.  

당신은 레모네이드 프렌차이즈의 사장이다. 다음 날 장사를 위해서는 필요한 레몬을 미리 구매해두어야하지만, 레몬을 너무 적게 준비하면 수익을 올리기 힘들고 너무 많이 준비하면 손해를 보게 된다.   

당신은 레모네이드의 판매량이 그 날의 온도와 관계가 있다는 것을 알아내고 이를 통해 머신 러닝을 활용하여 준비해야 할 레몬의 수를 예측하려고 한다.    

지도학습을 위해서는 다음과 같은 작업이 필요하다.  

1. 과거의 데이터를 준비한다. 이 데이터를 표로 표현하여 결과와 이에 영향을 미치는 원인을 파악해야 한다.
2. 데이터를 분석하여 결과가 될 수 있는 열의 수와 이의 원인이 될 수 있는 열의 수를 파악하여 모델을 만든다.
3. 과거의 데이터로 모델을 학습(FIT)시킨다. 이 과정을 통해 모델은 원인에 따른 결과를 예측할 수 있는 능력을 가지게 된다.   
4. 완성된 모델에 원하는 값을 입력하고 결과를 받아낸다. 

결국 우리는 모델이 있어야 머신 러닝을 활용할 수 있다는 것을 알 수 있다.   

<br/>

## 모델
***

모델을 활용하는 것은 머신러닝의 가장 중요한 부분이라고 할 수 있다. TensorFlow 에서는 모델의 사용에 대한 3가지 방식을 제시한다. 

1. 기존 모델을 사용 
2. 기존 모델을 다시 학습시키기
3. 자바스크립트로 개발 

학습에서는 3번의 직접 개발을 목표로 한다.

<br/>

## 나의 모델 만들기 
***

우리는 TensorFlow.js 의 라이브러리를 활용하여 우리가 준비한 과거 데이터를 이용한 모델을 생성할 수 있다. 그 전체 코드는 다음과 같다. 

```html
<!DOCTYPE html>
<html>
 
<head>
    <title>TensorFlow.js Tutorial - lemon</title>
 
    <!-- Import TensorFlow.js -->
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@1.0.0/dist/tf.min.js"></script>
     
</head>
 
<body>
    <script>
        // 1. 과거의 데이터를 준비합니다. 
        var 온도 = [20,21,22,23];
        var 판매량 = [40,42,44,46];
        var 원인 = tf.tensor(온도);
        var 결과 = tf.tensor(판매량);
 
        // 2. 모델의 모양을 만듭니다. 
        var X = tf.input({ shape: [1] });
        var Y = tf.layers.dense({ units: 1 }).apply(X);
        var model = tf.model({ inputs: X, outputs: Y });
        var compileParam = { optimizer: tf.train.adam(), loss: tf.losses.meanSquaredError }
        model.compile(compileParam);
 
        // 3. 데이터로 모델을 학습시킵니다. 
        var fitParam = { epochs: 100} 
        // var fitParam = { epochs: 100, callbacks:{onEpochEnd:function(epoch, logs){console.log('epoch', epoch, logs);}}} // loss 추가 예제
        model.fit(원인, 결과, fitParam).then(function (result) {
             
            // 4. 모델을 이용합니다. 
            // 4.1 기존의 데이터를 이용
            var 예측한결과 = model.predict(원인);
            예측한결과.print();
 
        });  
 
        // 4.2 새로운 데이터를 이용
        // var 다음주온도 = [15,16,17,18,19]
        // var 다음주원인 = tf.tensor(다음주온도);
        // var 다음주결과 = model.predict(다음주원인);
        // 다음주결과.print();
    </script>
</body>
 
</html>
```

이 코드를 통하여 각 부분별로 내용을 정리하고자 한다.  

<br/>

### 라이브러리 설치 
***

```html
<head>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@1.0.0/dist/tf.min.js"></script> 
</head>
```

웹에서 Tensorflow.js 의 라이브러리를 사용하기 위해서는 위와 같은 스크립트 코드를 head 태그에 입력해주어야 한다. 이 코드는 [텐서플로우 공식 홈페이지 가이드](https://www.tensorflow.org/js/tutorials/setup?hl=ko){:target="_blank"} 에서 확인할 수 있다.   

<br/>

### 과거의 데이터 준비하기
***

```html
<script>
    var 온도 = [20,21,22,23];
    var 판매량 = [40,42,44,46];
    var 원인 = tf.tensor(온도);
    var 결과 = tf.tensor(판매량);
</script>
```

먼저 모델을 생성하기 위한 과거의 데이터를 준비하여야 한다. 레모네이드의 판매량은 온도와 관련이 있다는 가정 하에 준비된 데이터들이다.   

+ 온도는 물품 판매일의 온도를 의미한다. 이는 데이터에서 **원인**이 된다.
+ 판매량은 판매일의 최종 판매량을 의미한다. 이는 데이터에서 **결과**가 된다.

이를 통해 우리는 판매량 = 온도 * 2 의 관계를 갖고 있다는 것을 알 수 있다.   

이를 TensorFlow가 이해할 수 있는 데이터의 형태로 만들기 위해 tf.tensor를 통해 알맞은 형태로 변환할 수 있다. 

<br/>

### 모델의 모양 만들기 
***

```html
<script>
    var X = tf.input({ shape: [1] });
    var Y = tf.layers.dense({ units: 1 }).apply(X);
    var model = tf.model({ inputs: X, outputs: Y });
    var compileParam = { optimizer: tf.train.adam(), loss: tf.losses.meanSquaredError }
    model.compile(compileParam);
</script>
```

가장 먼저 해야 할 일은 모델에 입력 및 출력될 값이 몇 개인지를 지정하는 것이다. 
우리는 온도와 판매량 각각 1개의 원인과 결과를 갖고 있다.    
+ var X = tf.input({ shape: [1] }); 코드를 통해 1개의 원인,     
+ var Y = tf.layers.dense({ units: 1 }).apply(X); 코드를 통해 1개의 결과를 갖고 있다는 것을 지정할 수 있다.

이러한 input 과 output 을 정의했다면 model 메소드를 사용하여 모델을 정의하고, complie 메소드로 모델을 생성할 수 있다.     

complie 메소드에는 특정 파라미터를 지정해주어야 한다.
+ optimizer 는 현재 생성하고자 하는 모델에 대해 더 효율적인 방법을 지정해주는 것
+ loss 는 생성된 모델의 완성도를 테스트 할 때의 측정 방법을 지정해주는 것

<br/>

### 모델을 학습시키기  
***

```html
<script>
    var fitParam = { epochs: 100} 
    model.fit(원인, 결과, fitParam).then(function (result) {
        ...
    });
</script>
```

다음은 모델을 학습(Fit)시키는 작업이 필요하다.    

모델을 학습시키기 위한 파라미터를 전달하는데, 여기서 사용하는 epochs는 얼마나 반복하여 학습을 진행할 것인지를 지정하는 것이다. epochs 값이 커질수록 모델은 더 완성도 있는 결과값을 내놓을 수 있다.   

원인, 결과, epochs 값을 인자로 하는 fit 메소드를 통해 모델을 학습시키고, 함수 내에는 이를 통한 예측 값을 출력시키는 내용을 작성하여 학습 상태를 확인할 수 있다.   

### 모델의 이용과 학습  
***

```html
<script>
    model.fit(원인, 결과, fitParam).then(function (result) {
        var 예측한결과 = model.predict(원인);
        예측한결과.print();
    }); 
</script>
```

predict 는 모델에게 원인에 대한 결과를 받아낼 수 있는 메소드이다. 인자로 받은 원인을 통해 결과 값을 추측하고, print 메소드를 통해 이를 출력할 수 있다.    

epochs 값이 적다면 적절한 값을 출력하지 못할 수 있다. 추가적인 학습을 통하여 더 완성도 있는 결과를 낼 수 있다.   


### 정확도 측정
*** 

```html
<script>
    //var fitParam = { epochs: 100} 
    var fitParam = { epochs: 100, 
    callbacks:{onEpochEnd:function(epoch, logs)
    {
        console.log('epoch', epoch, logs, 'RMSES=>', Math.sqrt(logs.loss));
    }}} 
    
    model.fit(원인, 결과, fitParam).then(function (result) {
        ...
    });
</script>
```
```console
...
epoch 293 {loss: 5651.81787109375} RMSES=> 75.1785732179971
epoch 294 {loss: 5648.55615234375} RMSES=> 75.15687694644949
epoch 295 {loss: 5645.29638671875} RMSES=> 75.13518740722452
epoch 296 {loss: 5642.037109375} RMSES=> 75.1134948552855
epoch 297 {loss: 5638.779296875} RMSES=> 75.0918057904789
epoch 298 {loss: 5635.5234375} RMSES=> 75.0701234679949
```

위 코드는 기존에 epochs 값만 지정했던 fitParam 에 콜백 함수를 통해 fit 메소드 작동 시 각 학습에 대한 로그를 출력하도록 하고 있다.     

출력 내용을 보면 logs 는 loss 라는 프로퍼티를 가진 객체라는 것을 알 수 있다. 이 loss 는 모델의 학습 상태를 나타내는 것으로, 0에 가까울 수록 학습상태가 좋다는 것을 뜻한다.    

모델은 기존에 주어진 원인과 결과를 토대로 학습을 진행한다. 충분한 학습이 이루어지지 않는다면 실제 원인에 따른 결과 값과 모델의 예측 결과 값은 차이가 있을 수 있다. 우리는 이러한 오차 수치를 파악하기 위해 이전에 다음과 같은 코드를 작성한 적이 있다. 

```html
<script>
    var compileParam = { optimizer: tf.train.adam(), loss: tf.losses.meanSquaredError }
</script>
```

이 코드에서 loss : tf.losses.meanSquaredError 는 
('각 원인에 따른 결과' - '모델의 예측값')^2 의 합을 값들의 갯수만큼 나눈 것이다. 때문에 오차의 값이 작아질수록 loss 값은 0에 가까워 질 것이다. 이를 평균 제곱 오차(Mean Squared Error), 즉 MSE 라 한다.   
하지만 loss 값은 기존의 값들을 제곱한 것이므로 여기서 제곱근을 구해준 평균 제곱근 오차(Root Mean Squared Error) RMSE 를 사용하여 더 보기 좋은 값을 얻을 수 있다.

## 가중치와 편향
***

모델을 만들기 위해 사용했던 원인과 결과를 생각해보면 판매량 = 2 * 온도 라는 가정을 할 수 있었다. 이와 같이 모델은 기본적으로 y = a*x + b 라는 계산식을 갖는다.       
여기서 a는 가중치(weight), b 는 편향(vias)이라는 이름으로 불리지만, 둘 다 합쳐서 가중치라고 불리기도 한다. 

```html
<script>
    var weights = model.getWeights();
    var weight = weights[0].arraySync()[0][0];
    var vias = weights[1].arraySync()[0];
    </script>
```

model.getWeigths() 은 2개의 값을 가진 배열을 반환하고, 이 배열 내의 값들은 tensor 객체임을 알 수 있다. 이 중 첫번째 값은 가중치, 두번째 값은 편향이다.   

이를 통해 모델은 predict 메소드에서 y = weight * x + vias 를 계산한다.    
모델이 자신만의 식을 생성하는 것은 복잡한 일이지만, predict 를 하는 것은 그다지 어려운 작업이 아니라는 사실을 알 수 있다.   





<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/4628>_   
_<https://opentutorials.org/course/4548>_ 
