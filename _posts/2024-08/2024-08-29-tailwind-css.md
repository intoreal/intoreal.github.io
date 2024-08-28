---
layout: post
title: "Tailwind CSS 사용법"
date: 2024-08-29 +0900
categories: [WEB, CSS]
tags: [web, css, tailwind]
published: true
author: jihwan
toc: true
---

## CSS 단위(rem, px)

```html
<!-- 4는 1rem이다. 대괄호를 써서 px 단위로 나타낼 수 있다. -->
<div class="w-4 w-[1rem] w-[20px]">
  Hello World
<div>
```

## 배경색, 투명도 설정(bg, opacity)
```html
<!-- 배경색 설정, 투명도 설정 -->
<div class="w-[100px] h-[100px] bg-orange-400 opacity-30">
  Hello World
<div>
```

## 테두리(border, border-color, rounded)
```html
<!-- 테두리 두께 설정, 테두리 rouned 설정 -->
<div class="w-[100px] h-[100px] border-[20px] border-red-400 rounded-[10px] rounded-full">
  Hello World
<div>
```

## 글자 크기 설정, 폰트 설정(text, font)
```html
<!-- 글자 크기 20px, 글자색, 굵게 -->
<div class="w-[100px] h-[100px] text-[20px] text-blue-400 font-bold">
  Hello World
<div>
```

## flex
```html
<!-- justify: 좌우 방향 정렬 방법, items: 상하 방향 정렬 방법 -->
<div class="w-[400px] h-[400px] flex flex-wrap justify-center items-center">
  <div class="h-[100px] w-[100px] bg-orange-400">A</div>
  <div class="h-[100px] w-[100px] bg-violet-400">B</div>
  <div class="h-[100px] w-[100px] bg-orange-400">A</div>
  <div class="h-[100px] w-[100px] bg-violet-400">B</div>
  <div class="h-[100px] w-[100px] bg-orange-400">A</div>
  <div class="h-[100px] w-[100px] bg-violet-400">B</div>
<div>
```

## hover, transition, cursor
```html
<div class="w-[400px] h-[400px] cursor-wait bg-orange-400 hover:bg-violet-400 transition duration-1000">
  Hello World
<div>
```

## relative, absolute
```html
<div class="w-[400px] h-[400px] bg-gray-400 relative">
  <div class="h-[100px] w-[100px] bg-orange-400">A</div>
  <div class="h-[100px] w-[100px] bg-violet-400 absolute top-[20px] opacity-50">B</div>
<div>
```
