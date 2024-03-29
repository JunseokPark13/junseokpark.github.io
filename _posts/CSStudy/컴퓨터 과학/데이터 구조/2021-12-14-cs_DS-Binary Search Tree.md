---
title: '[CS] 데이터 구조 - Binary Search Tree'
author: Bandito
date: 2021-12-14 23:12:00 +0900
categories: [Study, CS]
tags: [CS, Computer Sceince]
comment: true
---

# Binary Search Tree

## 이진 탐색 트리란
+ 이진 탐색 트리(Binary Search Tree) 란 이진 탐색(Binary Search) 와 연결리스트(Linked List)를 결합한 자료구조의 일종이다.
+ 이진탐색의 효율적인 탐색 능력을 유지하면서, 빈번한 자료 입력과 삭제가 가능하도록 고안되었다.
+ 이진탐색은 탐색에 소요되는 시간복잡도가 `O(logn)` 으로 빠르지만, 자료의 입력이나 삭제가 불가능하다.
+ 연결리스트의 경우 자료 입력 및 삭제에는 `O(1)` 이지만, 탐색에는 `O(n)` 의 시간복잡도를 가진다.


<br>

## 이진 탐색 트리의 속성
    
![image](https://user-images.githubusercontent.com/49611158/145981420-9bd0a967-0d3d-46b1-a57f-f4f93fd4f206.png)    

+ 각 노드의 왼쪽 서브트리에는 해당 노드의 값보다 작은 값을 지닌 노드들로 이루어져있다.
+ 각 노드의 오른쪽 서브트리에는 해당 노드의 값보다 큰 값을 지닌 노드들로 이루어져있다.
+ 중복된 노드가 있으면 안된다.
    - 검색 목적의 자료구조이므로 중복이 많으면 굳이 트리를 사용할 필요가 없다.
    - 중복인 경우, 노드에 count 값을 증가시키는 등의 방식이 적합하다.
+ 왼쪽 및 오른쪽 서브트리 또한 이진 탐색 트리이다.
+ 이진 탐색 트리를 순회할 때는 중위 순회(in-order) 방식을 사용한다.
    - 왼쪽 서브트리 -> 루트 -> 오른쪽 서브트리
    - 이를 통해 모든 값들을 정렬된 순서로 읽을 수 있다.

<br>

## 이진 탐색 트리의 핵심 연산

```javascript
class Node {
    constructor(data, left = null, right = null) {
        this.data = data
        this.left = left
        this.right = right
    }
}
```



### 검색
+ 트리 안에 해당 값이 포함되어 있는지를 확인하는 메서드이다.

```javascript
class BST {
    constructor() {
        this.root = null
    }
    
    /* ..... */

    find(data) {
        const current = this.root

        while (current !== null) {
            if (current.data === data) return true
            else if (current.data > data) current = current.left
            else current = current.right
        }
        return false
    }
}
```

### 삽입
+ 새로운 값을 추가한다.
+ 트리 중간에 조건에 맞는 위치가 있을 수 있으나, 서브트리의 속성이 깨질 수 있으므로 삽입 연산은 반드시 단말 노드에서 수행한다.

```javascript
class BST {
    constructor() {
        this.root = null
    }

    /* ..... */

    add(data) {
        if (this.root === null) {
            this.root = new Node(data)
            return
        }

        const current = this.root
        const searchTree = (node) => {
            if (data < node.data) {
                if (node.left === null) {
                    node.left = new Node(data)
                    return
                }
                return searchTree(node.left)
            } else if (data > node.data) {
                if (node.right === null) {
                    node.right = new Node(data)
                    return
                }
                return searchTree(node.right)
            } else {
                return null
            }
        }
        return searchTree(current)
    }
}
```

### 삭제
+ 삭제 연산은 3가지 케이스가 있을 수 있다.
    1. 자식 노드가 없을 경우
    2. 자식 노드가 하나 있을 경우
    3. 자식 노드가 두 개 있을 경우

+ 자식 노드가 없을 경우, 그냥 해당 노드 값을 지우면 된다.
+ 자식 노드가 하나 있을 경우, 해당 노드를 지우고 하나 뿐인 자식 노드를 지운 노드의 위치에 바로 연결한다.

    
![image](https://user-images.githubusercontent.com/49611158/146003742-4319ccd2-5124-4c4e-afe7-3dddc4c83489.png)    

+ 자식 노드가 두 개 있을 경우에는 조금 복잡하다.
    - 위 그림에서 중위 순회 순서는 다음과 같다.     
    4 → 10 → 13 → 16 → 20 → 22 → 25 → 28 → 30 → 42
    - 이 때 16 을 삭제한다고 하면, 아래와 같은 대상을 찾아야한다.
        + 삭제 대상 노드의 왼쪽 서브트리 중 최대 값인 predecessor (13)
        + 삭제 대상 노드의 오른쪽 서브트리 중 최소 값인 successor (20)
    - 16 의 위치에 successor 의 값인 20을 복사하고, 20 을 삭제한 뒤 20의 자식노드를 20의 위치에 배치시키면 된다.
    - 혹은 16의 위치에 predecessor 의 값인 13을 복사하고, 13을 삭제한 뒤 13의 자식노드를 13의 위치에 배치시키면 된다.
    - 이진 트리의 구조상, successor 는 자식노드가 하나이거나 하나도 존재하지 않을 것이다.

```javascript
class BST {
    constructor() {
        this.root = null
    }

    /* ..... */

    delete(data) {
        const current = this.root
        const parent = this.root
        const isLeftChild = false
        while (current.data !== data) {
            parent = current
            if (current.data > data) {
                isLeftChild = true
                current = current.left
            } else {
                isLeftChild = false
                current = current.right
            }
            if (current === null) return false
        }
        // 자식이 없는 경우
        if (current.left === null && current.right === null) {
            if (current === root) root = null
            if (isLeftChild) parent.left = null
            else parent.right = null
        }
        // 자식이 한 개인 경우
        else if (current.right === null) {
            if (current === root) root = current.left
            else if (isLeftChild) parent.left = current.left
            else parent.right = current.left
        } else if (current.left === null) {
            if (current === root) root = current.right
            else if (isLeftChild) parent.left = current.right
            else parent.right = current.right
        }
        // 자식이 두 개인 경우
        else if (current.left !== null && current.right !== null) {
            const successor = getSuccessor(current)
            if (current === root) root = successor
            else if (isLeftChild) parent.left = successor
            else parent.right = successor
            successor.left = current.left
        }
        return true
    }

    getSuccessor(node) {
        const successor = null
        const successorParent = null
        const current = node.right
        while (current !== null) {
            successorParent = successor
            successor = current
            current = current.left
        }
        if (successor !== node.right) {
            successorParent.left = successor.right
            successor.right = node.right
        }
        return successor
    }
}
```

<br>

## 균등 트리와 편향 트리, 시간복잡도
+ 균등 트리는 완전 이진 트리와 같은 형태를 뜻한다.
+ 편향 트리는 한 쪽으로만 쏠린 트리와 같은 형태를 뜻한다.
+ 이진 탐색 트리의 핵심 연산들은 트리의 높이 h에 의해 `O(h)` 의 수행시간을 가지게 되므로, 편향 트리와 같이 불균형 트리의 경우에는 시간복잡도가 `O(n)` 까지 하락할 수 있다.
+ 이러한 편향된 트리를 해결하기 위해 이를 개선한 트리인 AVL Tree 나 Red Black Tree 가 등장했다.
    - [Red Black Tree](https://nesoy.github.io/articles/2018-08/Algorithm-RedblackTree)
    - [AVL Tree](https://yoongrammer.tistory.com/72)
