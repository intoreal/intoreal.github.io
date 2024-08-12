---
layout: post
title: "torch.utils.data.random_split"
date: 2024-08-13 +0900
categories: [python, pytorch]
tags: [python, pythorch]
published: true
author: jihwan
toc: true
---

## 사용 예시

```python
full_dataset = torchvision.datasets.MNIST(root='./dataset/MNIST', download=True, train=True)

train, val, test = torch.utils.data.random_split(full_dataset, [0.7, 0.2, 0.1])
```