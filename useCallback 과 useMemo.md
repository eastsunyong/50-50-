### **메모이제이션 (memoization)** 이란 ?

**memoization**이란 기존에 수행한 연산의 결과값을 어딘가에 저장해두고 동일한 입력이 들어오면 재활용하는 프로그래밍 기법을 말한다.

**memoization**을 절적히 적용하면 **중복 연산**을 피할 수 있기 때문에 메모리를 조금 더 쓰더라도 애플리케이션의 성능을 **최적화**할 수 있다.

### **useMemo**

- **사용법**

```coffeescript
useMemo(() => fn, deps)
```

useMemo 는 **deps** 가 변한다면, **() => fn 이라는 함수를 실행**하고, 그 함수의 반환 값을 반환한다.

- **예시**

```jsx
import React, { useState, useCallback, useMemo } from "react";

export default function App() {
  const [ex, setEx] = useState(0);
  const [why, setWhy] = useState(0);

// useMemo 사용하기
  useMemo(() => {console.log(ex)}, [ex]);

// 두 개의 버튼을 설정했다. X버튼만이 ex를 변화시킨다.return (
    <>
      <button onClick={() => setEx((curr) => (curr + 1))}>X</button>
      <button onClick={() => setWhy((curr2) => (curr2 + 1))}>Y</button>
    </>
  );
}
```

![https://blog.kakaocdn.net/dn/cssgzW/btrRMUOkJLG/daxLgLw0KaLOyglF5pnJhK/img.png](https://blog.kakaocdn.net/dn/cssgzW/btrRMUOkJLG/daxLgLw0KaLOyglF5pnJhK/img.png)

이런 작고 소중한 버튼이 있다.

먼저 위 코드는 X라는 버튼을 누를 때에 '**ex**' 라는 상태값이 변화하는 코드이다.

> useMemo(() => {console.log(ex)}, [ex])
> 

에서 **deps** 는 [**ex**] 이다.

**ex 가 변할 때에만 () => {console.log(ex)} 이 실행된다.**

따라서 **X 버튼을 누를 때에만 콘솔창에 ex 값이 출력된다.**

Y 버튼을 누르더라도 APP 이라는 함수 컴포넌트가 전부 재실행(리렌더링) 되지만,

ex 라는 값은 변하지 않았기 때문에 useMemo는 에는 아무런 변화가 없다.

### **useCallback**

useMemo 는 그냥 함수를 **실행**해버리는데, 얘는 함수를 **반환**한다.

> useCallback(fn, deps)
> 

useCallback 는 **deps** 가 변한다면, **fn** 이라는 **새로운!**함수를 반환한다.

```jsx
import React, { useState, useCallback, useMemo } from "react";

export default function App() {
  const [ex, setEx] = useState(0);
  const [why, setWhy] = useState(0);

// useCallback 이 () => {console.log(why)} 라는 함수를 반환한다.const useCallbackReturn = useCallback(() => {console.log(why)}, [ex]);

// useCallback 이 담겨있는 함수를 실행
  useCallbackReturn()

  return (
    <>
      <button onClick={() => setEx((curr) => (curr + 1))}>X</button>
      <button onClick={() => setWhy((curr2) => (curr2 + 1))}>Y</button>
    </>
  );
}
```

아까 그 코드와 같은 버튼을 보여주는 코드이다.

위의 **useCallback** 은 **() => {console.log(why)}** 라는 함수를 **반환**해주고 있다.

위의 useCallback 은 다음의 순서로 진행될 것이다.

1. 처음 컴포넌트가 시작될 때 실행 **() => {console.log(0)}**
2. ex 가 변할 때까지 함수는 **() => {console.log(0)}**
3. **ex 가 변한다면** 그제서야 why 의 값을 가져와서 **() => {console.log(새로운 값)}**

예를 들어서 **Y 버튼을 다섯번** 누른다고 해보자.

Y 버튼이 눌리면 'why'라는 상태의 값이 1씩 증가할 것이다.

![https://blog.kakaocdn.net/dn/efbrTh/btrRPCso9WT/lWzxRRKBhDs9KqKixJRW6k/img.gif](https://blog.kakaocdn.net/dn/efbrTh/btrRPCso9WT/lWzxRRKBhDs9KqKixJRW6k/img.gif)

위의 움짤에서 보듯이, Y를 다섯번 누를 때 동안에는 계속 함수가 **() => {console.log(0)}** 이다.

(물론 이 때 why라는 상태값은 계속 값이 증가한다.)

그러다가 **X 버튼**을 누르면서 ex 라는 변수(deps) 가 변하자 마자, **() => {console.log(5)}** 를 반환한다.

**deps가 변해야 함수 컴포넌트와 상태값(why) 를 공유하는 것이다!!**

따라서 useCallback 은 함수와는 상관 없는 상태값이 변할 때,

**함수 컴포넌트에서 불필요하게 함수를 업데이트 하는 것을 방지**해준다.

다만, deps 를 잘못 설정하면 아무리 함수 컴포넌트를 재실행해도 함수가 변하지 않으면서

내가 원치 않는 상황이 올 수도 있으므로 **섬세한 컨트롤**이 필요하다..

이런 상황은 **useMemo**도 똑같다. useMemo 역시 Y 버튼을 5번 눌러도, X버튼을 안 누르면 실행이 되지 않는다.

추가로, react 공식 문서에서도 인정하듯이, 아래의 두 식은 같다.

> useMemo((...)=>fn, deps) === useCallback(fn, deps)
>
