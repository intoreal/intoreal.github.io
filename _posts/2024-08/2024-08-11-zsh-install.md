---
layout: post
title: "zsh 설치 방법"
date: 2024-08-11 +0900
categories: [Linux, zsh]
tags: [linux, ubuntu, zsh]
published: true
author: jihwan
toc: true
---

## 1. zsh 설치
```bash
sudo apt install zsh
```

## 2. oh-my-zsh 설치
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```


## 3. 플러그인 설치
### (1) Auto Suggestions
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# ~/.zshrc 파일 plugin 리스트에 zsh-autosuggestions 추가
```

### (2) Syntax Highlighting
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
 
# ~/.zshrc 파일 plugin 리스트에 zsh-syntax-highlighting 추가
```

### (3) Autojump
- 파이썬 설치 필요
```bash
git clone git://github.com/wting/autojump.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/autojump

cd autojump
./install.py or ./uninstall.py
```