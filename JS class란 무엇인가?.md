## `class`란?

Javascript의 `class`는 객체(Object)와 관련이 있다.객체를 직접 작성하여 정의하고 생성할 수도 있지만, 클래스로 만들어주면 여러 객체를 더 쉽게 만들 수 있다.**클래스는 객체를 생성하기 위한 템플릿**이다.

`class`를 통해 원하는 구조의 객체 틀을 짜놓고, 비슷한 모양의 객체를 공장처럼 찍어낼 수 있다.

쉽게 생각해서 **클래스 = 붕어빵 기계**, 그리고 **객체 = 붕어빵** 으로 보면 된다.

---

### `class`를 사용하는 이유는?

JavaScript는 `prototype`기반의 객체지향 프로그래밍 언어이다.그렇다면 JS에 왜 `class`가 추가된 것이고 왜 사용하는 걸까?

ES6부터 추가된 `class`는 직관적으로 쉽게 코드를 읽을 수 있게 만들어 줄 뿐만 아니라, 작성하기도 쉽고 또 `class` 기반 언어에 익숙한 개발자가 더 빠르게 적응할 수 있다.

**`prototype`**

```
function Me(name) {
  this.name = name;
}

Me.prototype.wow = function () {
  console.log("WOW!");
};

let person = new Me("Jason");
person.wow(); // WOW!
```

**`class`**

```
class Me {
  constructor(name){
    this.name = name;
  }

  wow(){
    console.log("WOW!");
  }
}

let person = new Me("Jason");
person.wow() // WOW!
```

---

###  `class` 살펴보기

```
class Korean {
  constructor(name, age) {
    this.name = name;
    this.age = age;
    this.country = 'Korea';
  }

  addAge(age) {
    return this.age + age;
  }
}
```

- 클래스 내에 정의된 함수를 `method`라고 부른다.
- 클래스를 통해 생성된 객체를 인스턴스(instance)라고 부른다.
- 클래스도 함수처럼 호출하기 전까지는 코드가 실행되지 않는다. 단지 `Korean`이라는 클래스를 정의만 했을 뿐이다. `new`키워드와 소괄호`()`를 사용하여 호출할 수 있다.
- 클래스 이름은 `Korean`과 같이 항상 대문자로 시작한다.
- `constructor`는 `class`에서 필요한 기초 정보를 세팅하는 곳이다. 객체를 `new`로 생성할 때 **가장먼저 자동으로 호출된다.**
    - `constructor()` 메소드에서 `name`과 `age`, 2개의 매개변수로 `Korean` 인스턴스의 `name`, `age` 프로퍼티에 값을 할당했다.
    - `this` 는 본인 객체를 의미한다. 클래스 내에서 메소드끼리 소통하기 위해서는 `this`가 필요하다.

```
let kim = new Korean("KIMJINYOUNG",24);

{
  name: 'KIMJINYOUNG',
  age: 24,
  country: 'Korea',
  addAge: function(age){
	return this.age + age;
  }
}
```

`Korean` 클래스를 이용해 `kim` 객체를 만들면 위와 같은 instance가 생성된다.

