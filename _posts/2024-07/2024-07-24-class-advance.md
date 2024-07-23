---
layout: post
title: "클래스를 사용한 유연한 util 사용"
date: 2024-07-24 +0900
categories: [python, basics]
tags: [python]
published: true
author: jihwan
toc: true
---

## util Class 정의

```python
class ImageTransform():
  def __init__(self, resize, mean, std):
    self.data_transform = {
        'train': transforms.Compose([
            transforms.RandomResizedCrop(resize, scale=(0.5, 1.0)),
            transforms.RandomHorizontalFlip(),
            transforms.ToTensor(),
            transforms.Normalize(mean, std)
        ]),
        'val': tranforms.Compose([
            transforms.Resize(256),
            transforms.CenterCrop(resize),
            transforms.ToTensor(),
            transforms.Normalize(mean, std)
        ])
    }
  
  def __call__(self, img, phase):
    return self.data_transform[phase](img)
```

## 사용 코드
```python

for phase in ['train', 'val']:
    transform = ImageTransform(size, mean, std)

    img = []
    img = transform(img, phase)
```