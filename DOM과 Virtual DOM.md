### **DOM(Document Object Model) 이란?**

- 영어 뜻풀이 그대로 하자면 문서 객체 모델을 의미한다

### **문서 객체란 ?**

- html, head, body와 같은 태그들을 javascript가 이용할 수 있는 (메모리에 보관할 수 있는) 객체를 의미한다.

### **따라서 돔이란 ?**

- 웹 페이지를 이루는 태그들을 자바스크립트가 이용할 수 있게끔 브라우저가 트리구조로 만든 객체 모델을 의미한다.

![https://k.kakaocdn.net/dn/p41Ck/btrQOnq3550/IRv7o1rcmiXHwdweXp47Zk/img.png](https://k.kakaocdn.net/dn/p41Ck/btrQOnq3550/IRv7o1rcmiXHwdweXp47Zk/img.png)

HTML의 DOM 트리

다시 말해 DOM은 HTML과 스크립팅언어(Javascript)를 서로 이어주는 역할을 하고 있다.

![https://k.kakaocdn.net/dn/qzhGF/btrQOmlpr39/CCG1F7fSlF3kQQSSSLEpIK/img.png](https://k.kakaocdn.net/dn/qzhGF/btrQOmlpr39/CCG1F7fSlF3kQQSSSLEpIK/img.png)

### 

### **자바스크립트는 어떻게 HTML 태그들을 조종할 수 있는 걸까?**

- document라는 전역 객체를 통해 접근할 수 있다.
- 또한 window라는 객체는 document객체의 상위에 위치한다.

### 

### **가상돔이 나오게 된 이유**

여기서 h1이라는 태그의 텍스트 색상을 빨간색으로 바꾸고자 한다면

우리는 document.getElementById('h1의 id')라는 DOM 접근 메서드를 이용할 것이다.

![https://k.kakaocdn.net/dn/FSEZ1/btrQPCneXpQ/Dl86oztEfC0ONcMTJBjugk/img.png](https://k.kakaocdn.net/dn/FSEZ1/btrQPCneXpQ/Dl86oztEfC0ONcMTJBjugk/img.png)

이 방식은 두 가지 측면에서 아쉬운 점이 있다.

### 

### **메모리 누수와 속도**

- 만일 개발자가 h1 태그를 찾는 코드를 변수에 저장하지 않고 매번 h1에 관련된 접근 메서드를 사용한다면 매단계마다 저 수많은 document 객체들을 전부 훑으며 찾는 현상이 발생되고 이것은 곧 메모리 누수로 이어진다.
- 또한 h1의 변화가 일어난다면 (DOM의 변화가 일어난다면) css를 다시 연산하고 레이아웃을 구성하고 웹페이지를 다시 그려주는 데에서도 시간이 든다.
- 단순히 h1만의 변화를 생각한다면 큰 문제는 없겠지만 문제는 이런 과정이 컴포넌트를 하나하나 조작할 때마다 일어난다.
- (ex. 한 화면에서 우리는 네비게이션(컴포넌트)을 열었을 때 특정 영역(컴포넌트)이 빨갛게 변하면서 위치가 변경되는 경우를 UI로 나타내야할 수도 있다. = 대략 2번 이상의 레이아웃이 일어날 것)

### **레이아웃이란?**

- 브라우저 로딩 과정 중 스타일 이후의 과정(스타일-> 레이아웃 -> 페인트 -> 합성)을 렌더링이라고 한다.
- 그리고 이 렌더링 과정은 상황에 따라 반복하여 발생할 수 있다.
- 돔이 추가되거나 삭제, 혹은 태그의 위치가 변하는 경우 렌더링이 일어난다.

### **코드량**

- 다른 하나는 객체를 찾기 위해 작성하는 코드가 번잡스러울 수 있다.
- id라는 고유성을 침해 당하지 않기 위해 해당 태그의 네이밍을 정할 때 심사숙고해야 할 것이고 해당 태그를 접근하기 위해 작성해야 하는 메서드가 그리 짧지가 않다. (document.getElementById('h1의 id'))

html 마크업을 시각적이 형태로 변환하는 시간(css가 적용되고 수정되어 반영되는 시간)이 드는 것은 어쩔 수 없지만, 최소한의 DOM 조작을 통해 작업을 처리한다면 개선하고자하여 가상돔이라는 개념을 도입한다.

# **가상 돔(Virtual DOM) 이란?**

- 실제 DOM의 가벼운 사본이다
- Virtual DOM을 사용하면 실제 DOM에 접근하여 조작하는 대신, 이를 추상화한 자바스크립트 객체를 구성하여 사용한다

### **가상 돔의 장점**

> 가상 DOM은 DOM의 상태를 메모리 위에 계속 올려두고, DOM에 변경이 있을 경우 해당 변경을 반영함DOM의 상태를 메모리에 저장하고, 변경 전과 변경 후의 상태를 비교한 뒤,
> 
> 
> **최소한의 내용만 반영 하는 기능 → 성능 향상**
> 

### **리액트가 가상돔을 반영하는 절차**

**EX) 특정 페이지에서 데이터가 변했다고 가정 했을 경우.**

### **리액트를 이용해 돔을 업데이트 시키는 절차**

**1. 데이터가 업데이트 되면, 전체 UI를 Virtual DOM에 리렌더링함**

**2. 이전 Virtual DOM에 있던 내용과 현재의 내용을 비교함 (가상 돔 끼리 비교)**

**3. 바뀐 부분만 실제 DOM에 적용이 됨**

**(컴포넌트가 업데이트 될때 , 레이아웃 계산이 한번만 이뤄짐)**

![https://k.kakaocdn.net/dn/cdtOiL/btrQOjB8dvx/kUhRU05R8ZpWHnBv26i1pK/img.png](https://k.kakaocdn.net/dn/cdtOiL/btrQOjB8dvx/kUhRU05R8ZpWHnBv26i1pK/img.png)

DOM 비교

### 

### **DOM을 건드리는 방식과 아닌 방식의 차이는 무엇인가요?**

- 직접 DOM을 건드리는 경우 DOM의 **구조를 파악**하고 있어야하며, 클래스명이다 **태그명이 바뀌는 경우** 다시 DOM 변경해야한다.
- **Angular**의 경우 view와 model을 연결시키는 바인딩작업이 있고 변화감지를 통해서 상태를 보고 있다가 업데이트되는식이다.
- **React**의 경우 가상 DOM이 있고, 가상 DOM이 실제 DOM과 비교하여 state가 변화되었는지 감지 한다.

### 

### **요약**

Virtual DOM은 실제 DOM 변화를 최소화 시켜주는 역할을 합니다.

먼저 브라우저는 HTML 파일을 스크린에 보여주기 위해 DOM 노드 트리 생성, 렌더트리 생성, 레이아웃, 페인팅 과정을 거칩니다.

DOM 노드는 HTML의 각 엘리먼트와 연관되어 있기 때문에 HTML 파일에 **20개의 변화**가 생기면 DOM 노드가 변경되고 그 이후의 과정역시 **20회 다시 이루어 집니다**.

작은 변화에도 매우 복잡한 과정들이 다시 실행되기 때문에 DOM 변화가 잦을 경우 **성능이 저하**됩니다.

이러한 단점을 보완하기 위해 나온게 **Virtual DOM**입니다.Virtual DOM은 뷰에 변화가 있다면, 그 변화가 **실제 DOM에 적용되기 전에 Virtual DOM에 적용시키고 최종 결과만 실제 DOM에 전달합니다.**

따라서 20개의 변화가 있다면 Virtual DOM은 변화된 부분만 가려내어 실제 DOM에 전달하고 실제 DOM은 그 변화를 1회로 인식하여 **단 한번의 렌더링 과정**만 거치게 됩니다.

