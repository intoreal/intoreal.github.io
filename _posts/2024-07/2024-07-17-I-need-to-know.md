---
# 사용할 layout file 지정
layout: post
# 게시글 제목
title: "내가 모르는 것들"
# 게시글 시간 설정. 파일 명 보다 우선한다.
date: 2024-07-17 +0900
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
pin: true
---
## 내가 알아야 할 것들

ㅁ 알아야 할 것
- model = torchvision.models.resnet18(pretrained=True)
  - for param in model.parameters():
  param.requires_grad = False
  - for name, param in model.named_parameters():
  param.requires_grad = False
  - model.fc = nn.Linear(512, 10)
  - for param in model.fc.parameters():
  param.requires_grad = True

  - optim = torch.optim.Adam(model.fc.parameters())

  - transforms.Resize(224), transforms.CenterCorp(224)

  - DataLoader(dataset, batch_size, num_workers, shuffle)

  - glob.glob(pathStr + '*.pth')
  * 반환값은 list?

  - model.load_state.dict(torch.load(model_path))

  - model.eval()

  - with no_grad():

  - preds[preds > = 0.5] = 1

  - preds.eq(labels.cpu()).int().sum()

  - image.clip(0,1), tensor
