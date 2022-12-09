**자바스크립트의 변수 선언은 var로만 가능했으나,**

**ES6(ES2015)부터 let과 const가 추가 되었다.**

옛날의 var가 최신의 let(변수), const(상수)로 분리되었다고 생각할 수 있으나, 내부 사정은 상당히 다르다.

(참고로 여전히 var도 함께 사용이 가능하다)

### **var, let, const 차이점**

1. **중복선언 가능 여부**
2. **재할당 가능 여부**
3. **변수 스코프 유효범위**
4. **변수 호이스팅 방식**

### **1. 중복선언**

**1. var : 중복 선언이 가능하다.**

```jsx
// 첫번째 변수 선언+초기화var a = 10;
console.log(a);// 10// 두번째 변수 선언+초기화var a = 20;
console.log(a);// 20// 세번째 변수 선언(초기화X)var a;
console.log(a);// 20
```

var로 선언한 변수는 중복해서 선언(+초기화)가 가능하다.

이 경우, 마지막에 할당된 값이 변수에 저장된다.

단, 초기화 없이 선언만 한 경우엔 선언문 자체가 무시된다.(에러는 발생하지 않음)

기존에 선언해둔 변수의 존재를 까먹고, 값을 재할당하게 되는 등의 실수가 발생하기 쉽다.

**2. const, let : 중복 선언 불가능**

```jsx
// let 중복 선언let a = 10;
let a = 20;// SyntaxError: Identifier 'a' has already been declared// const 중복 선언const b = 10;
const b = 20;// SyntaxError: Identifier 'b' has already been declared
```

let, const로 선언한 변수는 중복 선언이 불가능하다.

코드에서 보는 것처럼 이미 선언한 변수를 다시 선언할 경우, 에러가 발생한다.

### **2. 재할당**

**1. var, let : 값의 재할당이 '가능'한 변수다.**

```jsx
var a = 10;
a = 20;
console.log(a);// 20let b = 111;
b = 222;
console.log(b);// 222
```

var와 let은 변수를 선언하는 키워드다.

변수 선언 및 초기화 이후에 반복해서 다른 값을 재할당 할 수 있다.

**2. const : 값의 재할당이 '불가능'한 상수다.**

```jsx
const c = 111;
c = 222;// TypeError: Assignment to constant variable.
```

const는 상수를 선언하는 키워드다.

처음에 선언 및 초기화하고 나면 다른 값을 재할당 할 수 없다.

(참고) const는 처음 선언할 때 반드시 초기화(값 할당)를 해주어야 한다.

```jsx
const a = 10;

const b;// SyntaxError: Missing initializer in const declaration
```

### **3. 스코프(Scope)**

스코프란 유효한 참조 범위를 말한다.

예를 들어, 함수 내부에서 선언된 변수는 함수 내부에서만 참조가 가능하다.

이 경우 변수의 스코프는 함수 내부로 한정 된다.

자바스크립트는 var로 선언한 변수의 스코프와 let, const로 선언한 변수의 스코프가 다르다.

**1. var : 함수 레벨 스코프(function-level scope)**

var는 함수 내부에 선언된 변수만 지역변수로 한정하며, 나머지는 모두 전역변수로 간주한다.

```jsx
function hello(){
    var a = 10;
    console.log(a);
}

hello();// 10console.log(a);//ReferenceError: a is not defined
```

hello 함수 내부에서 선언된 a변수는 함수 내부에서만 참조가 가능하며, 외부에서 참조시 에러가 발생한다.

하지만, 함수를 제외한 영역에서 var로 선언한 변수는 '전역변수'로 취급된다.

```jsx
if(true) {
    var a = 10;
    console.log(a);// 10
}

console.log(a);// 10
```

자바스크립트애서는

if문, for문, while문, try/catch 문 등의 코드 블럭{ ... } 내부에서 var로 선언된 변수를 전역 변수로 간주한다.

그래서 블럭 외부에서도 어디에서나 참조할 수 있다.

그러나, let과 const는 다르다.

**2. let, cost : 블록 레벨 스코프(block-level scope)**

let, const는 함수 내부는 물론, if문이나 for문 등의 코드 블럭{ ... } 에서 선언된 변수도 지역변수로 취급한다.

```jsx
if(true) {
    let a = 10;
    console.log(a);// 10
}

console.log(a);// ReferenceError: a is not defined
```

if문의 블럭 내부에서 let으로 선언된 변수는 외부에서 참조되지 않음을 알 수 있다.

당연히 함수 내부에서 선언된 변수도 외부에서 참조할 수 없다.

```jsx
function hello() {
    let a = 10;
    console.log(a);// 10
}

console.log(a);// ReferenceError: a is not defined
```

정리하자면,

var는 함수 내부에 선언된 변수만 지역 변수로 인정하는 함수 레벨 스코프이다.

let, const는 블록 내부에서 선언된 변수까지도 지역변수로 인정하는 블록 레벨 스코프이다.

