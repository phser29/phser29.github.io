---
layout: single
title: "reactHock"
categories: javaScript
tag: react
toc: true
---

# react hock

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

- 