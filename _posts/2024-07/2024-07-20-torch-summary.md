---
layout: post
title: "파이썬 모듈을 확인하는 torch summary"
date: 2024-07-20 +0900
categories: [python, pytorch]
tags: [python, torchsummary]
published: true
author: jihwan
toc: true
---

## 개요
- pytorch 모델을 Keras와 같은 형태로 출력한다. 


## 사용방법
### 패키지 다운로드
```bash
pip install torchsummary
```

### 사용 코드
```python
from torchsummary import summary

summary(model.to(device), input_size=(3, 224, 224))
```

### 결과물
```text
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1         [-1, 16, 220, 220]           1,216
              ReLU-2         [-1, 16, 220, 220]               0
         MaxPool2d-3         [-1, 16, 110, 110]               0
            Conv2d-4         [-1, 32, 106, 106]          12,832
              ReLU-5         [-1, 32, 106, 106]               0
         MaxPool2d-6           [-1, 32, 53, 53]               0
            Linear-7                  [-1, 512]      46,023,168
            Linear-8                    [-1, 2]           1,026
           Softmax-9                    [-1, 2]               0
================================================================
Total params: 46,038,242
Trainable params: 46,038,242
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.57
Forward/backward pass size (MB): 19.47
Params size (MB): 175.62
Estimated Total Size (MB): 195.67
----------------------------------------------------------------
```

## 더 좋은 대안 torchinfo
### 패키지 다운로드
```bash
!pip install torchinfo
```

### 코드
```python
from torchinfo import summary
summary(model, input_size=(1,3,224,224))
```

### 결과물
```text
==========================================================================================
Layer (type:depth-idx)                   Output Shape              Param #
==========================================================================================
LeNet                                    [1, 2]                    --
├─Conv2d: 1-1                            [1, 16, 220, 220]         1,216
├─ReLU: 1-2                              [1, 16, 220, 220]         --
├─MaxPool2d: 1-3                         [1, 16, 110, 110]         --
├─Conv2d: 1-4                            [1, 32, 106, 106]         12,832
├─ReLU: 1-5                              [1, 32, 106, 106]         --
├─MaxPool2d: 1-6                         [1, 32, 53, 53]           --
├─Linear: 1-7                            [1, 512]                  46,023,168
├─ReLU: 1-8                              [1, 512]                  --
├─Linear: 1-9                            [1, 2]                    1,026
├─Softmax: 1-10                          [1, 2]                    --
==========================================================================================
Total params: 46,038,242
Trainable params: 46,038,242
Non-trainable params: 0
Total mult-adds (Units.MEGABYTES): 249.06
==========================================================================================
Input size (MB): 0.60
Forward/backward pass size (MB): 9.08
Params size (MB): 184.15
Estimated Total Size (MB): 193.83
==========================================================================================

```