---
layout: post
title: "Supabase, NextJS14 배운점(코드)"
date: 2024-09-09 +0900
categories: [WEB, nextjs]
tags: [web, supabase, nextjs, css, tailwind]
published: true
author: jihwan
toc: true
---
## 0. 배운점
[React]
input 태그에 키보드 입력시 발생하는 이벤트 타입 : (e:React.ChangeEvent<HTMLInputElement>) => {}

const useHydrate = () => {
  const [isMount, setIsMount] = useState(false);
  useEffect(()=> {
    setIsMount(true);
  }, [])
  return isMount
}
export default useHydrate
const isMount = useHydrate();if (!isMount) return null;



[NextJS14]
error.tsx, loading.tsx는 'use client'를 사용해야 한다.
env에서 앞부분에 NEXT_PUBLIC을 사용하면 클라이언트에서 읽을 수 있다. 

서버 컴포넌트에서 클라이언트 컴포넌트를 Container로서 사용한다. 
클라이언트 컴포넌트는 async 함수 컴포넌트가 될 수 없고 비동기 함수를 await로 실행시킬 수 없다. 
클라이언트 컴포넌트에서 async 함수를 사용하고 싶다면 useEffect를 사용해서 그 안에서 호출하는건 가능하다. 이 경우, await 없이 함수를 호출해야 하며 이 비동기함수를 기다려주지는 않는다. 그리고, 의존성 배열에 함수를 넣어줘야 하는데 useCallback을 사용해서 반복 랜더링을 방지하자.
클라이언트 컴포넌트에서 상태를 사용하고 싶다면 커스텀 훅을 만드는 것이 좋다. 
커스텀 훅에는 'use client'를 명시하지 않아도 된다. 당연히 client에서 실행된다. 
useState에 저장하는 데이터의 타입이 있다면 useState<type>(초기값)으로 타입을 지정해줄 수있다. 
반복되는 컴포넌트의 key 프로퍼티는 react가 관리하므로 자식 컴포넌트에서 받을 필요가 없다. 
DB 등에서 데이터를 불러올 때는 항상 try catch와 에러처리를 하자 getTodo()

// route handler, server action, server component(set 방지 필요)
import { cookies } from "next/headers";
const cookieStore = cookies();
cookieStore.get("myKey")?.value
cookieStore.set("myKey", "myValue", options)
cookieStore.set("myKey", "", options)

// middleware
const cookieStore = request.cookies;
const prev = cookieStore.get("myCookie")?.value;
const response = NextResponse.next();
response.cookies.set("myCookie", `${Number(prev ?? 0) + 1}`, {
  path: "/",
  httpOnly: true,
});

미들웨어를 만들때 함수명은 export function middleware(request: NextRequest) {} 이다.
revalidatePath("URL 경로"); 는 정적 생성 사이트에서만 사용 가능하다. 
window.location.reload(); 페이지 새로고침





[supabase]
const supabase = createBrowserClient<타입>(URL, ANON_KEY)
타입스크립트 타입 파일 생성 npx supabase gen types typescript --project-id "fbpxfuncddyagnasfftz" --schema public >types/supabase.ts
.order("id", {ascending:false})
.ilike("content", `%${term}%`)
.limit(500)
.update({content, updated_at: new Date().toISOString()})
// update 전에 select 금지
// order 다음에 is 금지, 순서가 정해져있다.
.select();
// 마지막에 select를 넣어서 update 결과물 볼 수있다. 
createBrowserClient를 서버에서 호출하면 이상한 결과가 나온다. 
Database type 형태 : type TodoDto = Database["public"]["Tables"]["todos_no_rls"]['Row']
<Auth redirectTo={process.env.NEXT_PUBLIC_OAUTH_BROWSER_REDIRECT_TO}        supabaseClient={supabase}        appearance={{          theme: ThemeSupa,        }}      />

const handleLogout = async () => {
  supabase.auth.signOut();
  // useState 변경
  getUserInfo();
};

const handleGoogleLogin = async () => {
  supabase.auth.signInWithOAuth({
    provider: "google",
    options: {
      redirectTo: process.env.NEXT_PUBLIC_OAUTH_BROWSER_REDIRECT_TO,
    },
  });
};
  





[javascript]
sleep 구현 : export const sleep = async (ms: number) =>
  new Promise((res, rej) => setTimeout(res, ms));

