## ES6에서 추가된 기능
+ String Literal
+ 객체 비구조화 ( Object Destructuring )
+ 객체 리터럴 ( Object Literal )
+ for .. of 
+ Spread Operator
+ Rest Parameter
+ Arrow Function
+ Default Params
+ includes
+ Trailing Commas
+ Map & Set

## 1. String Literal

ES6의 String Literal을 활용하면 문자열을 좀 더 직관적으로 결합할 수 있습니다.

- es5

```
const val1 = 'my string';
const val2 = 'my string2';

const conVal = val1 + ', '+ val2;

console.log(conVal);
// my string, my string2
```

- es6

```jsx
const val1 = 'my string';
const val2 = 'my string2';

const litVal = `${val1}, ${val2}`
//  여기서 사용된 ` 은 Tab키 위에 있는 backtick 입니다. 작은 따옴표 아님

console.log(litVal);
// my string, my string2
```

## 2. 객체 비구조화 ( Object Destructuring )

객체의 프로퍼티 각각을 바로 꺼내 쓸 수 있습니다.

```
const address = {
    country: 'South Korea',
    city : 'Seoul',
    street: 'Gangnam',
    str_num: 141,
    postcode:'00510',
  }
```

위와 같은 객체가 있을 경우 객체의 프로퍼티 각각에 접근하고 싶으면

- es5

```
console.log(address.country);
// South Korea
console.log(address.city);
// Seoul
console.log(address.street);
// Gangnam
console.log(address.str_num);
// 141
console.log(address.postcode);
// 00510
```

- es6

```cpp
const { country, city, street, str_num, postcode } = address;

console.log(country);
// South Korea
console.log(city);
// Seoul
console.log(street);
// Gangnam
console.log(str_num);
// 141
console.log(postcode);
// 00510
```

## 3. 객체 프로퍼티 초기화 단축

ES6에선 객체 프로퍼티 이름이 로컬 변수 이름과 같으면 콜론과 값 없이 작성해도 됩니다.값을 직접 명시해주는 경우와 함께 사용할 수도 있습니다

- es5

```
function getAddress(country, city, street) {
    const myAddress  = {
      country: country,
      city: city,
      street: street,
      str_num:888,
      postcode: '9999'
    };
 }

getAddress('Korea','Seoul','Euncheon');
```

- es6

```
function getAddress(country, city, street) {
    const myAddress  = {
      country,
      city,
      street ,
      str_num:888,
      postcode: '9999'
    };
 }

getAddress('Korea','Seoul','Euncheon');
```

## 4. for .. of

기존에도 for..in 이나 forEach 처럼 반복문을 좀 더 편하게 쓰려는 시도는 있었지만 효율적이지 않았습니다( 지금은 두 방법 모두 사용을 권장하지 않습니다. )

for.. of는 이런 아쉬움을 덜어낼 수 있도록 ES6에 추가된 효율적인 반복문입니다

```jsx
let years = [2001, 2010, 2015, 2018];
```

위와 같은 배열이 있을 때

- for .. in

```
for(let year in years){
    console.log(year);
// 0, 1, 2, 3
}
```

for(변수 in 배열) 을 사용하면 키 값이 출력됩니다(사용 권장하지 않습니다)

- forEach

```coffeescript
years.forEach((year) => {
    console.log(year);
    // 2001, 2010, 2015, 2018
})
```

forEach는 배열의 내용을 출력할 수 있지만 가독성이 떨어지고 내부에서 break문 등을 사용할 수 없습니다.(사용 권장하지 않습니다)

- for .. of

```
for(let year of years){
  console.log(year);

  if(year == 2001){
   	break;
  }
// 2001
}
```

for..of의 경우 배열의 내용을 출력할 수 있고 내부에서 break문도 사용 가능합니다.

## 5. Spread Operator

...을 사용해 배열, 객체, 문자열을 다른 배열, 객체, 문자열과 결합하기가 매우 수월해졌습니다.

```jsx
let years = [2001, 2010, 2015, 2018];

let newArr = [2000, 2020];

let koreanHistory = {
    liberate : 1945,
    625: 1950
};

let worldHistory = {
    worldWar1: 1914,
    worldWar2: 1945,
};
```

이런 배열과 객체가 있을 경우 배열, 객체끼리 결합하려면

- es5

```yaml
// 배열
var concatArr = newArr.concat(years);

console.log(concatArr);
// 2000, 2020, 2001, 2010, 2015, 2018
// 정렬되어 있지 않음

// 객체
var assignObj = Object.assign(worldHistory,koreanHistory);

console.log(assignObj);
// {625: 1950, worldWar1: 1914, worldWar2: 1945, liberate: 1945}

console.log(koreanHistory);
// {625: 1950, liberate: 1945}

console.log(worldHistory);
// {625: 1950, worldWar1: 1914, worldWar2: 1945, liberate: 1945}
// worldHistory도 변경되었다

```

위와 같은 방법을 사용해야 했지만

- es6

```yaml
// 배열
let yearsCp = [2000, ...years, 2020];

console.log(yearsCp);
// [2000, 2001, 2010, 2015, 2018, 2020]
// 정렬되어 있음

const assignObj = {...worldHistory, ...koreanHistory}

console.log(assignObj);
// {625: 1950, worldWar1: 1914, worldWar2: 1945, liberate: 1945}

console.log(worldHistory);
// {worldWar1: 1914, worldWar2: 1945}

console.log(koreanHistory);
// {625: 1950, liberate: 1945}
// 기존 객체들은 그대로다

```

위와 같이 표현 가능하게 개선되었습니다.

## 6. Rest Parameter

... 을 함수의 인자에 사용해 배열을 인자로 받을 수도 있습니다

```
function printYears(years) {
    console.log(years);
}

