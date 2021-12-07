---
title: "[HackerRank][Javascript] Forming a Magic Square"
author: Bandito
date: 2021-12-07 23:30:00 +0900
categories: [Study, HackerRank]
tags: [Algorithm, HackerRank, Javascript]
comment: true
---

# HackerRank - Forming a Magic Square

---

### 문제 링크 : <https://www.hackerrank.com/challenges/magic-square-forming>

---

<br/>

## 문제

---

```
We define a magic square to be an 'n x n'  matrix of distinct positive integers from '1 to n^2' where the sum of any row, column, or diagonal of length 'n' is always equal to the same number: the magic constant.

You will be given a '3 x 3' matrix 's' of integers in the inclusive range [1, 9]. We can convert any digit 'a' to any other digit 'b' in the range [1,9] at cost of |a - b|. Given 's', convert it into a magic square at minimal cost. Print this cost on a new line.
```

<br>

1 부터 9 까지만 들어갈 수 있는 3 x 3 마방진을 만들어야 한다.    

주어진 3 x 3 배열에서 특정 값 a 를 b 로 바꾸면 이를 바꾼 비용은 |a - b| 가 된다.    

마방진을 만들 수 있는 가장 최소 비용의 합을 구하여라

<br/>
<br/>

Example :

```
Input: 
5 3 4
1 5 8
6 4 2

=>
8 3 4
1 5 9
6 7 2

[0, 0] 에서 |5 - 8| = 3
[1, 2] 에서 |8 - 9| = 1
[2, 1] 에서 |4 - 7| = 3

3 + 1 + 3 = 7
```


 
<br/>

## 제한사항

- 1 <= s[i][j] <= 9

<br/>
<br/>

## 내 풀이

---

처음에는 이걸 어떻게 비교해줘야하나 고민이 많았다. 3x3 크기이니까 일단 모든 방향으로 더하여 근사치를 구하고 필요한 부분을 바꿀까도 생각해봤지만 아무리봐도 경우의 수가 너무 많아보였다.    

마방진이라는 개념 자체는 잘 알고있었지만, 놓치고 있는 점이 있을까 하여 1~9가 들어갈 수 있는 마방진에 대해 찾아봤는데, 1~9로 만들 수 있는 3x3 크기의 마방진은 오직 8개의 경우밖에 나오지 않는다는 점을 알았다.   

그것도 하나의 케이스에 대해서 회전하거나 대칭하였을 뿐이었다. 이렇게 된 이상 가장 빠른 방법은 이미 알고있는 케이스들을 가지고 비교하는 것 같았다.   

문제를 풀고 나니 실제로도 그게 가장 정석적인 풀이 같았다.   


<br>


+ Solution 

```javascript
function formingMagicSquare(s) {
    const allCase = [
        [[8, 3, 4], [1, 5, 9], [6, 7, 2]],
        [[6, 1, 8], [7, 5, 3], [2, 9, 4]],
        [[2, 7, 6], [9, 5, 1], [4, 3, 8]],
        [[4, 9, 2], [3, 5, 7], [8, 1, 6]],
        [[4, 3, 8], [9, 5, 1], [2, 7, 6]],
        [[2, 9, 4], [7, 5, 3], [6, 1, 8]],
        [[6, 7, 2], [1, 5, 9], [8, 3, 4]],
        [[8, 1, 6], [3, 5, 7], [4, 9, 2]]
    ]
    let min = Infinity
    for(let c of allCase) {
        let diff = 0
        for(let i in s) {
            diff += s[i].reduce((acc, val, idx) => {
                acc += Math.abs(val - c[i][idx])
                return acc
            }, 0)
        }
        if (diff < min) min = diff 
    }
    return min
}

```

<br>

1. 문제의 조건에 맞는 모든 마방진 케이스를 `allCase` 라는 배열에 넣어둔다.
2. 주어진 배열 `s` 와 `allCase` 의 케이스들을 하나씩 비교한다.   
  + 각 케이스들과의 자릿수 차이를 모두 `diff` 라는 변수에 저장한다.
  + 현재 `min` 보다 `diff` 가 작다면, `min` 을 `diff` 로 갱신한다.
3. `min` 을 반환한다.


<br>


## 소감

---

푸는 방법만 안다면, 풀이 자체는 굉장히 별거 없는 문제였지만... 케이스가 이렇게 적다는걸 알았다면 더 빠르게 풀 수 있었을 텐데, 아쉽다.   

사실 아직도 이렇게 푸는게 가장 적합한 풀이라는게 조금 싱숭생숭하다.    