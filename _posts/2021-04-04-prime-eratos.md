---
title: 소수 판별, 에라토스테네스의 체
author: rapidfe
date: 2021-04-04 18:05:00 +0900
categories: [알고리즘 c++, 내용정리]
tags: [수학]
math: true
---

# **개요**

---

에라토스테네스가 고안한 소수를 찾는 방법이다. 대표적인 소수 판별 알고리즘으로 쓰이고 있다.

N이하의 자연수에서 \\(\sqrtN\\)이하의 자연수의 배수를 모두 삭제하여, N이하의 소수를 구하는 방법이다.

![eratos](/assets/img/eratos.png)

#### **왜 \\(\sqrtN\\)까지인가?**

소인수 분해를 생각해 보면 간단하다.



# **풀이**

---

이분탐색을 이용해야 하는 문제다.

#### **풀이 1**

각 블루레이 크기를 작은 것부터 선형적으로 선택하고, 그 크기 안에 담을 레슨 동영상을 이분탐색으로 찾아 해당 크기가 답인지 판단한다. 배열에 누적합을 저장해서 구현했다. 제출 결과 통과는 되었지만 100ms가 넘는 꽤 긴 시간이 측정되었다.

#### **풀이 2**

각 블루레이 크기를 이분탐색으로 선택하고, 그 크기 안에 담을 레슨 동영상을 선형적으로 찾아 해당 크기가 답인지 판단했다. 8ms로 시간이 크게 개선되었다.

#### **알게된 것**

이분탐색은 아직 익숙치 않아서 이번 기회에 기본을 조금 다져보고자 여러 방법으로 풀어봤다. 이분탐색을 이용하려 할 땐 알고리즘을 어떻게 구상해야 할까? 

\\("\\)먼저 무식하게 구상을 해 보고 반복 횟수가 큰 반복문에 이분탐색 사용을 고려해보자.\\(\textrm"\\)

이 문제 같은 경우, 레슨의 총 갯수는 \\(10^5\\)개고 레슨의 총 시간은 \\(10^9\\)개다. 레슨의 갯수는 선형적으로 탐색해도 무방하다. 하지만 각 블루레이의 크기는 최대가 되는 경우가 레슨의 총 시간(\\(10^9\\))이 되는 경우이므로 이분탐색을 적용하는 것이 좋다.

#### **풀이 1) 오답 1**

블루레이의 크기가 가장 긴 레슨의 시간보다 작은 경우를 고려하지 않음.



# **코드**

---

**풀이 1**

{%raw%}

```c++
#include <iostream>
#include <algorithm>

using namespace std;

int N,M,arr[100001], maxi=0;

int bin_search(int left, int size){
    int st=left, right=N,mid;
    while( left<right-1 ){
        mid = (left+right)/2;
        if( arr[mid]-arr[st-1]>size ) right = mid-1;
        else left = mid;
    }
    if( arr[right]-arr[st-1]>size ) return left+1;
    else return right+1;
}

void solution(){
    int idx, ans;
    for(ans=max(arr[N]/M, maxi); ans<arr[N]; ans++){
        idx = 1;
        for(int i=0; i<M; i++) idx = bin_search(idx, ans);
        if( idx==N+1 ) break;
    }
    cout<<ans;
}

int main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cin>>N>>M;
    for(int i=1; i<=N; i++){
        cin>>arr[i];
        maxi = max(maxi, arr[i]);
        arr[i] += arr[i-1];
    }
    solution();
    return 0;
}
```

{%endraw%}

**풀이 2**

{%raw%}

```c++
#include <iostream>
#include <algorithm>

using namespace std;

int N,M,arr[100000], maxi=0;

void solution(){
    int left=1,right=1000000000,mid,sum,idx;
    while( left<=right ){
        mid = (left+right)/2;
        idx = 0;
        for(int i=0; i<M; i++){
            sum = 0;
            for(; idx<N; idx++){
                if( sum+arr[idx]>mid ) break;
                sum += arr[idx];
            }
        }
        if( idx==N ) right = mid-1;
        else left = mid+1;
    }
    cout<<left;
}

int main(){
    ios::sync_with_stdio(false);
    cin.tie(0);
    cin>>N>>M;
    for(int i=0; i<N; i++){
        cin>>arr[i];
        maxi = max(maxi, arr[i]);
    }
    solution();
    return 0;
}
```

{%endraw%}
