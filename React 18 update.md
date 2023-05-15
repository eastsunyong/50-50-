### React 18 버전 변경점

1️⃣  자동 배치

2️⃣  동시성 제어 기능

3️⃣  서스펜스를 지원하는 새로운 서버 사이드 렌더링 아키텍처

### 1️⃣ 자동 배치

```
리액트 배치 ?
성능 개선을 위해 여러 개의 상태 업데이트를 한 번의 리렌더링 으로 묶는 작업
리액트 배치는 이벤트 이후의 콜백에서는 작동하지 않는다.

자동 배치 ?
일반적인 이벤트 핸들러 함수 스코프에서 상태 업데이트가 발생하지 않더라도
자동으로 배치를 적용하는 것

이를 적용하기 위해,
컴포넌트 트리를 기존의 ReactDOM.render 함수 대신
새로운 ReactDOM.createRoot 함수를 사용해야한다.
```

### 2️⃣ 동시성 제어 기능

```
리액트에서 상태 업데이트는 항상 직접적인 상호 작용 반영에 반응하여 업데이트 되었다.

리액트 모든 상태 업데이트에서 제어를 하기 위해서는
setTimeout, throttle, debounce 등을 활용하는 것이 전부였다.

하지만 React 18부터는 startTransition API를 제공함으로써,
업데이트를 명시적으로 구분하여 상태 업데이트를 진행할 수 있다.
```

```
import { useTransition } from 'react';

function TransitionTest() {
    const [isPending, startTransition] = useTransition();

    function handleChange(e) {
        const val = e.target.value;

        // 바로 보여줘야 하는(업데이트) 비지니스 로직
        setDataValue(val);

        // 다른 업데이트에 영향을 줄 수 있는 비지니스 로직을 감싼다.
        startTransition(() => {
            // 느린 렌더링 또는 네트워크 로직이 들어 갈 수 있다.
            setDataQuery(val);
        });
    }

}
```

### 3️⃣ 새로운 서버 사이드 렌더링

```
React 17에서 전체 컴포넌트 트리 중 일부가 나머지 부분보다 느리다면,
SSR의 전체 성능은 급격하게 낮아지게 된다.
* 각 단계마다 그 느린 부분에서 병목 현상이 발생하기 때문

React 18에서는 Suspense를 사용하여 앱을 더 작은 독립적인 유닛으로 만들 수 있다.
이를 통해 앱의 나머지 부분의 렌더링을 방해하지 않게 할 수 있다.

Suspense ?
코드를 불러오는 동안 “기다릴 수 있고”,
기다리는 동안 로딩 상태(스피너와 같은 것)를 선언적으로 지정할 수 있도록 하는것
- https://ko.reactjs.org/docs/concurrent-mode-suspense.html
```

- **HTML 스트리밍** : 서버 단에서, renderToString 대신 새로운 pipeToNodeWritable API를 사용하여 HTML을 스트리밍할 수 있다.
- **선택적 Hydaration** : 앱에서 렌더링 비용이 많이 드는 서브 컴포넌트 트리를 Suspense로 감싸서, 전체 앱의 Hydration을 방해하지 않고 별도의 Hydration을 진행할 수 있다.

```
lazy 컴포넌트와 Suspense를 서버 사이드 렌더링에서 사용할 수 없었다는 것이 문제점

하지만 React 18부터는 새로운 렌더링 API인 pipeToNodeWritable 덕분에,
Suspense와 함께 lazy 컴포넌트를 사용할 수 있게 되었다.
```
