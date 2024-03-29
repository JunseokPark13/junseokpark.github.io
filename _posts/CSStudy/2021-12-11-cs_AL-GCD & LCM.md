---
title: '[CS] 알고리즘 - GCD & LCM'
author: Bandito
date: 2021-12-11 21:30:00 +0900
categories: [Study, CS]
tags: [CS, Computer Sceince]
comment: true
---

# GCD & LCM

최대공약수와 최소공배수를 사용해야하는 문제가 가끔 등장하는데, 항상 정확한 코드가 생각이 바로바로 나질 않아 조금 고생을 했다.    

이번 기회에 이를 정리해두고자 한다.


## GCD (Greatest Common Divisor)
+ N 개의 숫자들에 대해서 A 로 나누었을 때 나머지가 0일 경우, 이 A를 공약수라고 한다.
+ GCM 은 최대공약수라는 의미로, N 개의 숫자들에 대해 나올 수 있는 공약수 중 가장 큰 것을 의미한다.
+ 최대공약수는 단순히 N 개의 숫자들의 약수를 나열하여 찾을 수도 있지만, 유클리드 호제법이라는 쉬운 방법이 존재한다.

### 유클리드 호제법
+ 두 양의 정수 a, b (a > b)에 대해,`a = b * q + r  (0 <= r < b)`라 하면,      
a, b의 최대공약수는 b, r의 최대 공약수와 같다.
+ 즉, `gcd(a, b) = gcd(b, r)` 이고, r = 0 이면 최대 공약수는 b 가 된다.    
결론적으로 r = 0 이 나올 때 까지 이를 계속 반복하면 최대공약수를 구할 수 있다.

```javascript
// 두 수 a, b 에 대한 GCD 을 구하는 함수
function GCD(a, b) {
    const r = a % b
    if (r === 0) return b   // r === 0 이면 b 를 반환
    return GCD(b, r)        // 아니라면 GCD(a, b) = GCD(b, r) 이므로 
                            // b, r 에 대해 다시 GCD 을 구한다.
}
```

<br>

```javascript
// N개의 수에 대하여 에 대한 GCD 을 구하는 함수
function nGCD(ary) {
    let gcd = ary[0]
    for(let i = 1; i < ary.length; i++) {
        gcd = GCD(gcd, ary[i])  // 2개의 수에 대해 gcd를 구한 뒤
    }                           // 해당 gcd와 다음 수에 대한 gcd를 구한다
    return gcd
}
```


## LCM (Least Common Multiple)
+ N 개의 숫자들에 대해 배수를 취했을 때 같은 수 A 가 나온다면 이를 공배수라고 한다.
+ LCM 은 최대 공배수라는 의미로, N 개의 숫자들에 대해 나올 수 있는 공배수 중 가장 작은 것을 의미한다.
+ 최대공배수를 구하기 위해서는 소인수분해를 사용할 수도 있다.    
각 수를 소인수분해하고, 최대 지수를 구하여 곱하면 된다.

```
12, 54 의 최소공배수는
12 = 2^2 * 3
54 = 2 * 3^3

이 중에서 2의 최대 지수는 2, 3의 최대 지수는 3이다.
그러므로 2^2 * 3^3 = 108 이 12 와 54의 최소공배수이다.
```

+ 최대공약수를 알고 있다면 좀 더 간편하게 구할 수 있다.

```
12, 54 의 최대공약수는 6이다.
12 와 54를 곱하고 이를 최대공약수인 6 으로 나눈다면
12 * 54 / 6 = 108 을 구할 수 있다.
```

<br>

```javascript
// 두 수 a, b 에 대한 LCM 을 구하는 함수
function LCM(n1, n2) {
    return n1 * n2 / GCD(n1, n2)
}
```

```javascript
// N개의 수에 대하여 에 대한 LCM 을 구하는 함수
function nLCM(ary) {
    let lcm = ary[0]
    for(let i = 1; i < ary.length; i++) {
        lcm = LCM(lcm, ary[i])  // 상단의 nGCD와 2개에 대한 최소공배수를 구하고
    }                           // 다시 다음 수와 함께 최소공배수를 구한다.
    return lcm                  
}
```