printYears(2000, 2001, 2010, 2015, 2018);
// 2000

function printYearsWithRestParameter(...years){
    console.log(years);
}

printYearsWithRestParameter(2000, 2001, 2010, 2015, 2018);
// [ 2000, 2001, 2010, 2015, 2018 ]
```

## 7. Arrow Function

화살표 함수를 활용하면 기존의 function 보다 함수를 보다 짧고 효율적으로 표현할 수 있습니다. 예를 들어

```yaml
const years = [
    {
        year: 2000,
        data: '크리스마스',
    },
    {
        year: 2001,
        data: '로스트메모리즈',
    },
    {
        year: 2002,
        data: '월드컵',
    },
    {
        year: 2015,
        data: '리액트네이티브',
    },
    {
        year: 2019,
        data: '올해',
    },
];
```

위와 같은 배열이 있다고 할 때

- es5

```fortran
const result = years.filter(function(data){
    return data.year > 2008;
});

console.log(result);
// [ { year: 2015, data: '리액트네이티브' }, { year: 2019, data: '올해' } ]
```

- es6

```yaml
const arrowReulst = years.filter((data) => data.year > 2008);

console.log(arrowReulst);
// [ { year: 2015, data: '리액트네이티브' }, { year: 2019, data: '올해' } ]
```

## 8. Trailing Commas

es6에선 데이터가 늘어날 경우를 대비해 객체나 배열의 마지막 값 뒤에 ,을 붙여둘 수 있습니다.

```
const myObj = {
    first : 'test1',
    second: 'test2',
};

console.log(myObj);
// { first: 'test1', second: 'test2' }
```

## 9. Default Params

es6에선 함수의 기본 파라미터를 세팅해 줄 수 있습니다.

```yaml
const defaultValue = [
    {
        year: 2000,
        data: '크리스마스',
    },
    {
        year: 2001,
        data: '로스트메모리즈',
    },
    {
        year: 2002,
        data: '월드컵',
    },
    {
        year: 2015,
        data: '리액트네이티브',
    },
    {
        year: 2019,
        data: '올해',
    },
];

function printYears(years = defaultValue){
    // default Value를 default Parameter로 설정해줄 수 있다
    console.log(years)
}

console.log('인자 없이 호출')
printYears();

// 인자 없이 호출
// [ { year: 2000, data: '크리스마스' },
//   { year: 2001, data: '로스트메모리즈' },
//   { year: 2002, data: '월드컵' },
//   { year: 2015, data: '리액트네이티브' },
//   { year: 2019, data: '올해' } ]

console.log('인자 넣고 호출')
printYears({
    year:1864,
    data:'크리스마스',
});

// 인자 넣고 호출
// { year: 1864, data: '크리스마스' }
```

## 10. includes

es5에서 배열에 특정 값이 있는지 알고싶으면 indexOf를 활용해 -1 값이 있는지를 봐야 했습니다.es6에선 includes를 활용하면 배열에 특정값이 있는지를 깔끔하게 확인할 수 있습니다. 예를들어

```ebnf
let years = [2001,2010,2015, 2018];
const fruits = ['apple','banana','potato'];
```

위와 같은 배열이 있을 때

- es5

```yaml
console.log(years.indexOf(2014) !== -1);
// false
console.log(fruits.indexOf('apple') !== -1);
// true
```

- es6

```
console.log(years.includes(2014));
// false
console.log(fruits.includes('apple'));
// true
```

## 11. Map 과 Set

es6부터는 javascript에서도 Map과 Set을 지원합니다

- Map

```
let map = new Map([['id','test']]);
// map 선언 ( 앞이 key, 뒤가 value가 된다 )
map.set('testId','test');
// map에 key와 value 추가 ( 역시 앞이 key, 뒤가 value가 된다 )

console.log(map);
// Map { 'id' => 'test', 'testId' => 'test' }

console.log(map.get('testId'));
// test
// key에 해당하는 value 출력

console.log(map.size);
// 2
// map 크기 출력

console.log(map.has('testId'));
// true
// map에 특정 key가 있는지 확인

console.log(map.entries());
// [Map Iterator] { [ 'id', 'test' ], [ 'testId', 'test' ] }
// map안의 모든 요소를 key, value 형태의 array로 집어넣은 iterator 반환

console.log(map.keys());
// [Map Iterator] { 'id', 'testId' }
// map안의 모든 key를 반환

console.log(map.values());
// [Map Iterator] { 'test', 'test' }
// map안의 모든 value를 반환

console.log(map.delete('testId'));
// true
// map 안에서 특정 key에 해당하는 key-value쌍 삭제

console.log(map.size);
// 1
map.clear();
// map안의 모든 값 삭제
console.log(map.size);
// 0
```

- Set

```
const set = new Set([1,1,1,1,1,1,1,2,4,4,4,3,3,3]);
// set 선언
set.add(4);
set.add(5);
// set에 값 추가
console.log(set);
// Set { 1, 2, 4, 3, 5 }
console.log(set.size);
// 5

// Set은 중복을 허용하지 않는다

set.delete(5);
// Set에서 특정 값 삭제
console.log(set.size);
// 4
set.clear();
// Set의 모든 값 삭제
console.log(set.size);
// 0
```

### 

### 정리 ES6에서 추가된 것은 무엇인가?

```erlang
let과 const같은 변수의 선언 방식, 화살표 함수와 같은 함수의 선언 방식이 추가되었습니다.
또 class가 추가되었으며 템플릿 엔진 문자열이 추가되어 백틱을 사용할 수 있습니다.
마지막으로 구조 분해 할당이 가능해졌습니다.
```
