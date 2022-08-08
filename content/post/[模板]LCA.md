---
title: "[模板]LCA"
date: 2022-07-27T08:50:36+08:00
draft: false
categories:	[模板]
tags: [数据结构]
image: "cover/10.jpg"
---

```cpp
void dfs(int x, int d) {
    dep[x] = d;
    for (int i = 0; i < g[x].size(); i++) {
        if (g[x][i] != fa[x][0]) {
            fa[g[x][i]][0] = x;
            dfs(g[x][i], d + 1);
        }
    }
}

void lca_init() {
    for (int j = 1; j <= 20; j++)
        for (int i = 1; i <= n; i++)
            if (fa[i][j - 1] && fa[fa[i][j - 1]][j - 1])
                fa[i][j] = fa[fa[i][j - 1]][j - 1];
}

int lca(int x, int y) {
    if (dep[x] < dep[y]) swap(x, y);
    for (int i = 20; i >= 0; i--)
        if (fa[x][i] && dep[fa[x][i]] >= dep[y]) x = fa[x][i];
    if (x == y) return x;
    for (int i = 20; i >= 0; i--)
        if (fa[x][i] && fa[y][i] && fa[x][i] != fa[y][i])
            x = fa[x][i], y = fa[y][i];
    return fa[x][0];
}
```

