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
<div class="w-4 w-[1rem] w-[20px] min-h-[70vh]">
  Hello World
<div>
```

## div 크기 지정
```html
<!-- w-full과 max-w mx-auto를 동시에 주면 좌우 여백을 두고 가운데로 정렬된다.  -->
<div class="w-full max-w-[800px] mx-auto h-[100px] bg-[#69CFCF]">
  Hello World
<div>

<!-- w-fit 자식 요소의 크기에 맞게 변경된다.  -->
<div class="w-fit h-[100px] bg-[#69CFCF]">
  Hello World
<div>


```

## 배경색, 투명도 설정(bg, opacity)
```html
<!-- 배경색 설정, 투명도 설정 -->
<div class="w-[100px] h-[100px] bg-orange-400 opacity-30">
  Hello World
<div>
<div class="w-[100px] h-[100px] bg-[#69CFCF]">
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
<!-- justify-center justify-between -->
<!-- flex-1 부모요소의 모든 공간을 차지한다.  -->
<!-- self-end flex의 마지막 요소로 간다 -->

<div class="w-[400px] h-[400px] flex flex-wrap justify-center items-center">
  <div class="h-[100px] w-[100px] bg-orange-400 flex-1">A</div>
  <div class="h-[100px] w-[100px] bg-violet-400 flex-1">B</div>
  <div class="h-[100px] w-[100px] bg-orange-400">A</div>
  <div class="h-[100px] w-[100px] bg-violet-400 self-end">B</div>
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
## 반응형 UI
```html
<!-- sm: 640px보다 더 작을 경우 적용시킨다.  -->
<!-- 640px 초과일 경우 flex-col 적용. 640px 이하일 경우 flex-row 적용 -->
<div class="w-[400px] h-[400px] bg-orange-400 flex flex-col sm:flex-row">
  Hello World
<div>


```

## group
```html
<div class="group">
  <button class="bg-blue-500 text-white px-4 py-2">
    Hover me!
  </button>
  <p class="text-gray-500 group-hover:text-red-500">
    This text changes color when the button is hovered.
  </p>
</div>
```