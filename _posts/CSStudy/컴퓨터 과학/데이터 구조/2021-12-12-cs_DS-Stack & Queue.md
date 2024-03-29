---
title: '[CS] 데이터 구조 - Stack & Queue'
author: Bandito
date: 2021-12-12 20:30:00 +0900
categories: [Study, CS]
tags: [CS, Computer Sceince]
comment: true
---

# Stack & Queue

## Stack    

![image](https://user-images.githubusercontent.com/49611158/145707530-fd05ec9c-dcc3-4fc7-8006-3f6ee229d3a1.png)

+ 영어로 stack 은 쌓아올린다는 것을 의미한다. 이와 같이 스택 자료구조는 물건을 쌓는 것 처럼 차곡차곡 쌓아 올린 형태의 자료구조를 의미한다.

### Stack 의 특징
+ 스택은 정해진 방향(`Top`) 으로만 데이터를 넣고 꺼낼 수 있다.
+ `Top` 은 스택에서 가장 위에 있는 데이터를 가리키며, 새로운 데이터를 넣으면 Top 이 가장 마지막에 들어온 새로운 데이터로 갱신된다.
+ 이를 LIFO(Last In First Out), 후입선출 방식이라고 부른다.
+ 스택에 새로운 데이터를 넣는 삽입 연산을 `push`, 가장 위의 데이터를 꺼내 삭제하는 연산을 `pop` 이라고 한다.

### Javascript 에서의 Stack 구현
+ 자바스크립트의 배열은 굉장히 유연하고 관련 메서드도 다양하기 때문에 매우 쉽게 스택을 구현할 수 있다.

```javascript
class Stack {
    constructor {
        this._array = new Array()
    }
    push(item) {
        this._array.push(item)
    }
    pop() {
        return this.array.pop()
    }
    peek() {
        return this.array[this.array.length - 1]
    }
    size() {
        return this.array.length
    }
    empty() {
        return this.array.length === 0
    }
    contain(item) {
        return this.array.some(val => val === item)
    }
}
```

<br>

## Queue    
    
![image](https://user-images.githubusercontent.com/49611158/145707947-1fc2dd89-0a60-4062-980f-ec8c7728748d.png)    

+ 영어로 queue 는 대기줄, 줄을 서서 기다리는 것을 의미한다. 이와 같이 큐 자료구조는 사람들이 줄을 서는 것 처럼 데이터들이 순차적으로 들어가고 나가는 자료구조를 의미한다.

### Queue 의 특징
+ 큐에는 데이터가 삽입되는 `rear` 부분과 데이터가 빠져나가는 `front` 부분이 있다. 때문에 가장 첫 원소는 `front`, 가장 끝 원소는 `rear` 에 존재한다.
+ `rear` 에서만 데이터가 들어오고, `front` 에서만 데이터가 빠져나갈 수 있다.
+ 이를 FIFO(First In, First Out), 선입선출 방식이라 부른다. 
+ 큐에 새로운 데이터를 `rear` 에 넣는 삽입 연산을 `enQueue`, `front` 에서 데이터를 꺼내 삭제하는 연산을 `deQueue` 라고 부른다.

### Javascript 에서의 Queue 구현
+ 스택과 마찬가지로 큐 또한 자바스크립트의 배열 메서드들을 통해 만들 수 있다.

```javascript
class Queue {
    constructor {
        this._array = new Array()
    }
    enqueue(item) {
        this._array.push(item)
    }
    dequeue() {
        return this.array.shift()
    }
    peek() {
        return this.array[0]
    }
    size() {
        return this.array.length
    }
    empty() {
        return this.array.length === 0
    }
    contain(item) {
        return this.array.some(val => val === item)
    }
}
```