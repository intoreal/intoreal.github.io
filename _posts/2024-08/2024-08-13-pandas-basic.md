---
layout: post
title: "판다스(pandas) 아주 기초"
date: 2024-08-13 +0900
categories: [python, pandas]
tags: [python, pandas]
published: true
author: jihwan
toc: true
---

## DataFrame의 생성

```python 
import pandas as pd

frame = pd.DataFrame({
    'id': [1,2,3,4],
    'name' : ['a', 'b', 'c', 'd'],
    'age' : [11,22,33,44]
})

print(frame)
#    id name  age
# 0   1    a   11
# 1   2    b   22
# 2   3    c   33
# 3   4    d   44
```
