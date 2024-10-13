---
layout: single
title: "reactHock"
categories: javaScript
tag: react
toc: true
---

# useState 훅

- 컴포넌트의 상태를 간편하게 생성하고 업데이트 해주는 도구를 제공해준다.

> const [state, setState] = useState(초기값);

```
import { ChangeEvent, useState } from 'react'

function App() {
  const [msg, setMsg] = useState<string>("");

  return (
    <div>
      <input type="text" value={msg} 
      onChange={(e: ChangeEvent<HTMLInputElement>) => setMsg(e.target.value)}/>
      <br />
      <span>입력 메시지 : {msg}</span>
    </div>
  )
}

export default App
```

# useEffect 훅

> useEffect(effectCasllback[, depsList]);

- effectCasllback 함수는 useEffect 훅을 사용할 때 반드시 작성해야 하며, 컴포넌트가 마운트되거나 depsList 배열에 지정한 상태나 속성이 변경되면 호출됨.

## depsList

- 의존 객체의 배열
- 지정된 상태나 속성이 변경되면 effectCallback 함수가 호출

## 클린업 함수

> () => void

- effectCallback 함수 내부에서 클린업 함수를 리턴하도록 작성
- 컴포넌트가 언마운트될 때 실행

# useReducer 훅

- 상태와 관련된 로직을 컴포넌트 밖으로 분리시킬 수 있음

- 입력 인자가 동일하면 리턴값도 동일해야 함
- 함수에 전달되는 인자는 불변성을 가져야 함. 따라서 인자를 변경할 수 없음

## 리듀서 함수

- 순수 함수여야 하기 때문에 sate와 action을 변경해서는 안되고 반드시 새로운 상태를 만들어서 리턴

```
(state, action) => {
  return newState
}
```

- 리액트 애플리케이션에서는 상태가 바뀌면 UI도 갱신되므로 상태의 변경 추적이 디버깅 시에 필요한데, 리듀서를 사용하면 과거 시점의 상태가 그대로 유지되므로 언제든지 과거 시점의 상태가 그대로 유지되므로 언제든지 과거 시점의 상태 데이터를 확인할 수 있고 시간대별로 상태가 어떻게 변경됐는지 추적할 수 있음

### useReducer 훅 사용

> const [state, dispatch] = useReducer(reducer, initialState);

```
import React from 'react'
import {produce} from 'immer';

export interface TodoItemType {
  id: number,
  todo: string
}

// 상수로 정의
export const TODO_ACTION = {
  ADD: "addTodo" as const,
  DELETE: "deleteTodo" as const,
}

export const TodoActionCreator = {
  addTodo: (todo: string) => ({type: TODO_ACTION.ADD, payload: {todo: todo}}),
  deleteTodo: (id: number) => ({type: TODO_ACTION.DELETE, payload: {id: id}})
}

export type TodoActionType =
  | ReturnType<typeof TodoActionCreator.addTodo>
  | ReturnType<typeof TodoActionCreator.deleteTodo>;

export const TodoReducer = (state: Array<TodoItemType>, action: TodoActionType) => {
  switch (action.type) {
    case TODO_ACTION.ADD: 
      return produce(state, (draft: Array<TodoItemType>) => {
        draft.push({id: new Date().getTime(), todo: action.payload.todo});
      })
    case TODO_ACTION.DELETE:
      // eslint-disable-next-line no-case-declarations
      const index = state.findIndex((item) => item.id === action.payload.id);
      return produce(state, (draft: Array<TodoItemType>) => {
        draft.splice(index, 1);
      });
      default:
        return state;
  }
}
```

```
import React, { useReducer, useState } from 'react'
import { TodoActionCreator, TodoItemType, TodoReducer } from './TodoReducer';

const idNow = new Date().getTime();
const initialTodoList: Array<TodoItemType> = [
  {id: idNow, todo: "운동"},
  {id: idNow + 1, todo: "독서"},
  {id: idNow + 2, todo: "음악감상"},
];

const App04 = () => {
  const [todoList, dispatchTodoList] = useReducer(TodoReducer, initialTodoList);
  const [todo, setTodo] = useState("");
  const addTodo = () => {
    dispatchTodoList(TodoActionCreator.addTodo(todo));
    setTodo("");
  }

  const deleteTodo = (id: number) => {
    dispatchTodoList(TodoActionCreator.deleteTodo(id));
  }

  return (
    <div style={{padding: "20px"}}>
      <input type="text" onChange={(e) => setTodo(e.target.value)} value={todo}/>
      <button onClick={addTodo}>할인 추가</button>
      <ul>
        {todoList.map((item) => (
          <li key={item.id}>
            {item.todo} &nbsp;&nbsp;
            <button onClick={() => deleteTodo(item.id)}>삭제</button>
          </li>
        ))}
      </ul>
    </div>
  )
}

export default App04;
```
- 리듀서의 장점
  - 상태 관리 기능을 컴포넌트로부터 분리할 수 있고, 유사한 상태 관리 기능을 사용하는 여러 컴포넌트가 상태 변경과 관리 기능을 공유할 수 있음.
  - 불변성을 가지는 상태 변경을 강제하게 되므로 상태 변경을 추적하기가 용의

## useRef 훅

- 리턴값은 값에 대한 참조를 포함하는 객체 참조 데이터에 접근하려면 반드시 .current 속성을 사용해야 함.

> const refObject = useRef(initialValue);

## 메모이제이션 훅

- 기존에 연산된 결괏값을 메모리에 캐싱하고, 동일한 입력과 환경에서 재사용하는 기법
- 중복 처리를 피할 수 있어서 애플리케이션의 성능을 최적화할 때 종종 사용

- useMemo
  - useMemo는 함수가 호출되고 연산된 리턴값을 캐싱하여 재사용함. 캐싱되는 것은 함수를 호출한 후의 리턴값

> const memoizedValue = useMemo< T >(factory: () => T, depsList)

- useCallback
  - 컴포넌트 내부의 함수를 캐싱하고, 렌더링할 때마다 함수가 생성되지 않게 재사용함. 캐싱되는 것은 컴포넌트 내부의 함수

> const memoizedCallback = useCallback(callback, depsList);



# modern react Hook



