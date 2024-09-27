---
layout: post
title: "Supabase, NextJS14 연습문제"
date: 2024-09-09 +0900
categories: [WEB, nextjs]
tags: [web, supabase, nextjs, css, tailwind]
published: true
author: jihwan
toc: true
---

## Git repository
https://github.com/dodokyo/supa-next-todo.git

## 1. 환경설정

### (1) supabase 설정
> supabase DB `todo_no_rls` 생성

### (2) 개발 환경 설정
> next 14.1.4 등 라이브러리 설치
> supabase API KEY 확인
> .env 설정
> Typescript Database type 파일 생성

## 2. (No RLS) Browser Supabase Client

### (1) supabase browser client 설정
> lib>supabase.ts
> supabase browser client를 위한 createSupabaseBrowserClient 구현

### (2) sleep 유틸리티 함수 구현
> async 함수를 위한 sleep 함수 구현

### (3) Error 페이지, loading 페이지 구현
> Error 페이지 생성 및 react-spinner 사용
> loading 페이지 생성 및 react-spinner 사용

### (4) Client Side에서 supabase browser client를 사용한 API 생성
> apis>todos-no-rls.ts
> getTodos(), getTodosById(id), getTodosBySearch(term), createTodos(content:string), updateTodos(id, content), deleteTodosSoft(id:number), deleteTodosHard(id)

### (5) TodoContainer 구현
> TodoList에 각종 함수 넣어주기 onCreateEmptyTodos, onUpdateTodos, onDeleteTodos, onSearchTodos

### (6) TodoContoroller 구현
> loading과 todo에 useState 사용
> getTodos(), try, catch 사용
> Todo에 대한 type 적용
> export loadng, todos, onCreateEmptyTodos(), onUpdateTodos(id, content), onSearchTodos(terms), onDeleteTodos (id)

### (7) TodoList 구현
> 화면에 sharedUserFullName 표기, Things to do:, todo contents  표기
> (좌) sharedUserFullname, Things To do
> (우) Share 글자와 아이콘 사용(IoShareSocialOutline)
> usehooks 에서 useCopyToClipboard() 사용하기
> inputbox, 붙어있는 돋보기 버튼(IoSearchOutline), rounded, new Task 버튼
> todoListData가 있으면 TodoItem 으로 보여주기, map 사용, key 사용

### (8) TodoListItem 구현
> 왼쪽에 글, 오른쪽에 수정(CiEdit), 수정완성(CiCircleCheck), 삭제 버튼(AiOutlineDelete)
> 클릭하면 수정모드로 isEdit true, input 태그
> TodoItems에서 받을 함수 시그니쳐 보여주기

## 3. (No RLS) Server Supabase Client

### (1) supabase server client 만들기
> 1. routehandler, serveraction
> 2. middleware
> 3. server component 용


### (2) middleware cookie 카운터 만들기

### (3) server action ping pong 만들기

### (4) server action getTodoAction() 만들기

### (5) Google Cloud OAuth 설정
> KEY 가져오기
> supabase에도 설정하기

### (6) @supabase/auth-ui-react의 <Auth>를 이용해서 Implicit Flow 구현(code를 브라우저에서 받는다. 클라이언트 안에 access token과 refresh token이 보관되어 있다. )
> useHydrate를 이용해서 화면 깨짐 방지
> 사용자 이름 출력(useState)
> 로그아웃 구현
> 별도 버튼으로 로그인 구현

### (7) OAuth PKCE Flow 구현(code를 서버에서 받고 처리해서 redirect한다 )
> getUserInfo 만들기

### (8) Github Login 구현


## 4. (RLS) Server Supabase Client

### (1) Supabase DB todos-with-RLS 만들기

### (2) RLS 정책 구현 및 검증

### (3) AuthHeader 구현
> 로그인 되어 있는지 여부를 !!를 이용해서 한번에 확인
> 상단 바 구현 flex
> home으로 보내는 useRouter 구현
> google login 버튼 만들기
> 로그인 되어 있으면 로그아웃 버튼 표시
> 사용자 정보 가져오기, layout.tsx에서 뿌리기

### (4) Share 페이지 만들기
> 페이지 UI 만들기
> supabase profile table 만들기
> getProfileById 서버액션 만들기, 잘못된 아이디는 pemanentRidirect 하기
> Controller에서 ownerUser id 추가
 



