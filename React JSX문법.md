### **JSX란 무엇인가?**

JSX를 리액트에서 무조건 사용해야하는것은 아니지만, JSX를 통해 얻는 이점이 많아 대부분의 개발자가 사용한다.

그렇다면 JSX란 무엇일까?

JSX는 **J**ava**S**cript **X**ML의 줄임말로 XML 형태로 작성되며, 아래 문법은 JavaScript에 XML을 확장한 JSX의 문법이다.

`const element = <h1>Hello, World!</h1>;`

그밖에 JSX의 특징은 아래와 같다.

▪ JSX(JavaScript XML)는 Javascript에 XML을 추가한 확장한 문법이다.

▪ 브라우저에서 실행되기 전에 바벨을 통해 일반적인 자바스크립트 코드로 변환된다.

▪ 공식적인 자바스크립트 문법은 아니다.

▪ JSX 하나의 파일에 자바스크립트와 HTML을 동시에 작성할 수 있다.

### **JSX 변환 예제**

![https://k.kakaocdn.net/dn/btdzfd/btrPQIb9YNZ/3ykNTyNZ7FjCxKDeN6ueg0/img.png](https://k.kakaocdn.net/dn/btdzfd/btrPQIb9YNZ/3ykNTyNZ7FjCxKDeN6ueg0/img.png)

JSX 변환 예제

위와같은 코드를 입력하면,  아래와 같은 자바스크립트 코드로 변환되어 렌더링된다.

```
function App() {
	return React.createElement("div", null, "Hello ", React.createElement("strong", null, "World"))
}
```

### **JSX 문법**

**1. 반드시 부모 요소는 한개의 태그로 감싸져 있어야 한다.**

virtual DOM에서 컴포넌트 변화를 효율적으로 감지하여 비교할수 있도록컴포넌트 내부는 하나의DOM트리로 구성되어 있어야 한다고 함

```jsx
import React from 'react';

function App() {
	return (
    	<div>
      		<div> 최상위의 부모 요소는 한개의 태그로 감싸져야 한다. </div>
      	</div>
    )
}

export default App;

// 아래처럼 쓰면 안됨!!!function App() {
	return (
    	<div> 첫번째요소 </div><div> 두번째요소 </div><div> 부모요소가 한개로 감싸져있지않음 </div>
    )
}
```

**2. 자바스크립트 표현**

react 내에서 자바스크립트 표현식 작성을 위해서 { } 로 감싸면 된다.

```jsx
import React from 'react'

function App(){
    const year = new Date().getFullYear()
    return(
        <div>
            <h1> Happy New Year,{year}</h1>
        </div>
    )
}

export default App;
```

위의 컴포넌트를 렌더링 하면 아래와같이 year 변수가 나온는것을 볼수있다.

![https://k.kakaocdn.net/dn/BHcJT/btrPXucm6fH/iZy0kHUTbngZ23iiozn9o1/img.png](https://k.kakaocdn.net/dn/BHcJT/btrPXucm6fH/iZy0kHUTbngZ23iiozn9o1/img.png)

참고로 Element도 변수에 넣어서 사용할 수 있다.

```jsx
import React from 'react'

function App(){
    const thumbnailImg = 'https://i1.daumcdn.net/thumb/R600x0/?fname=https://blog.kakaocdn.net/dn/sh7sG/btrpoV7Nxky/QsZZ2HBGlrKRuGqK5ZgRa0/img.png';
    const textElement = <span> 변수에 넣은 textElement <br/></span>;
    const imageElemet = <img style={{ width:'200px' }} src={ thumbnailImg } alt="dd"/>;
// style을 JSX내부에 넣어주려면 object로 넣어주어야 한다return(
        <div>
            { textElement }
            { imageElemet }
        </div>
    )
}

export default App;
```

결과

![https://k.kakaocdn.net/dn/6Mju5/btrPQ4eZqgi/Xkva66edQyowefLcUl0Fxk/img.png](https://k.kakaocdn.net/dn/6Mju5/btrPQ4eZqgi/Xkva66edQyowefLcUl0Fxk/img.png)

**3. 삼항연산자를 이용한 조건부 렌더링**

JSX내부의 자바스크립트 표현식에서 if문을 사용할 수 없어서**{ } 안에 삼항연산자를 사용하면 조건에 따라 렌더링을 다르게 할 수 있다.**

```jsx
import React from 'react'

function App(){
    const boolean = true
    return(
        <div>
            { boolean ? ( <h1> true </h1> ) : ( <h1> flase </h1> ) }
        </div>
    )
}

export default App;
```

결과

![https://k.kakaocdn.net/dn/ugNtV/btrPQ5rtH9i/KAPUknIKpDUMukuZC3nSs1/img.png](https://k.kakaocdn.net/dn/ugNtV/btrPQ5rtH9i/KAPUknIKpDUMukuZC3nSs1/img.png)

**4. &&(AND)연산자를 이용한 조건부 렌더링**

**특정조건을 만족할때만 내용을 보여주고, 만족하지 않을때는 렌더링 하지 않는 경우**에 사용한다.

```jsx
import React from 'react'

function App(){
    const boolean = true
    return(
        <div>
            { boolean && <h1>보여준다</h1> }
        </div>
    )
}

export default App;
```

위코드의 결과는 아래와같다.

![https://k.kakaocdn.net/dn/bAHUrd/btrPXucm6fc/ZagWzWxP1VReg2RfRxgKFK/img.png](https://k.kakaocdn.net/dn/bAHUrd/btrPXucm6fc/ZagWzWxP1VReg2RfRxgKFK/img.png)

근데 저기서 boolean값을 false로 바꿔주게되면 아래와같이 아무것도 렌더링되지않게된다.

![https://k.kakaocdn.net/dn/bfaMhv/btrPQHK3c5k/JYv9HCZzsxN0I4tDJhgQF0/img.png](https://k.kakaocdn.net/dn/bfaMhv/btrPQHK3c5k/JYv9HCZzsxN0I4tDJhgQF0/img.png)

**5. ||(OR)연산자를 이용한 조건부 렌더링**

어떤값이 undefined일 수가 있다면,**OR연산자를 사용하여 해당값이 undefind인 경우일때 사용할 값을 지정하여** 오류를 방지한다.

컴포넌트내부에서 undefined만 반환하면 오류가 난다.

```tsx
import React from 'react'

function App(){
// 오류가 발생하는 코드const boolean = undefined;
    return boolean
}

export default App;
```

위와같은 경우가 생길 수 있다면, OR 연산자를 사용하여 아래같이 오류를 방지한다.

```
import React from 'react'

function App(){
    const boolean = undefined;
    return boolean || 'undefined 입니다'
}

export default App;
```

결과

![https://k.kakaocdn.net/dn/O0qwO/btrPTk9pB3w/wTm9HUIuKw6ipylNRsi1Sk/img.png](https://k.kakaocdn.net/dn/O0qwO/btrPTk9pB3w/wTm9HUIuKw6ipylNRsi1Sk/img.png)

근데 참로고 아래처럼 JSX내부에서 undefined를 렌더링 하는것은 오류나지 않는다.

```jsx
import React from 'react'

function App(){
    const boolean = undefined;
    return(
        <div>
            { boolean }
        </div>
    )
}

export default App;
```

**6. 클로징태그와 셀프 클로징태그**

HTML에서 input이나 br을 사용할 때 태그를 닫지 않는 경우가 있다.

하지만 리액트에서는 반드시 **클로징 태그를 써줘야** 한다.

![https://k.kakaocdn.net/dn/cVVh4A/btrPQIJ12JS/FOMTqOlBhEujgakldMKTDk/img.png](https://k.kakaocdn.net/dn/cVVh4A/btrPQIJ12JS/FOMTqOlBhEujgakldMKTDk/img.png)

모든 태그에 셀프 클로징태그  **/  를 이용하거나 태그를 닫아주어야한다.**

![https://k.kakaocdn.net/dn/kLKF7/btrPS0XsXZF/oQDejzlwUJLNdKUpvexyd0/img.png](https://k.kakaocdn.net/dn/kLKF7/btrPS0XsXZF/oQDejzlwUJLNdKUpvexyd0/img.png)

**7. class정의시 class가 아닌 className을 사용한다.**

class가 es6의 클래스와 겹치는 예약어라서 className을 사용한다고 한다!

```jsx
import React from 'react'

function App(){
    const boolean = true
    return(
        <div>
            <input className="input-text" type="text"/>
        </div>
    )
}

export default App;
```
