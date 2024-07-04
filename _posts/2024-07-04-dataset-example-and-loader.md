---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "torchvision dataset과 DataLoader 사용법"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-07-04 +0900
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [pytorch, torchvision]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [python, pytorch, torchvision, mnist, dataloader]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
---

## 패키지 import
```python
import torch
from torhvision import datasets, transforms
import matplotlib.pyplot as plt
```
## MNIST 데이터 사용
```python
mnist_dataset = datasets.MNIST(root='./data', train=True, transform=transforms.ToTensor(), download=True)

# 데이터 직접 읽기
plt.figure(figsize=(5,4))
for i in range(4):
  img, label = mnist_dataset[i]
  plt.subplot(2,2, i +1);
  plt.title(f"Label: {label}") 
  plt.imshow(img.permute(1,2,0))
plt.show()

# DataLoader 사용
data_loader = torch.utils.data.DataLoader(mnist_dataset, batch_size=16, shuffle=True)
for imgs, labels in data_loader:
  plt.figure(figsize=(6,7))
  plt.subplots_adjust(hspace=0.5)
  for i, (img, label) in enumerate(zip(imgs, labels)):
    plt.subplot(4,4, i+1)
    plt.imshow(img.permute(1,2,0))
    plt.title(f"Label: {label}")
  plt.show()
  break
```

## CIFAR-10 데이터 사용
```python
cifar_dataset = datasets.CIFAR10(root='./data', download=True, train=True, transform=transforms.ToTensor())

# 데이터 바로 읽기
plt.figure(figsize=(5,4))
for i in range(4):
  img, label = cifar_dataset[i]
  plt.subplot(2,2,i+1)
  plt.title(f"Label: {label}")
  plt.imshow(img.permute(1,2,0))
plt.show()

# DataLoader 사용
data_loader = torch.utils.data.DataLoader(cifar_dataset, batch_size=16, shuffle=True)
for imgs, labels in data_loader:
  plt.figure(figsize=(6,7))
  plt.subplots_adjust(hspace=0.5)
  for i, (img, label) in enumerate(zip(imgs, labels)):
    plt.subplot(4,4,i+1)
    plt.imshow(img.permute(1,2,0))
    plt.title(f"Label: {label}")
  plt.show()
  break
```

## fashion_MNIST 데이터 사용
```python
fashion_dataset = datasets.FashionMNIST(root='./data', train=True, download=True, transform=transforms.ToTensor())

# 데이터 바로 읽기
plt.figure(figsize=(5,4))
for i in range(4):
  img, label = fashion_dataset[i]
  plt.subplot(2,2,i+1)
  plt.title(f"Label: {label}")
  plt.imshow(img.permute(1,2,0))
plt.show()

# DataLoader 사용
data_loader = torch.utils.data.DataLoader(fashion_dataset, batch_size=16, shuffle=True)
for imgs, labels in data_loader:
  plt.figure(figsize=(6,7))
  plt.subplots_adjust(hspace=0.5)
  for i, (img, label) in enumerate(zip(imgs, labels)):
    plt.subplot(4,4,i+1)
    plt.imshow(img.permute(1,2,0))
    plt.title(f"Label: {label}")
  plt.show()
  break
```