- 참고로 블록은 if문이나 for문 등에서 중괄호{ } 로 둘러싸인 코드 영역을 말한다.

### **4. 호이스팅**

**잠깐 ! 먼저 알고 있어야 하는 지식 !**

### 변수 선언, 초기화, 할당 단계

**변수 선언**

- 변수 선언 단계에서는 값을 저장하기 위한 메모리 공간을 확보한다. 그리고 저장한 메모리를 식별하기 위한 변수 이름을 설정하는 것까지 변수 선언 단계에서 진행된다.

**변수 초기화**

- 변수 선언 단계를 거쳐 메모리 공간을 확보한 후에는 해당하는 메모리 공간에 undefined를 할당하여 초기화한다.

**변수 할당**

- 초기화 단계까지 마쳐 undefined가 할당된 변수에 원하는 값을 재할당한다.

**호이스팅이란?**

- 소스코드에서 선언된 모든 식별자(변수, 함수, 클래스)들이 유효범위 내 최상단에 마치 끌어올려진 것처럼 동작되는 자바스크립트 고유의 특징이다.

var와 let/const 는 호이스팅 과정도 다르다.

**1. var: 호이스팅이 발생한다.**

```jsx
console.log(a);// undefinedvar a = 10;

console.log(a);// 10
```

뒤에서 선언된 변수 a가 앞에서 참조되었음에도 에러를 발생시키지 않는다.

코드 실행 전에 자바스크립트 엔진이 미리 1) 변수를 선언하고,  2)undefined로 초기화해 두었기 때문이다.

이게 바로 var로 선언된 변수의 호이스팅이다.

**2. let, const: 호이스팅이 발생한다. 하지만 다른 방식으로 작동한다.**

```jsx
console.log(a);// ReferenceError: Cannot access 'a' before initializationlet a = 10;
```

뒤에서 선언된 변수를 앞에서 참조하려 하니 에러가 발생한다.

마치 호이스팅이 발생하지 않는 것처럼 보인다.

이런 현상이 발생하는 이유는 let, const의 호이스팅 과정이 var와 다르게 진행되기 때문이다.

let/const로 변수를 선언하는 경우,

코드 실행 전에는 1) 변수 선언만 해두며, 2) 초기화는 코드 실행 과정에서 변수 선언문을 만났을 때 수행한다.

그래서 호이스팅이 발생하기는 하지만, 값을 참조할 수 없어서 호이스팅이 발생하지 않는 것처럼 보이는 것이다.

변수의 선언과 초기화 사이에 일시적으로 변수 값을 참조할 수 없는 구간을 TDZ(Temporal Dead Zone)라고 한다.

그렇다면, 호이스팅이 발생하는걸 어떻게 확인할 수 있을까?

아래의 두 코드를 비교해보면 알 수 있다.

```jsx
let a = 10;// 전역변수 a선언if(true){
    console.log(a);// 10
}
```

이 코드는 전역변수로 선언된 a의 값 10을 if문 블럭에서 참조하여 출력하고 있디.

```jsx
let a = 10;// 전역변수 a선언if(true){
    console.log(a);// ReferenceError: Cannot access 'a' before initializationlet a = 20;// 지역변수 a 선언
}
```

이 코드는 if문 블럭 내부에서 지역변수 a를 다시 선언했다.

이 경우, 지역변수 a 앞에서 console.log()로 참조시 에러가 발생한다.(전역 변수 a가 있음에도!!!)

왜냐하면 지역변수 a가 호이스팅되면서 TDZ 구간이 만들어졌기 때문이다.

즉, let으로 선언된 변수도 호이스팅이 발생함을 알 수 있다.

(참고로 지역변수가 전역변수보다 우선 순위를 갖는다)

### **번외 함수 호이스팅은 어떻게 이루어 지는가** ?

우선 변수를 함수에 담는 표현식을 **함수 표현식** 이라고 한다

함수 호이스팅은 2가지 경우가 있다

1.**함수 표현식**

- 함수 표현식 이란 ?
    - 변수에 함수를 담는 표현식을 뜻한다

```jsx
 console.log(apple)// Type Errorvar apple = () => {
        console.log('hello')
    }

  console.log(apple)// Reference Error

  const apple = () => {
        console.log('hello')
    }
```

함수 표현식 같은 경우

- var 변수로 함수 표현식을 했을 경우 Type Error 가 발생한다. 그 이유는 undefined 이라는 데이터 타입은 함수와 달리 호출될수 없기 때문이다.
- let, const 같은 경우 Reference Error 가 발생하게 된다.

2. 함수 선언문

- 함수 선언문이란 ?
    - 선언과 동시에 함수가 생성되는 것을 뜻한다
    - 선언과 동시에 함수가 생성되므로 선언 전에도 함수를 사용할수 있다는 특징을 가지고 있다

```jsx
 Apple()// 111function Apple() {
    console.log('111')
}
```

하지만 선언 전에도 사용을 할 수있게 되면 디버깅 하는데 어려움을 겪을수 있어 사용을 지양하자는 목소리도 있다
