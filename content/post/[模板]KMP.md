---
title: "[模板]KMP"
date: 2022-07-27T10:11:53+08:00
draft: false
categories:	[模板]
tags: [字符串]
image: "cover/6.jpg"
---

```cpp
vi pre(string s) {
    int n = s.size();
    vi nxt(n);
    for (int i = 1; i < n; i++) {
        int j = nxt[i - 1];
        while (j > 0 && s[j] != s[i]) j = nxt[j - 1];
        if (s[i] == s[j]) j++;
        nxt[i] = j;
    }
    return nxt;
}
```