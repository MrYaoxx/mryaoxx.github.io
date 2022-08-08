---
title: "「REOI-1」深潜的第六兽"
date: 2022-08-08T16:46:04+08:00
draft: false
categories:	[题解]
tags: [线段树]
image: "cover/24.jpg"
---

# [「REOI-1」深潜的第六兽](https://www.luogu.com.cn/problem/P8463)

## 题目背景

“〈十七兽〉全都不会飞。因此，在它们毁灭大地以后，悬浮大陆群还能像这样浮在天空。

“可是，只有〈深潜的第六兽〉在本身留在大地的同时，还能对悬浮大陆群发动攻击。它有两种能力，『分裂增生』和『快速茁壮』。

“留在地表的本体会让身体分裂出几万个碎块，然后随风飞扬，等待碰巧飘流到某座悬浮岛。抵达岛上以后，它会当场发育茁壮，大约六到八小时过后就能占据并毁灭整座岛。”

## 题目描述

现在有一只〈第六兽〉，在某一次的「分裂增生」时分裂出了 $n$ 个碎块，这些碎块会笔直向上飞去，如果其中一块碎块遇到了一座浮空岛（为了研究方便，我们不妨将它当成一条二维空间中的线段处理），便会迅速占据它，并一分为二，再次从浮空岛的两端笔直向上飞去。

不过好在，那些只是一些无关紧要最为荒凉毫无人烟的岛屿，但如果就这样放任它们继续肆虐，势必会给那些至关重要的浮空岛带来毁灭性的打击。于是乎，负责清理〈第六兽〉的军官们，决定以他们所在的岛屿为直线建立 $x$ 轴，并以重力的方向为正方向建立 $y$ 轴，他们总共监测到了 $m$ 座浮空岛，并确定了那些碎块分裂出的位置（距离 $x$ 轴的位置视作无限远），于是他们想知道，如果放任这些碎块，那么当它们到达军官的位置时，最终会有多少碎块。

注意，若一座浮空岛的 $ l_i $ 与 $ r_i $ 相同，即为一个点， 〈第六兽〉占据后仍然会分裂成两只，从这个点向上飞去。

**提示：浮空岛作为实体显然不会重叠。**

**简要题意：**

在一个平面直角坐标系上有 $m$ 条平行于 x 轴的线段，第 $i$ 条线段为 $(l_i,h_i)$ 与 $(r_i,h_i)$ 的连线。特别注意 $l_i$ 可与 $r_i$ 相等，此时线段变为一个点。

在直线 $y=10^9$ 上有 $n$ 个点，分别位于 $(x_i,10^9)$。

现在，x 轴上这些点逐渐向下（y轴负方向）移动。若触碰到线段，则会一分为二，分裂出的两个点分别从线段的两端继续向下移动。

特别地，若线段为一个点，则会原地分裂成 2 个。

问所有初始点在经历了线段的分裂后，在最后会有多少个点掉在 $ x $ 轴上

## 输入格式

第一行输入两个数 $ n $ 和 $ m $。

接下来 $ m $ 行，每行三个数 $ l_i $ , $ r_i $ , $ h_i $ ,分别描述一座被视作线段的浮空岛的左端点横坐标，右端点横坐标，以及线段的纵坐标（ $ 0 \leq l_i,r_i,h_i \leq 10^5，l_i \leq r_i$）。

接下来一行 $ n $ 个数，$ x_i $表示第 $ i $ 个碎块的横坐标（ $ 0 \leq x_i \leq 10^5 $）。

## 输出格式

输出一个整数 $ ans $ ，表示最后会有多少个碎块落在 $ x $ 轴上，答案对 $998244353$ 取模。

## 样例 #1

### 样例输入 #1

```
2 2
1 3 2
2 6 1
3 5
```

### 样例输出 #1

```
5
```

## 提示

样例解释：

注意， $y$ 轴正方向为重力方向。
在坐标轴中，横坐标为 $x$ 的碎块，先掉到纵坐标为2的线段上，然后分成两个从 $1$ 和 $3$ 往下掉，$3$ 的那个掉到了纵坐标为1的线段上，分成两个从 $2$ 和 $6$ 往下掉，第一个碎块一共变成了 $3$ 块，分别掉在 $1，2，6$ ，第二个碎块一共变成了两个碎块，分别掉在 $2，6$。

