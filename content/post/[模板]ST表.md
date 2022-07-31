---
title: "[模板]ST表"
date: 2022-07-27T08:53:27+08:00
draft: false
categories:	[模板]
tags: [数据结构]
image: "img/7.jpg"
---

```cpp
void log_init() {
    logn[1] = 0;
    logn[2] = 1;
    for (int i = 3; i <= n; i++) logn[i] = logn[i / 2] + 1;
}

void rmq_init() {
    for (int i = 1; i <= n; i++) f[i][0] = a[i];
    for (int j = 1; j <= LOGN; j++)
        for (int i = n; i >= 1; i--)
            if (i + (1 << (j - 1)) <= n)
                f[i][j] = max(f[i][j - 1], f[i + (1 << (j - 1))][j - 1]);
}

int rmq(int l, int r) {
    int k = logn[r - l + 1];
    return max(f[l][k], f[r - (1 << k) + 1][k]);
}
```

