---
title: '[Machine Learning] TensorFlow 정리 - 2'
author: Bandito
date: 2021-01-09 14:00:00 +0900
categories: [Study, Javascript]
tags: [Machine Learning, Javascript, TensorFlow]
comment: true
description: 'asdsadasd'
---

# TensorFlow 정리 - 2
+ 이 문서에 있는 내용들
    + [변수가 여러개일 때](#변수가-여러개일-때)
    + [딥러닝 - Hidden Layer](#딥러닝---hidden-layer)

<br/>

## 변수가 여러개일 때  
***

이전까지 살펴봤던 예제에서는 원인이 되는 열이 1개 뿐이었다. 여기서 원인이 되는 열이 많아진다면 계산은 더 복잡해질 수 있다.

![bostonchart](https://drive.google.com/uc?export=view&id=1cNJy0vF-F0E963274trgEFksQCAcOwFs)

위 테이블은 회귀분석을 위한 예시로 유명한 보스톤 주택 가격 표이다. 위 사진에서 1~13번 열은 원인, 결과가 되는 값은 가장 오른쪽에 있는 14번째 집값 열이고, 이는 해당 지역의 집값 중 중간값을 의미한다.   

이번에는 이 값들을 가지고 분석을 수행하고자 한다.  

```html
<script>
    var 보스톤_원인 = [
    [0.00632,18,2.31,0,0.538,6.575,65.2,4.09,1,296,15.3,396.9,4.98],
    [0.02731,0,7.07,0,0.469,6.421,78.9,4.9671,2,242,17.8,396.9,9.14],
    ...
    ]
    var 보스톤_결과 = [ 
    [24],
    [21.6],
    ...
    ]
</script>
```

데이터를 담은 js 파일에는 위와 같은 보스톤_원인 배열과 보스톤_결과 배열이 있다. 이전에 사용했던 Tensorflow.js 코드에 위 값을 대입할 것이다. 

이를 통해 출력되는 RMSE 는 6000번 이상의 학습을 진행했음에도 4~5 사이를 유지하였다. 이 데이터에 대한 가중치와 편향은 다음과 같았다. 

```console
// weight
0: [-0.09378816932439804]
1: [0.04790984094142914]
2: [-0.024096526205539703]
3: [2.7535271644592285]
4: [-1.0979664325714111]
5: [5.345874309539795]
6: [-0.010746989399194717]
7: [-1.035591959953308]
8: [0.19616594910621643]
9: [-0.01056033093482256]
10: [-0.4941858649253845]
11: [0.01280394196510315]
12: [-0.45401158928871155]
// vias
[6.612276077270508]
```

가중치를 보았을 때 6번째 값인 RM, 방의 수가 가장 결과값에 영향을 많이 준다는 사실을 알 수 있었다.

<br/>

```html
<script>
    var 보스톤_원인 = [
    [0.00632, 18, 2.31, 0, 0.538, 6.575, 65.2, 4.09, 1, 296, 15.3, 396.9],
    [0.02731, 0, 7.07, 0, 0.469, 6.421, 78.9, 4.9671, 2, 242, 17.8, 396.9],
    ...
    ]
    var 보스톤_결과 = [ 
    [4.98, 24],
    [9.14, 21.6],
    ...
    ]
</script>
```
```html
<script>
    var X = tf.input({ shape: [12] });
    var Y = tf.layers.dense({ units: 2 }).apply(X);
    var model = tf.model({ inputs: X, outputs: Y });
</script>
```
위와 같이 종속 변수, 즉 결과가 2개인 경우가 있을 수 있다. 이럴 때에는 위와 같이 모델에 삽입하는 X 와 Y 에서의 값들을 적절히 수정하는 것으로 적용할 수 있다.   


## 딥러닝 - Hidden Layer
***

이전에도 설명했듯이 딥 러닝은 인간의 뇌를 이루는 신경세포인 뉴런을 모방한 방식이다. 우리가 생성한 모델을 원인과 결과, 가중치와 편향의 조합으로 그림처럼 나타내면 다음과 같다. 

![perceptron](https://drive.google.com/uc?export=view&id=1bZSJq_m5qNkD3N1UKqyXIlvIHVMWUhj5)

이를 인공지능 분야에서는 perceptron 이라고 한다. 이는 여러 Node로 구성되고 이러한 perceptron이 모여 여러 층의 Layer 를 구성하여 전체적인 Artificial Neural Network, 즉 인공 신경망을 구축하게 된다.   

![layers](https://drive.google.com/uc?export=view&id=10Oqlleh5TJlThvpcd7UmTZ5clJP3ejAM)

여러 perceptron 으로 구성된 신경망은 가장 바깥쪽에 위치하는 input layer와 output layer 를 제외하면 중간의 숨겨진 hidden layer 로 구성되게 된다.    
hidden layer의 수와 여기에 속한 node 의 수가 많을 수록 더 완성도 높은 모델을 만들 수 있다.   

```html
<script>
    var X = tf.input({ shape: [13] });
    var H1 = tf.layers.dense({units:13, activation:'relu'}).apply(X);
    var H2 = tf.layers.dense({units:13, activation:'relu'}).apply(H1);
    var Y = tf.layers.dense({ units: 1 }).apply(H2);
    var model = tf.model({ inputs: X, outputs: Y });
</script>
```

hidden layer를 추가하는 것은 어렵지 않다. 위 코드 처럼 input layer인 X 부터 시작하여 각 layer 를 apply 하는 중간 H1, H2 layer를 선언해주고, 최종적으로 output layer 인 Y 로 연결되게 한다.  

hidden layer 에는 activaction 이라는 function 을 지정해주어야 제대로 동작한다. 이는 가중치와 편향치를 조절하는 역할을 하며, 'ReLU' 함수는 가장 일반적인 방법에 속한다.   





<br/><br/><br/>
_참고한 글이나 영상 :_   
_<https://opentutorials.org/course/4628>_   
_<https://opentutorials.org/course/4548>_ 