[typescript]
타입을 설정할 때는 type Dto 형태로 정의한다. 앞글자는 대문자이다. 
interface TodoListProps = {
  todoDataList: Database["public"]["Tables"]["todos_no_rls"]["Row"][];
};
타입인지 타입들로 구성된 리스트인지 주의하자.
널 병합 연산자 (todoDataList ?? []) 없으면 []를 반환한다.
<input value={todo?.content ?? ""} onChange={handleChange}></input>
typescript는 매개변수 이름을 지정해 값을 넣는 방식(named arguments) 지원이 안된다. 파이썬과 헷갈렸다. 객체를 사용하면 흉내낼 수 있다. 
export const createSupabaseServerClient = async ({serverComponent = false}:{serverComponent?: boolean}) =>{}
호출할 때는 createSupabaseServerClient({serverComponent: true})

[Google Login]
Google Cloud > API 및 서비스 > OAuth 동의 화면 > 사용자 유형 외부 등 설정
Google Cloud > API 및 서비스 > 사용자 인증 정보 > 웹 어플리케이션 > 승인된 자바스크립트 원본 : 홈페이지, 승인된 Redirection URI : supabase의 callback URI 추가
// 이렇게 하면 call



## 1. 환경설정

### (1) supabase 설정
> supabase DB `todo_no_rls` 생성

### (2) 개발 환경 설정
> next 14.1.4 등 라이브러리 설치
```bash
yarn add react-spinners@^0.13.8  
yarn add react-icons@^5.0.1  
yarn add @supabase/supabase-js@^2.42.0  
yarn add @supabase/ssr@^0.1.0  
yarn add @supabase/auth-ui-react@^0.4.7  
yarn add @supabase/auth-ui-shared@^0.1.8  
yarn add cookies-next@^4.1.1 
```

> supabase API KEY 확인
> .env 설정
```bash
NEXT_PUBLIC_HOME_URL=http://localhost:3000

NEXT_PUBLIC_SUPABASE_URL=https://aetvypaqciizlauonwml.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImFldHZ5cGFxY2lpemxhdW9ud21sIiwicm9sZSI6ImFub24iLCJpYXQiOjE3MjQ0MzI0MzYsImV4cCI6MjA0MDAwODQzNn0.FBhDgqgYjiNRITsL0jsiSiKEvlsAV_RTV6W0qca9zjQ

NEXT_PUBLIC_AUTH_REDIRECT_TO=http://localhost:3000/auth
NEXT_PUBLIC_AUTH_PKCE_REDIRECT_TO=http://localhost:3000/auth/callback?next=/auth

```

> Typescript Database type 파일 생성
```json
{
  "scripts": {
    "supabase:typegen": "npx supabase gen types typescript --project-id aetvypaqciizlauonwml --schema public > types/supabase.ts"
  },
}
```

## 2. (No RLS) Browser Supabase Client

### (1) supabase browser client 설정
> lib>supabase.ts
> supabase browser client 설정

```typescript
import { createBrowserClient } from "@supabase/ssr";
import { Database } from "@/types/supabase";

export const createSupabaseBrowserClient = () =>
  createBrowserClient<Database>(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
  );

```

### (2) sleep 유틸리티 함수 구현
```typescript
export const sleep = (ms: number) => new Promise((res) => setTimeout(res, ms));

```

### (3) Error 페이지, loading 페이지 구현
> Error 페이지
```typescript
"use client";
import React from "react";
import { BounceLoader } from "react-spinners";

const Error = () => {
  return (
    <div className=" flex flex-col items-center mt-12">
      <div>
        <BounceLoader />
      </div>
      <div className=" font-bold my-2">There is something wrong...</div>
    </div>
  );
};

export default Error;

```

> loading 페이지
```typescript
"use client";
import React from "react";
import { DotLoader } from "react-spinners";

const Error = () => {
  return (
    <div className=" flex flex-col items-center mt-12">
      <div>
        <DotLoader />
      </div>
      <div className=" font-bold my-2">loading...</div>
    </div>
  );
};

export default Error;


```


