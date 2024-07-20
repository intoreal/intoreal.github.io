---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "CNN 모델 구성 예시"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-07-15 +0900
# 게시글의 카테고리. 최상단과 서브 카테고리만 있다.
categories: [python, pytorch]
# 게시글 태그 설정. ,로 태그들을 구분해서 작성 가능하다.
tags: [pytorch]
# 공개여부 설정. true면 공개하고 false면 공개하지 않는다.
published: true
# 사용자 정의 변수. 본문에서 {{ page. food }} 형태로 사용 가능하다.
author: jihwan
# 만약 우측 Table Of Contents를 사용하고 싶지 않다면 false로 전환
toc: true
---

## 환경설정 및 데이터 준비
```python
import torch

device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")

from torchvision import datasets, transforms
from torch.utils.data import DataLoader

train_dataset = datasets.CIFAR10(root='./work/CIFAR10', train=True, download=True, transform = transforms.ToTensor())
test_dataset = datasets.CIFAR10(root='./work/CIFAR10', train=False, download=True, transform = transforms.ToTensor())

train_loader = DataLoader(train_dataset, batch_size= 100)
test_loader = DataLoader(test_dataset, batch_size=100)


```

## CNN 모델 구성
```python
# 모델 구성
import torch.nn as nn
import torch.nn.functional as F

class Cifar10CNN(nn.Module):
  def __init__(self):
    super().__init__()
    self.layer1 = nn.Sequential(
        nn.Conv2d(in_channels=3, out_channels=128, kernel_size=3),
        nn.BatchNorm2d(128),
        nn.ReLU(),
        nn.MaxPool2d(kernel_size=2, stride=2)
    ) # 128 x 15 x 15
    self.layer2 = nn.Sequential(
        nn.Conv2d(in_channels=128, out_channels=64, kernel_size=5, padding=2),
        nn.Conv2d(in_channels=64, out_channels=64, kernel_size=5, padding=2),
        nn.BatchNorm2d(64), 
        nn.ReLU(),
        nn.MaxPool2d(kernel_size=3, stride = 1, padding=1)
    ) # 64 x 15 x 15
    self.fc1 = nn.Linear(64 * 15 * 15, 512)
    self.drop = nn.Dropout(0.2)
    self.fc2 = nn.Linear(512, 128)
    self.fc3 = nn.Linear(128, 10)
  
  def forward(self, input_data):
    out = input_data.view(-1, 3, 32,32)
    # print("1", out.shape)
    out = self.layer1(out)
    # print("2", out.shape)
    out = self.layer2(out)
    # print("3", out.shape)
    out = out.view(out.size(0), -1)

    out = self.fc1(out)
    # print("4", out.shape)
    out = self.drop(out)
    out = self.fc2(out)
    out = self.fc3(out)
    return out
```
## 모델 생성
```python
model = Cifar10CNN()
model = model.to(device)

```

## 손실함수 및 최적화 함수 설정
```python
creterion = nn.CrossEntropyLoss()
optim = torch.optim.Adam(model.parameters(), lr= 0.001)

```

## 미니배치 단위 학습
```python
# 미니배치 단위 학습
for epoch in range(10):
  for imgs, labels in train_loader:
    imgs, labels = imgs.to(device), labels.to(device)
    # print(imgs.shape)

    # Forward pass
    pred = model(imgs)
    loss = creterion(pred, labels)

    # Backward pass
    optim.zero_grad()
    loss.backward()
    optim.step()
  
  score = 0
  for imgs, labels in test_loader:
    imgs, labels = imgs.to(device), labels.to(device)

    # Forward pass
    pred = model(imgs)
    pred = torch.max(pred, dim=1)[1]

    score += (pred == labels).sum()
  print(f"Accuracy : {score/len(test_dataset)}")



```
