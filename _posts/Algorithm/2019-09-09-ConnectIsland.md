---
layout: post
title: 프로그래머스:섬 연결하기
date: 2019-09-09 13:40:00
author: "SeWonKim"
categories: [algorithm]
tags: [jekyll, algorithm, Programmers]
fullview: false
comments: true
description: Programmers Coding Test
---

## Problem

[섬 연결하기](https://programmers.co.kr/learn/courses/30/lessons/42861)

---

## Background Idea

### 신장 트리(Spanning Tree)

그래프의 과점에서 트리는 사이클이 없는 단순 연결 그래프이다.  
n개의 정점으로 이루어진 무방향 그래프에서 n개의 모든 정점과 n-1개의 간선으로 만들어진 트리를 신장 트리라고 한다.

```
신장; 伸長
길이 따위를 길게 늘림.
```

### 신장트리는 최소의 간선을 이용해서 모든 정점을 연결한 그래프!

**가중치의 합이 최소가 되는 신장 트리**를 **최소 비용 신장 트리(Minimum Cost Spanning Tree)**라고 한다.

### 최소 비용 신장 트리를 만드는 방법

1. Kruskal 알고리즘1
2. Kruskal 알고리즘2
3. Prime 알고리즘

### Kruskal 알고리즘1 - 가중치가 가장 큰 간선을 제거하면서...!

1. 모든 간선을 가중치에 따라서 내림차순으로 정리한다.
2. 가장 가중치가 높은 간선을 제거한다. (정점을 그래프에서 분리시키는 간선은 제거할 수 없으므로 그 다음으로 가중치가 높은 간선을 제거한다.)
3. 그래프에 n-1개의 간선만 남을 때까지 2를 반복한다.

### Kruskal 알고리즘2 - 가중치가 가장 작은 간선을 삽입하면서...!

1. 모든 간선을 가중치에 따라서 오름차순으로 정리한다.
2. 가장 가중치가 작은 간선을 삽입한다. (사이클을 형성하는 간선은 삽입할 수 없으므로 그 다음으로 가중치가 작은 간선을 삽입한다.)
3. 그래프에 n-1개의 간선을 삽입할 때까지 2를 반복한다.

### Prime 알고리즘

1. 시작 정점을 선택한다.
2. 선택한 정점에 부속된 모든 간선 중에서 가중치가 가장 작은 간선을 연결하여 트리를 확장한다.
3. 이전에 선택한 정점과 새로 확장된 정점에 부속된 모든 간선 중에서 가중치가 가장 작은 간선을 삽입한다.
4. 그래프에 n-1개의 간선을 삽입할 때까지 3을 반복한다.

## 문제풀이에 적용

문제 풀이에는 Kruskal 알고리즘2를 적용해보았다.  
[알고리즘 구현에 참고한 영상](https://www.youtube.com/watch?v=LQ3JHknGy8c)  
[Union-Find](https://www.youtube.com/watch?v=AMByrd53PHM) 알고리즘을 먼저 구현할 수 있어야 한다.

보통 부모로 합칠 때에는 일반적으로 더 작은 값으로 합치게 된다.
1, 2, 3이 연결되어 있을 때 세 노드의 부모 노드는 모두 1이다. **재귀함수를 사용해서 표현**

🍎 이 문제를 왜 Minimum cost spanning tree로 풀어야해 ?  
n개의 섬을 모든 섬이 통행 가능하도록 할 때 => n개의 섬을 n-1개의 노드로 연결  
그 때 필요한 최소비용 구하기 => 간선의 최소비용을 구하는 것이므로 최소 비용 신장 트리가 적격이다.

1. 간선을 기준으로 오름차순으로 정렬
2. d[i]는 노드 i의 부모 노드를 저장하는 배열
3. 모든 간선을 검사해서 start와 end가 연결되지 않았으면 연결해준다.  
   이 때 오름차순으로 정렬했기 때문에 간선의 최소비용을 구할 수 있다.

---

## Code

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

// mininum cost sapanning tree 만들기
// kruskal algorithm

// d[i] = 노드 i의 부모 노드를 가리킨다.
int d[101];

// 최상위 노드를 찾는 함수 (Union-find)
int getParent(int node){
    if(node == d[node]){
        return node;
    }
    else return d[node] = getParent(d[node]);
}

// 간선의 가중치를 기준으로 오름차순 정렬
bool cmp(const vector<int> &a, const vector<int> &b){
    return a[2] < b[2];
}

int solution(int n, vector<vector<int>> costs) {
    int answer = 0;

    for(int i=0; i<n; i++){
        d[i] = i;
    }

    // 1. 간선의 가중치를 기준으로 오름차순으로 정렬(krustal 2)
    sort(costs.begin(), costs.end(), cmp);


    // 2. 모든 간선을 검사
    for(int i=0; i<costs.size(); i++){
        int start = getParent(costs[i][0]);
        int end = getParent(costs[i][1]);
        int cost = costs[i][2];

        // start와 end가 아직 연결되지 않았을 때
        if(start != end){
            // start를 end의 parent로 설정
            d[start] = end;

            // 간선 가중치 값 더해주기
            answer += cost;
        }

    }

    return answer;
}
```

## Review

자료구조 과목에서 분명히 신장 트리, 최소 비용 신장 트리에 대해서 배웠는데... 전혀 생각이 안난다. 마치 처음 배우는 듯 하다.  
크루스칼 알고리즘도 너무나 생소하다. 책에는 막 밑줄도 쳐져있는데?! 아무튼... 이번 기회에 다시 복습의 시간을 가질 수 있어 다행이라고 생각한다 ^^...!
