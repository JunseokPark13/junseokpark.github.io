---
title: '[CS] 데이터 구조 - Array & ArrayList & LinkedList'
author: Bandito
date: 2021-12-11 19:10:00 +0900
categories: [Study, CS]
tags: [CS, Computer Sceince]
comment: true
---

# Array & ArrayList & LinkedList

## Array
+ 우리가 흔히 아는 배열로, 길이가 고정되어있다. 생성 후 길이를 마음대로 변경할 수 없다.
+ 배열 초기화 시 메모리에 할당되어 ArrayList 보다 속도가 빠르다.
+ Primitive Type(원시 타입), Reference Type(참조 타입) 둘 다 저장이 가능하다.
+ 메모리 공간이 연속적으로 구성되고, 물리 주소와 논리 주소가 동일하여 인덱스 연산자 사용이 가능하다.
+ 특정 위치에 있는 원소 접근 혹은 수정이 `O(1)`의 시간복잡도를 가진다.
+ 배열 중간에서 원소를 제거하거나 삽입한다면 `O(n)`의 시간복잡도를 가진다.
+ 중간에 빈 공간이 있다면 그 만큼 메모리 낭비가 발생할 수 있다. 

<br>

## ArrayList
+ Array 를 이용해 만든 List 형 자료 구조로, 생성 후 데이를 추가하여 가변적 길이로 사용할 수 있다. 
+ 또한 중간에 빈 공간을 허용하지 않기 때문에 메모리 공간 낭비가 없다. 
+ 데이터 추가는 add, 삭제는 remove 를 사용한다. add 로 데이터를 추가할 때 배열의 최대 크기가 넘으면 2배 크기의 배열을 만들고 원본을 복사하여 재생성한다.
+ Primitive Type(원시 타입), Reference Type(참조 타입) 둘 다 저장이 가능하다.
+ 중간에 원소를 삽입/삭제하거나 add 및 copy 는 `O(n)` 의 시간복잡도를 가진다.

<br>

## LinkedList 
+ Node를 활용하는 가변적인 List 형 자료 구조이다.
+ 물리 공간과 논리 공간이 일치하지 않고 메모리 공간 또한 연속적으로 구성되어 있지 않다. 그러므로 인덱스 연산자를 활용할 수 없다.
+ 맨 앞, 맨 뒤에 원소를 삽입하는 시간복잡도가 `O(1)` 이고, 중간에 새로운 원소를 삽입하거나 삭제할 때 저장공간을 확장하거나 축소하여 재할당핲 필요가 없다.
+ 인덱스 연산자를 사용할 수 없어서, 맨 처음 노드나 맨 마지막 노드부터 원하는 위치를 향해 계속 참조를 수행해야 하므로, 접근 및 수정, 삽입, 삭제에 대한 시간 복잡도는 `O(n)` 이다.

    
![image](https://user-images.githubusercontent.com/49611158/145671815-b981befd-be88-405f-ae1b-7a99e0295e6f.png)    


<br>

## 자바스크립트에서의 배열
+ 일반적인 배열은 선언 후 배열의 크기를 변경할 수 없고, 모든 배열의 공간이 동일한 크기를 가지며 연속적으로 이어져 있는 밀집 배열(dense array)이다.
+ 하지만 자바스크립트의 배열은 일반적인 배열과 다른, 배열의 동작을 흉내낸 특수 객체이다.
    - 배열의 요소들을 위한 메모리 공간은 모두 동일하지 않아도 된다.
    - 명시적인 배열 자료형이 없으므로 어떤 데이터 타입이라도 넣을 수 있다.
    - 동적으로 크기 조절이 가능하다.
    - 배열의 요소가 연속적이지 않은 희소 배열(sparse array)이다.

```javascript
console.log(Object.getOwnPropertyDescriptors([1, 2, 3]));
/*
{
  '0': { value: 1, writable: true, enumerable: true, configurable: true },
  '1': { value: 2, writable: true, enumerable: true, configurable: true },
  '2': { value: 3, writable: true, enumerable: true, configurable: true },
  length: { value: 3, writable: true, enumerable: false, configurable: false }
}
*/
```

+ 위와 같이 자바스크립트의 배열은 인덱스를 프로퍼티 키로 갖고, length 프로퍼티를 갖는 특수 객체이다. 모든 값은 객체의 프로퍼티 값이 될 수 있으므로 어떤 타입의 값이라도 배열의 요소가 될 수 있는 것이다.

+ 일반적인 배열 vs 자바스크립트 배열
    - 일반적인 배열은 인덱스로 배열 요소에 빠르게 접근이 가능하지만, 특정 요소를 탐색하거나 삽입, 삭제에서는 효율적이지 않다.
    - 자바스크립트 배열은 해시 테이블로 구현된 객체이므로 접근은 성능적으로 느리지만, 특정 요소 탐색이나 요소를 삽입, 삭제하는 경우에는 일반적인 배열보다 빠르다.
+ 하지만 대부분의 모던 자바스크립트 엔진은 배열을 일반 객체와 구별하여 보다 배열처럼 동작하도록 최적화하여 구현하고 있다.