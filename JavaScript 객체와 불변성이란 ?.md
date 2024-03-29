- 자바스크립트에서는 불변성을 유지하는 값들과 그렇지 않은 값들이 나누어져 있다. 불변성을 유지하는 값들을 기본형 타입이라고 부르며 메모리 내에 고정된 크기로 저장되면서, 원시 데이터 값 자체를 보관한다. 종류 Boolean, Number, String, null, undefined 가 있다 . 참조형 Object 타입들은 변경가능한 값들이다. 참조형 종류에는 Array(배열), function(함수) 가 있다

원시타입

원시 타입이란 있는 그대로 저장되는 데이터를 표현한다. 그리고 원시값을 변수에 할당하면 값이 복사되어 들어간다. 즉, 원시값이 할당된 변수들은 모두 자기 자신만의 고유한 값을 가지게 된다.

원시 타입 종류 :

- boolean : true, false
- 숫자 : 1, 2, 3...
- 문자열 : "Hello World"
- null
- undefined

참조타임

참조 타입이란 자바스크립트 객체를 나타낸다. 참조 타입은 변수에 값을 직접 저장하지 않는다. 변수에 저장되는 것은 메모리 안에서 객체의 위치를 가리키는 **포인터**이다. **무엇이 저장되느냐**, 이것이 원시 타입과 참조 타입의 가장 큰 차이점이다.

참조 타입의 종류

원시 타입을 제외하고 전부 참조 타입으로 봐도 좋다.

- 객체 : {}
- 배열 : []
- 함수 : function
- Date

불변 객체를 만드는 방법

- 불변 객체란 '변하지 않는 객체' 즉 이미 할당한 객체가 변하지 않는다는 뜻을 가지고 있다 JS에서 불변 객체를 만들 수 있는 방법은 기본적으로 2가지 인데 const와 Object.freeze() 를 사용하는 것이다. const 키워드는 변수를 상수로 선언할 수 있다.Object.freeze() 자바스크립트에서 기본적으로 제공하는 메소드인 Object.freeze() 메소드이다. 공식 문서에서는 "객체를 동결하기 위한 메소드" 라고 적혀있다.

얕은 복사(Shallow Copy)와 깊은 복사(Deep Copy)얕은 복사는 객체의 참조값(주소 값)을 복사하고, 깊은 복사는 객체의 실제 값을 복사한다.자바스크립트에서 값은 원시값과 참조값 두 가지 데이터 타입의 값이 존재한다.자바스크립트에서 원시 타입(primitive type)의 값은 새로운 메모리 공간에 독립적인 값을 저장하기 때문에 깊은 복사가 되고 참조 타입(reference type)값은 얕은 복사가 된다. 원시 타입과 참조 타입의 가장 큰 차이점은 원본이 바뀌면 참조 타입은 복사본도 같이 변경되지만, 원시 타입은 변경되지 않는다는 점이 큰 차이점이다.

```jsx
// 원시 타입의 깊은 복사let a = '원본 데이터';
let b = a;

a = '수정 데이터';

console.log(a);// '수정 데이터'console.log(b);// '원본 데이터'
```

원시 타입은 복사 시 값 자체를 담은 독립적인 메모리를 생성하기 때문에 a가 재할당 되더라도 b에는 아무런 영향을 미치지 않는다.

```jsx
// 참조 타입의 얕은 복사let a = {name:'원본 데이터'};
let b = a;

a.name = '수정 데이터';

console.log(a);// '수정 데이터'console.log(b);// '수정 데이터'
```

원시 타입과 달리 참조 타입인 오브젝트는 새로운 값으로 변수 값을 재할당 하자 복사된 변숫값도 같이 변경되는 것을 확인할 수 있다. 즉, 데이터가 그대로 하나 더 생성된 것이 아닌 해당 데이터의 메모리 주소를 전달하게 돼서, 결국 한 데이터를 공유하게 되는 걸 알 수 있다

