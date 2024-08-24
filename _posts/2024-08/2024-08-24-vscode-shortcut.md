---
layout: post
title: "VSCode 키보드 단축키"
date: 2024-08-24 +0900
categories: [IDE, vscode]
tags: [vscode, shortcut]
published: true
author: jihwan
toc: true
---

## 유용한 단축키
* ctrl + shift + e : Explorer 탭으로 이동
* ctrl + shift + e : Explorer 탭으로 이동
* ctrl + b : 사이트 패널 닫기

* ctrl + pageUp/pageDown : 탭 이동
* ctrl + w : 탭 닫기

* ctrl + ` : 터미널 열기/닫기



## 새로 설정해야 할 단축키

`ctrl+shift+p`를 누른 후 *Preferences: Open Keyboard Shortcuts(JSON)* 선택
JSON 파일에 아래 내용 추가(window 기준)
```json
// Place your key bindings in this file to override the defaults
[
  {
    "key": "ctrl+n",
    "command": "explorer.newFile",
    "when": "explorerViewletFocus"
  },
  {
    "key": "ctrl+shift+n",
    "command": "explorer.newFolder",
    "when": "explorerViewletFocus"
  },
]
```