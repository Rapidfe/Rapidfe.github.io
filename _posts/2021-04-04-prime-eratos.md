---
title: 소수 찾기, 에라토스테네스의 체
author: rapidfe
date: 2021-04-04 18:05:00 +0900
categories: [알고리즘 c++, 내용정리]
tags: [수학]
math: true
---

# **내용**

---

에라토스테네스가 고안한 소수를 찾는 방법이다. 대표적인 소수 판별 알고리즘으로 쓰이고 있다.

\\(N\\)이하의 자연수에서 \\(\sqrt N\\)이하의 자연수의 배수를 모두 삭제하여, \\(N\\)이하의 소수를 구하는 방법이다.

![eratos](/assets/img/eratos.png)

#### **왜 \\(\sqrt N\\)까지인가?**

만약 \\(N\\)보다 작은 어떤 합성수 \\(m\\)(삭제해야 할 수)이 \\(m=ab\\\)라면 \\(a\\)와 \\(b\\)중 적어도 하나는 \\(\sqrt m\\)이하이다. 즉 \\(\sqrt N\\)이하 수의 배수만 삭제하면 \\(N\\)이하의 합성수는 모두 삭제된다.



# **구현**

---

{%raw%}

```c++
#include <iostream>

using namespace std;

int arr[101] = {0,};

int main(){
    // 100이하의 소수 구하기
    for(int i=2; i*i<=100; i++){
        if( arr[i]==1 ) continue;
        for(int j=i+i; j<=100; j+=i)
            arr[j] = 1;
    }

    // 출력
    for(int i=1; i<=100; i++)
        if( arr[i]==0 ) cout<<i<<" ";
    return 0;
}
```

{%endraw%}

> [[참고 블로그 1]](https://velog.io/@yuriyaam/%EC%BD%94%EB%94%A9-07.-%EC%86%8C%EC%88%98-%EA%B5%AC%ED%95%98%EA%B8%B0)
>
> [[나무위키]](https://namu.wiki/w/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98%20%EC%B2%B4)

