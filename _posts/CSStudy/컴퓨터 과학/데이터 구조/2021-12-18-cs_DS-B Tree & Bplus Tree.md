---
title: '[CS] 데이터 구조 - B Tree & B+ Tree'
author: Bandito
date: 2021-12-18 19:40:00 +0900
categories: [Study, CS]
tags: [CS, Computer Sceince]
comment: true
---

# B Tree & B+ Tree

+ 이진 트리는 하나의 부모가 두 개의 자식밖에 가지질 못하므로 균형이 맞는 트리를 구성하지 못한다면 검색 효율이 매우 떨어질 위험이 있다.     
하지만 구조의 간결함 덕분에 검색, 삽입, 삭제 모두 `O(logN)`의 성능을 기대할 수 있기 때문에 이를 개선한 데이터 구조가 많이 개발되었다.

## B Tree

<br>

![image](https://user-images.githubusercontent.com/49611158/146637575-6c937cf0-1c33-42c5-828f-5c53aa495f1d.png)

<br>

+ B Tree 는 이진 탐색 트리를 확장한 트리로, 각 노드(Node) 는 여러 개의 Key를 가질 수 있고, 여러 개의 자식(Child) 를 가질 수 있다.
+ B Tree 는 트리의 균형을 자동으로 맞추는 로직까지 갖추어 레벨로는 완전히 균형을 맞춘 트리이다.
+ 최대 M개의 자식을 가질 수 있는 B트리를 M차 B트리라고 한다.
    - 노드는 최대 M개 부터 M/2개 까지의 자식을 가질 수 있다.
    - 노드에는 최대 M-1개 부터 [M/2]-1개의 키가 포함될 수 있다.
    - 노드의 키가 x개라면, 자식의 수는 x+1개이다.
    - 최소차수는 자식수의 하한값을 의미하며, 최소차수가 t라면 `M = 2t - 1`을 만족한다.     
    최소차수 t가 2라면 `3차 B트리`이며, key의 하한은 1개이다.
+ 아래 그림은 차수가 3인 B 트리이다. key 들은 노드 안에서 항상 정렬된 값을 가지며, 이진 검색 트리처럼 각 key들의 왼쪽 자식은 key 보다 작고, 오른쪽 자식은 key 보다 크다.



+ [삽입, 검색 삭제에 대한 내용](https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Tree)

<br>

## B+Tree

<br>

![image](https://user-images.githubusercontent.com/49611158/146637950-52a6d1c1-7a19-4f13-9f75-76ee6df80a7f.png)

<br>

+ B+Tree에서는 data가 오직 리프 노드에만 들어갈 수 있다.
    - 모든 key, data가 리프 노드에 모여있다. B트리는 리프노드가 아닌 각자 key 마다 data를 가지지만, B+트리는 리프 노드에 모든 data를 가진다.
    - 모든 리프노드가 연결리스트의 형태를 띄고 있다. B트리는 옆에 있는 리프노드를 검사할 때 다시 루트노드부터 검사해야하지만, B+트리는 리프노드에서 선형 검사를 수행할 수 있어 시간복잡도가 줄어든다.
    - 리프노드의 부모 key는 리프노드의 첫번쨰 key보다 작거나 같다.
+ B트리와 같이 M차 B+트리는 M차 B트리와 같은 특징을 가진다.
+ [삽입, 검색 삭제에 대한 내용](https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Plus-Tree)
