---
title: "洛谷P1347 排序"
date: 2022-08-28T14:49:49+08:00
draft: false
categories:	[题解]
tags: [图论]
image: "cover/30.png"
---

# 排序

## 题目描述

一个不同的值的升序排序数列指的是一个从左到右元素依次增大的序列，例如，一个有序的数列 $A,B,C,D$ 表示$A<B,B<C,C<D$。在这道题中，我们将给你一系列形如 $A<B$ 的关系，并要求你判断是否能够根据这些关系确定这个数列的顺序。

## 输入格式

第一行有两个正整数 $n,m$，$n$ 表示需要排序的元素数量，$2\leq n\leq 26$，第 $1$ 到 $n$ 个元素将用大写的 $A,B,C,D\dots$ 表示。$m$ 表示将给出的形如 $A<B$ 的关系的数量。

接下来有 $m$ 行，每行有 $3$ 个字符，分别为一个大写字母，一个 `<` 符号，一个大写字母，表示两个元素之间的关系。

## 输出格式

若根据前 $x$ 个关系即可确定这 $n$ 个元素的顺序 `yyy..y`（如 `ABC`），输出

`Sorted sequence determined after xxx relations: yyy...y`.

若根据前 $x$ 个关系即发现存在矛盾（如 $A<B,B<C,C<A$），输出

`Inconsistency found after x relations.`

若根据这 $m$ 个关系无法确定这 $n$ 个元素的顺序，输出

`Sorted sequence cannot be determined.`

（提示：确定 $n$ 个元素的顺序后即可结束程序，可以不用考虑确定顺序之后出现矛盾的情况）

## 样例 #1

### 样例输入 #1

```
4 6
A<B
A<C
B<C
C<D
B<D
A<B
```

### 样例输出 #1

```
Sorted sequence determined after 4 relations: ABCD.
```

## 样例 #2

### 样例输入 #2

```
3 2
A<B
B<A
```

### 样例输出 #2

```
Inconsistency found after 2 relations.
```

## 样例 #3

### 样例输入 #3

```
26 1
A<Z
```

### 样例输出 #3

```
Sorted sequence cannot be determined.
```

## 提示

$2 \leq n \leq 26,1 \leq m \leq 600$。

## 题解

拓扑排序

输入 $A \lt B$, 建一条边 $A → B$, 每次都进行拓扑排序

当 dfs 到一个点时, 将其 $color$ 设为 $1$ (若 $color$ 已经为 $1$, 说明存在矛盾), 当这个点 dfs 结束时, 将 $color$ 设为 $2$

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
typedef double db;
typedef pair<int, int> pii;
typedef pair<long long, long long> pll;
typedef vector<int> vi;
typedef vector<long long> vll;
typedef vector<pii> vpii;
typedef vector<pll> vpll;

const int N = 110, MOD = 1e9 + 7, INF = 0x3f3f3f3f;
int n, m, t, color[N];
char a, b, tmp;
vi g[N], order;
bool vis[N];

void dfs(int u) {
    color[u] = 1;
    for (auto v : g[u]) {
        if (color[v] == 1) {
            printf("Inconsistency found after %d relations.", t);
            exit(0);
        }
        if (color[v] == 0) dfs(v);
    }
    color[u] = 2;
    order.push_back(u);
}

int main() {
#ifndef ONLINE_JUDGE
    freopen("data/in.txt", "r", stdin);
    freopen("data/out.txt", "w", stdout);
#endif
    cin >> n >> m;
    for (t = 1; t <= m; t++) {
        cin >> a >> tmp >> b;
        g[a - 'A'].push_back(b - 'A');

        memset(color, 0, sizeof(color));
        order.clear();
        int cnt = 0;
        for (int i = 0; i < n; i++)
            if (!color[i]) dfs(i), cnt++;
        if (cnt > 1) continue;
        if (order.size() == n) {
            printf("Sorted sequence determined after %d relations: ", t);
            for (int i = order.size() - 1; i >= 0; i--)
                printf("%c", order[i] + 'A');
            printf(".");
            return 0;
        }
    }
    printf("Sorted sequence cannot be determined.");
    return 0;
}
```

