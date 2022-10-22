# 구조분해 (Destructuring assignment)

## 1. 문법

구조분해의 기본 문법은 아래와 같습니다.

```
const [a, b] = [1, 2];
console.log(a);// 1
console.log(b);// 2const [c, d, ...rest] = [1, 2, 3, 4, 5, 6, 7];
console.log(c);// 1
console.log(d);// 2
console.log(rest);// [3, 4, 5, 6, 7]const { e, f } = { e: 1, f: 2 };
console.log(e);// 1
console.log(f);// 2const x = [1, 2, 3, 4, 5];
const [y, z] = x;
console.log(y);// 1
console.log(z);// 2
```

구조분해 할당의 좌변 은 값을 담을 변수, 우변 에는 값을 널을 변수가 됩니다.

## 2. 배열 구조분해

### 기본 변수 할당

배열 구조분해 변수에 값을 할당하는 기본 방법은 아래와 같습니다.

```
var foo = ['one', 'two', 'three'];
var [one, two, three] = foo;

console.log(one); // "one"
console.log(two); // "two"
console.log(three); // "three"
```

foo에 one, two, three를 각각 저장한 후, 변수 one two three에 구조분해로 할당되어 출력되는 것을 확인 할 수 있습니다.

### 선언에서 분리한 할당

변수 선언과 할당을 분리하여 배열 구조분해 할당을 할 수 있습니다.

```jsx
var a, b;

[a, b] = [1, 2]
console.log(a);// 1console.log(b);// 2
```

### 기본값 설정

배열 구조분해는 기본값 설정이 가능합니다.

```
var a, b;

[a=5, b=7] = [1];
console.log(a);// 1console.log(b);// 7
```

a=5, a=7로 기본값을 할당하였습니다. a에는 1이 할당되었고, b에는 값이 할당되지 않았기 때문에 기본값인 7이 할당된 것을 확인 할 수 있습니다.

### 값 교환

스와핑, 두개의 값 교환을 배열 구조분해를 사용하면 한줄로 표현이 가능합니다.

```jsx
var [a, b] = [1, 3];

[a, b] = [b, a];
console.log(a);// 3console.log(b);// 1
```

### 함수의 반환된 배열

함수에서 반횐된 배열로도 구조분해 할당이 가능합니다. => 자바스크립트의 함수는 1급함수 이기 때문입니다.

```jsx
function foo() {
  return [1, 2];
}

var [a, b] = foo();
console.log(a);// 1console.log(b);// 2
```

foo() 에서 배열 [1,2]를 리턴합니다. 이 리턴 값으로 구조분해 할당하여 변수 a와 b에 값이 출력되는 것을 확인 할 수 있습니다.

### 값 무시하기

```jsx
function foo() {
  return [1, 2, 3];
}
var [a, , b] = foo();
console.log(a);// 1console.log(b);// 3

[a, , b] = [4, 5, 6];
console.log(a);// 4console.log(b);// 6
```

리턴된 값 2와 할당된 값 5를 무시한 상태로 할당되는 것을 확인할 수 있습니다.모든 값을 무시하는 것도 가능합니다.

```
[,,] = [1, 2, 3, 4, 5];
```

### 전개 연산자를 이용한 저장

...(전개연산자)를 이용해 나머지 배열을 변수에 할당이 가능합니다.

```
var [a, ...b] = [1, 2, 3];

console.log(a);// 1console.log(b);// [2, 3]
```

## 3. 객체 구조분해

### 기본 변수 할당

```yaml
var a = { p: 42, q: true };
var { p, q } = a;

console.log(p); // 42
console.log(q); // true
```

### 선언에서 분리한 할당

```
var{ a, b } ={ a:1, b:2 };

console.log(a);// 1
console.log(b);// 2
```

### 새로운 변수 이름에 할당

```yaml
var a = { p: 42, q: true };
var { p: foo, q: bar };

console.log(foo); // 42
console.log(bar); // true
```

### 중첨된 객체와 배열 구조분해

```
var metadata = {
  title: 'Scratchpad',
  translations: [
    {
      locale: 'de',
      localization_tags: [],
      last_edit: '2014-04-14T08:43:37',
      url: '/de/docs/Tools/Scratchpad',
      title: 'JavaScript-Umgebung',
    },
  ],
  url: '/en-US/docs/Tools/Scratchpad',
};

var {
  title: englishTitle,
  translations: [{ title: localeTitle }],
} = metadata;
console.log(englishTitle);// "Scratchpad"console.log(localeTitle);// "JavaScript-Umgebung"
```

### for...of 문에서 구조분해

```
var people = [
  {
    name: 'Mike Smith',
    family: {
      mother: 'Jane Smith',
      father: 'Harry Smith',
      sister: 'Samantha Smith',
    },
    age: 35,
  },
  {
    name: 'Tom Jones',
    family: {
      mother: 'Norah Jones',
      father: 'Richard Jones',
      brother: 'Howard Jones',
    },
    age: 25,
  },
];
for (var {
  name: n,
  family: { father: f },
} of people) {
  console.log('Name: ' + n + ', Father: ' + f);
}
// "Name: Mike Smith, Father: Harry Smith"
// "Name: Tom Jones, Father: Richard Jones"
```

### 매개변수에서 구조분해

개인적으로 이 구조분해는 많이 쓰이는 것 같습니다.

```
var user = {
  id: 42,
  displayName: 'jdoe',
  fullName: { firstName: 'John', lastName: 'Doe' },
};

function userId({ id }) {
  return id;
}

console.log(userId(user));// 42
```

### 동적 변수 이름 사용

```jsx
let target = "z";
let { [target]: foo } = { z: "bar" };

console.log(foo);// "bar"
```
