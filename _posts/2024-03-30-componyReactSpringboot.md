---
layout: single
title: "spring_react"
categories: java
tag: spring
toc: true
---

# springboot React

## React

### Router

- 로딩 분할 (코드분할)

> Suspense // 자식 요소가 로드되기 전까지 화면에 대체 UI를 보여줌

> Lazy  // 동적 import() 를 호출하는 함수를 인자로 가짐

- children 속성
  - 컴포넌트 내부에 다른 컴포넌트를 적용

> Outlet //중첨적으로 라우팅이 적용될 때 기존 컴포넌트의 구조를 유지할수 있게 함.

- 중첩라우팅
```
{
    path:"todo",
    element: <Suspense fallback={Loading}><TodoIndex/></Suspense>,
    children: [ // 중첩 라우팅
      {
        path:"list",
        element: <Suspense fallback={Loading}><TodoList/></Suspense>
      }
    ]
  }
```

> Navigate replace to="list" //리다이렉션 처리

- useParams()
  - 경로 처리할 때 쓰임
  > const {tno} = useParams();

- useSeachParams()
  - useParams()가 경로 자체의 값을 사용하는데 비해 '?' 이후에 나오는 쿼리스트링은 useSeachParams()을 사용
  - todo/list?page=3&isze=20과 유사한 형태의 경로와 쿼리스트링이 사용될때 원하는 쿼리스트링의 값을 추출

- useNavigate()
  - React-Router를 이용하면 고정된 링크로 이동할 때도 있지만, 대부분은 상황에 따라서 동적으로 데이터를 처리해서 이동하는 경우가 더 많음 이럴땐 'Link' 보단 useNavigate()를 활용

- createSearchParams()
  - React-Router의 함수를 이용해서 '/todo/modify/xx'로 이동시에 필요한 쿼리스트링을 만듬


## Springboot