### (4) Client Side에서 supabase browser client를 사용한 API 생성
> getTodos(), getTodosById(id), getTodosBySearch(term), createTodos(content:string), updateTodos(id, content), deleteTodosSoft(id:number), deleteTodosHard(id)
> apis>todos-no-rls.ts
```typescript
"use client";

import { createSupabaseBrowserClient } from "@/lib/client/supabase";

// todoList 가져오기
export const getTodos = async () => {
  const supabase = createSupabaseBrowserClient();
  const result = await supabase
    .from("todos_no_rls")
    .select("*")
    .is("deleted_at", null)
    .order("id", {
      ascending: false,
    });

  return result.data;
};

// todoList 가져오기 + by Id
export const getTodosById = async (id: number) => {
  const supabase = createSupabaseBrowserClient();
  const result = await supabase
    .from("todos_no_rls")
    .select("*")
    .is("deleted_at", null)
    .eq("id", id);

  return result.data;
};

// todoList 가져오기 + search
export const getTodosBySearch = async (terms: string) => {
  const supabase = createSupabaseBrowserClient();
  const result = await supabase
    .from("todos_no_rls")
    .select("*")
    .is("deleted_at", null)
    .ilike("content", `%${terms}%`)
    .order("id", { ascending: false })
    .limit(500);

  return result.data;
};

// todoList 생성하기
export const createTodos = async (content: string) => {
  const supabase = createSupabaseBrowserClient();
  const result = await supabase
    .from("todos_no_rls")
    .insert({
      content,
    })
    .select();

  return result.data;
};

// todoList 업데이트 하기
export const updateTodos = async (id: number, content: string) => {
  const supabase = createSupabaseBrowserClient();
  const result = await supabase
    .from("todos_no_rls")
    .update({
      content,
      updated_at: new Date().toISOString(),
    })
    .eq("id", id)
    .select();

  return result.data;
};

// todoList softDelete
export const deleteTodosSoft = async (id: number) => {
  const supabase = createSupabaseBrowserClient();
  const result = await supabase
    .from("todos_no_rls")
    .update({
      deleted_at: new Date().toISOString(),
      updated_at: new Date().toISOString(),
    })
    .eq("id", id)
    .select();

  return result.data;
};

// todoList hardDelete
// export const deleteTodosHard = async (id: number) => {
//   const supabase = createSupabaseBrowserClient();
//   const result = await supabase.from("todos_no_rls").delete().eq("id", id);
//   return result.data;
// };


```
### (5) TodoContainer 구현
```typescript
"use client";
import React, { useEffect } from "react";
import useTodosController from "../hooks/useTodosController";
import TodoList from "@/components/ui/TodoList";

const TodoContainer = () => {
  const {
    loading,
    todos,
    onCreateEmptyTodos,
    onDeleteTodos,
    onSearchTodos,
    onUpdateTodos,
  } = useTodosController();

  return (
    <div>
      <TodoList
        sharedUserFullName="test user"
        owerUserId="123123"
        loading={loading}
        todoListData={todos}
        isReadOnly={false}
        onUpdate={onUpdateTodos}
        onCreate={onCreateEmptyTodos}
        onDelete={onDeleteTodos}
        onSearch={onSearchTodos}
      />
    </div>
  );
};

export default TodoContainer;

```
### (6) TodoContoroller 구현
```typescript
import {
  createTodos,
  deleteTodosSoft,
  getTodos,
  getTodosBySearch,
  updateTodos,
} from "@/apis/todos-no-rls";
import { Database } from "@/types/supabase";
import { useState, useEffect } from "react";

type TodoDto = Database["public"]["Tables"]["todos_no_rls"]["Row"];

const useTodosController = () => {
  const [loading, setLoading] = useState(true);
  const [todos, setTodos] = useState<TodoDto[]>([]);

  const onGetTodos = async () => {
    setLoading(true);
    try {
      const resultTodos = await getTodos();
      if (resultTodos) setTodos(resultTodos);
    } catch (error) {
      console.error(error);
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    onGetTodos();
  }, []);

  // 비어있는 todo 생성
  const onCreateEmptyTodos = async () => {
    await createTodos("");
    await onGetTodos();
  };
  // todo 업데이트
  const onUpdateTodos = async (id: number, content: string) => {
    await updateTodos(id, content);
    await onGetTodos();
  };
  // todo 삭제
  const onDeleteTodos = async (id: number) => {
    await deleteTodosSoft(id);
    await onGetTodos();
  };
  // todo 검색
  const onSearchTodos = async (terms: string) => {
    if (terms) {
      const todoResult = await getTodosBySearch(terms);
      if (todoResult) setTodos(todoResult);
    } else {
      await onGetTodos();
    }
  };

  return {
    loading,
    todos,
    onCreateEmptyTodos,
    onUpdateTodos,
    onDeleteTodos,
    onSearchTodos,
  };
};

export default useTodosController;

```
### (7) TodoList 구현
```typescript
```
### (8) TodoListItem 구현
```typescript
```


## 3. (No RLS) Server Supabase Client


## 4. (RLS) Server Supabase Client


