1 느슨한 타입의 동적언어
JavaScript는 느슨한 타입의 동적 언어이다. JS의 변수는 어떤 특정한 타입과 연결되지 않으며, 모든 타입으로 할당 및 재할당이 가능하다.변수의 타입을 미리 선언할 필요가 없다. 프로그램이 처리되는 과정에서 자동으로 파악되고, 이 말은 결국 같은 변수에도 불구하고 상황에 따라 값의 타입이 바뀔 수 있다는 뜻이기도 하다.

문제점 
모든 타입으로 할당 및 재할당을 하니 혼자 프로그램을 짤 때는 문제가 없지만 대형프로젝트나 협업 프로젝트시 타입이 올바른지 체크하는 것이 까다롭기 때문에 배포시 예상치 못한 문제와 직면 할 수 있다.

보완점
JS 느슨한 타입의 보완 방법은 강력한 문법을 추가한 TypeScript 를 사용하여 보완 할 수 있다. (TypeScript 란? MS에서 개발한 오픈소스, 프로그래밍 언어이며, JS의 단점을 보완하기 위해 만들어졌다. Js는 동적타입 언어이기 때문에 런타임 속도는 빠르지만 안전성이 보장되지 않는다. 타입스크랩트는 정적 타입 언어이기 때문에 컴파일시 시간이 조금 걸리더라도 안정성을 보장한다는 것이 장점이다.)

형변환 2종류 
형변환 이란 명시적일 수도 있고, 암시적일 수도 있다. 명시적 형변환(explicit coercion)은 Number("123") 처럼 프로그래머의 코드에서 암시적으로 자료형을 정해서 변환하는 과정이다. 암시적 형변환(implicit coercion)은 연산자 사용으로 인해 자연적으로 일어나는 형변환이다. 대표적인 예시로 ==, +, > 등 연산자의 사용이 있다. 예외적으로 ===는 형변환을 얘기하지 않는다.

명시적 형변환 
Js에서의 명시적 형변환은 주로 세 가지가 있다. String() 은 문자형으로 변환, Number() 숫자형으로 변환, 마지막으로 Boolean() 이 값이 True 인지 False 변환 해준다. 

 1.  String ()

문자열이 아닌 값을 문자열로 바꾸려면 이렇게 String 함수를 활용하면 되는데, 소괄호 안에 값을 넣어주면 그 값이 문자열로 변한다.

 2. Number()

console.log(Number('')); // 0
console.log(Number('abc')); // NaN
console.log(Number('123')); // 123
console.log(Number('123a')); // NaN
console.log(Number(true)); // 1
console.log(Number(false)); // 0
console.log(Number(null)); // 0
console.log(Number(undefined)); // NaN
console.log(Number({name: 'bigtop'})); // NaN
console.log(Number({})); // NaN
가장 먼저 볼 수 있는 빈 문자열은 0으로 변환된다.

그리고 '123'과 같이 따옴표를 벗겨냈을 때 온전히 숫자로 사용이 가능한 문자열은 숫자 123으로 변환된다.

그러나 '123a'와 같이 숫자와 문자가 혼합된 문자열은 NaN값으로 변환된다.

또 한 가지, boolean형태의 값은 true는 1, false는 0으로 변환된다.

비슷한 의미의 null과 undefined는 여기서 차이를 보이는데, null은 0으로 변환되지만, undefined는 NaN값으로 변환된다.

마지막으로 빈 문자열이 0으로 변환되기 때문에 빈 객체 값도 0일까 싶지만 빈 객체는 그대로 NaN값으로 변환된다.

참고로 '123a'와 같은 숫자와 문자가 혼합된 경우에도 숫자로 시작하는 문자열인 경우 parseInt 혹은 parseFloat 함수를 사용하면 숫자 형태로 변환이 가능하다.

 

  3. Bloolean

Boolean 형태는 당연히 true 혹은 false 두 가지 값으로 변형되는데, 단순하게 생각해서 뭔가 어떤 값이 있는 것 같은 가진 값들은 true, 그 반대는 false로 변환된다.

 

암시적 형변환
  1. 덧셈 연산자  ( + )

// string
console.log('문자' + 1234); // 문자1234
console.log('문자' + true); // 문자true

// number
console.log(1234 + '1234'); //12341234
console.log(1234 + true); // 1235

// boolean
console.log(true + 123); // 124
console.log(false + 123); // 123
연산을 할 때는 피연산자가 한쪽이라도 '문자열'이면 문자열 연산이 된다.

그런 원리로 string 구간을 보면, 한쪽만 문자열인 경우 반대편도 문자열 형태로 형변환을 일으킨 뒤 연산을 수행한다.

그리고 나머지 경우는 산술덧셈 연산을 수행하는데, string을 제외한 구간을 살펴보면 덧셈 연산을 할 때 양쪽 피연산자를 모두 숫자형으로 형 변환을 일으킨 뒤 연산을 수행한다.

 

  2. 관계 연산자  ( <, <=, >, >= )

// string
console.log('a' <= 'b'); // true
console.log('a' <= 1234); // false

// number
console.log(1234 <= 1234); // true
console.log(1234 <= true); // false

// boolean
console.log(false <= true); // true
console.log(false <= false); // true
관계 연산자도 산술연산과 동일하다. 양쪽 모두 문자열인 경우를 제외하면 양쪽 모두 숫자형으로 형 변환을 일으킨 후 연산한다. 관계 연산자도 산술연산과 동일하다. 양쪽 모두 문자열인 경우를 제외하면 양쪽 모두 숫자형으로 형 변환을 일으킨 후 연산한다.

 

    3.  논리 연산자(&&, ||, !)

// string
console.log('문자' && 1234); // 1234
console.log('문자' && true); // true
console.log('문자' || 1234); // 문자
console.log('문자' || true); // 문자

// number
console.log(1234 && 1234); // 1234
console.log(1234 && true); // true
console.log(1234 || 1234); // 1234
console.log(1234 || true); // 1234

// boolean
console.log(true && true); // true
console.log(true && false); // false
console.log(true && null); // null
console.log(true && undefined); // undefined
 

undefined와 null의 미세한 차이들을 비교해보세요.
undefined 와 Null 의 차이점은 우선 undefined 은 원시값으로 선언한 후에 값을 할당하지 않은 변수나 값을 주어지지 않은 인수에 자동으로 할당된다 Null 은 원시값 중 하나로 어떤 값이 의도적으로 비어있음을 표현한다 여기서 차이가 나타난다 undefined 는 값이 지정되지 않은 경우를 의미하지만 Null 의 경우에는 해당 변수가 어떤 객체더 가리키지 않다는 것을 의미한다

==, === 차이점  
==, === 차이점은 ==는 a == b 라고 할때, a와 b의 값이 같은지를 비교해서, 같으면 true, 다르면 false라고 한다. ===는 Strict, 즉 엄격한 Equal Operator로써, "엄격하게" 같음을 비교할 때 사용하는 연산자이다. ===는 a === b 라고 할때, 값과 값의 종류(Data Type)가 모두 같은지를 비교해서, 같으면 true, 다르면 false라고 한다. 