| 子问题 | 特殊限制条件 | 分值 |
| :-----------: | :-----------: | :-----------: |
| 1 | $ 1\leq n,m \leq 10 $ | 10 |
| 2 | $ 1\leq n,m \leq 100 $ | 5 |
| 3 | $ 1\leq n\leq 10^4， 1\leq m \leq 5\times 10^5 $ | 35 |
| 4 |$ 1\leq n,m \leq 5\times 10^5 $|50|

本题各个子问题之间不捆绑测试。

对于 $100\%$ 的数据 $ 1\leq n,m \leq 5\times 10^5 $，所有数字均为非负整数。


## 题解

线段树模板题 (我太弱了, 比赛时调了两小时都没找到bug)

```
若触碰到线段，则会一分为二，分裂出的两个点分别从线段的两端继续向下移动。
```

这句话的意思就是 $:$
首先, 统计线段上有多少个点, 并将这些点删除, 最后在线段两端加上这些点的数量

可以用区间修改, 区间查询的线段树维护

### 第一步: 将岛屿按高度排序

### 第二步: 线段树维护

定义两个 $LazyTag$

+ $ad[] : $ 加

+ $cl[] : $ 区间是否清空


## Code

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

const int N = 500010, MOD = 998244353, INF = 0x3f3f3f3f;
int n, m, max_x;
ll q[N], sum[4 * N], ad[4 * N], ans;
bool cl[4 * N];
struct {
    int l, r;
} p[4 * N];
struct island {
    int l, r, h;

    bool operator<(const island a) { return h > a.h; }
} a[N];

void up(int x) { sum[x] = (sum[x << 1] + sum[(x << 1) + 1]) % MOD; }

void change(int x, ll k, bool c) {
    cl[x] = c;
    if (!c) {
        sum[x] = (sum[x] + k * (p[x].r - p[x].l + 1)) % MOD;
        ad[x] = (ad[x] + k) % MOD;
    } else {
        sum[x] = 0;
        ad[x] = 0;
    }
}

void down(int x) {
    if (ad[x] || cl[x]) {
        change(x << 1, ad[x], cl[x]);
        change((x << 1) + 1, ad[x], cl[x]);
        ad[x] = 0;
        cl[x] = false;
    }
}

void build(int x, int l, int r) {
    p[x].l = l;
    p[x].r = r;
    if (l == r) {
        sum[x] = q[l];
        return;
    }
    int mid = (l + r) >> 1;
    down(x);
    if (l <= mid) build(x << 1, l, mid);
    if (mid < r) build((x << 1) + 1, mid + 1, r);
    up(x);
}

void insert(int x, int l, int r, int L, int R, ll k, bool c) {
    if (r < L || l > R) return;
    if (L <= l && r <= R) {
        change(x, k, c);
        return;
    }
    int mid = (l + r) >> 1;
    down(x);
    if (l <= mid) insert(x << 1, l, mid, L, R, k, c);
    if (mid < r) insert((x << 1) + 1, mid + 1, r, L, R, k, c);
    up(x);
}

void query(int x, int l, int r, int L, int R) {
    if (r < L || l > R) return;
    if (L <= l && r <= R) {
        if (!cl[x]) ans = (ans + sum[x]) % MOD;
        return;
    }
    int mid = (l + r) >> 1;
    down(x);
    if (l <= mid) query(x << 1, l, mid, L, R);
    if (mid < r) query((x << 1) + 1, mid + 1, r, L, R);
    up(x);
}

int main() {
#ifndef ONLINE_JUDGE
    freopen("data/in.txt", "r", stdin);
    freopen("data/out.txt", "w", stdout);
#endif
    ios::sync_with_stdio(false);
    cin >> n >> m;
    for (int i = 1; i <= m; i++)
        cin >> a[i].l >> a[i].r >> a[i].h, max_x = max(a[i].r, max_x);
    for (int i = 1; i <= n; i++) {
        int x;
        cin >> x;
        q[x]++;
        max_x = max(max_x, x);
    }
    sort(a + 1, a + m + 1);
    build(1, 1, max_x);
    for (int i = 1; i <= m; i++) {
        ans = 0;
        query(1, 1, max_x, a[i].l, a[i].r);
        insert(1, 1, max_x, a[i].l, a[i].r, 0, true);
        insert(1, 1, max_x, a[i].l, a[i].l, ans, false);
        insert(1, 1, max_x, a[i].r, a[i].r, ans, false);
    }
    ans = 0;
    query(1, 1, max_x, 1, max_x);
    cout << ans;
    return 0;
}
```
