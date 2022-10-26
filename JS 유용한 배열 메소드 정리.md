## JavaScript의 유용한 배열 메소드 정리

---

### 📌 1. push & unshift

```jsx
let arr = [1, 2, 3];

console.log(arr.push('push!'));// [1, 2, 3, 'push!']console.log(arr);//console.log(arr.unshift('unshift!'));// 5console.log(arr);// ['unshift!', 1, 2, 3, 'push!']
```

- push 배열 끝에 요소를 추가시킨다.
- unshift 배열 앞에 요소를 추가시킨다.
- 배열의 length를 반환한다.
- **기존 배열을 변경한다.**

---

### 📌 2. pop & shift

```jsx
let arr = ['unshift!', 1, 2, 3, 'push!'];

console.log(arr.pop());// push!console.log(arr);// ['unshift!', 1, 2, 3]console.log(arr.shift());// unshift!console.log(arr);// [1, 2, 3]
```

- pop 배열 끝의 요소를 제거한다.
- unshift 배열 앞의 요소를 제거한다.
- 제거한 요소를 반환한다.
- **기존 배열을 변경한다.**

---

### 📌 3. concat

```yaml
let arr1 = [1, 2];
let arr2 = [3, 4];
let arr3 = [5, 6];

console.log(arr1.concat(arr2)); // [1, 2, 3, 4]
console.log(arr1.concat(arr2, arr3, 7)); // [1, 2, 3, 4, 5, 6, 7]
```

- 인자로 주어진 배열이나 값을 기존 배열에 합친다.
- 합친 배열을 반환한다.
- **기존 배열이나 값을 변경하지 않는다.**

---

### 📌 4. slice

```yaml
arr.slice(begin, end)

let arr = [1, 2, 3, 4, 5];

console.log(arr.slice(2, 4)); // [3, 4]
console.log(arr); // [1, 2, 3, 4, 5]
```

- begin(포함)부터 end 전까지의 요소가 담긴 배열을 return한다.
- **기존 배열을 변경하지 않는다.**

---

### 📌 5. splice

```
array.splice(start, deleteCount, item1, item2, ...)

let arr = [1, 2, 3, 4];

console.log(arr.splice(0, 2)); // [1, 2]
console.log(arr); // [3, 4]

console.log(arr.splice(2, 1, 123)); // [3]
console.log(arr); // [1, 2, 123, 4]
```

- 배열을 추가, 제거할 수 있다.
- 제거한 요소가 담긴 배열을 반환한다.
- **기존 배열을 변경한다.**

---

### 📌 6. filter

```yaml
arr.filter(callback(currentValue, index, array), thisArg)

let arr = [1, 2, 3, 4, 5, 6, 7, 8];

let result = arr.filter((val) => {
	return val % 2 === 0;
});

console.log(result); // [2, 4, 6, 8]
console.log(arr); // [1, 2, 3, 4, 5, 6, 7, 8]
```

- 콜백함수에서 조건을 만족하는 요소를 담은 새로운 배열을 반환한다.
- currentValue : 처리할 현재 요소이다.
- index : 처리할 현재 요소의 인덱스이다.
- array : map을 호출한 배열이다.
- thisArg : callback을 사용할 때 this로 사용하는 값이다.
- **기존 배열을 변경하지 않는다.**

---

### 📌 7. map

```yaml
arr.map(callback(currentValue, index, array), thisArg)

let arr = [1, 2, 3, 4, 5];

let result = arr.map((val) => {
	return val += 5 ;
});

console.log(arr); // [1, 2, 3, 4, 5]
console.log(result); // [6, 7, 8, 9, 10]
```

- 콜백함수를 실행한 결과를 담은 새로운 배열을 반환한다.
- currentValue : 처리할 현재 요소이다.
- index : 처리할 현재 요소의 인덱스이다.
- array : map을 호출한 배열이다.
- thisArg : callback을 사용할 때 this로 사용하는 값이다.
- **기존 배열을 변경하지 않는다.**

---

### 📌 8. forEach

```yaml
arr.forEach(callback(currentValue, index, array), thisArg)

let arr =[1, 2, 3, 4, 5];

arr.forEach(function(el, index) {
  arr[index] += 3;
});

console.log(arr);   // [4, 5, 6, 7, 8];
```

- 주어진 함수를 배열 요소 각각에 대해 실행하고 그 결과를 모은 배열을 반환한다.
- currentValue : 처리할 현재 요소이다.
- index : 처리할 현재 요소의 인덱스이다.
- array : map을 호출한 배열이다.
- thisArg : callback을 사용할 때 this로 사용하는 값이다.
- **기존 배열을 변경한다.**

---

### 📌 9. fill

```
arr.fill(value, start, end)

let arr = [1, 2, 3, 4, 5];

console.log(arr.fill("hi!")); // ['hi!', 'hi!', 'hi!', 'hi!', 'hi!']
console.log(arr.fill("bye!", 1, 4)); // ['hi!', 'bye!', 'bye!', 'bye!', 'hi!']
console.log(arr.fill("ok!", 2)); // ['hi!', 'bye!', 'ok!', 'ok!', 'ok!']

console.log(arr) // ['hi!', 'bye!', 'ok!', 'ok!', 'ok!']
```

- start(포함)부터 end 전까지를 value로 채운다.
- start, end값이 없다면 value로 가득 채운다.
- **기존 배열을 변경한다.**

---

### 📌 10. includes

```
arr.includes(valueToFind, fromIndex)

let arr = ['Kim', 'Park', 'Choi'];

console.log(arr.includes('Kim')); // true
console.log(arr.includes('Son')); // false
console.log(arr.includes('Kim', 2)); // false
```

- 배열에 요소 포함 여부를 boolean으로 반환한다.
- fromIndex는 이 배열에서 검색을 시작할 위치이고, 기본값은 0이다.

---

### 📌 11. join

```
arr.join(separator = ',');

let arr = [1, 2, 3, 4, 5];

console.log(arr.join());// 1,2,3,4,5
console.log(arr.join('-'));// 1-2-3-4-5
console.log(arr.join(''));// 12345
console.log(arr);// [1, 2, 3, 4, 5]
```

- 배열을 문자열로 결합하여 반환한다.
- separator는 배열을 문자열로 결합할 때 이어 붙일 값이며, 기본값은, 이다.
- **기존 배열을 변경하지 않는다.**

---

### 📌 12. reduce

```
arr.reduce(callback(total, currentValue, currentIndex, arr), initialValue)

let arr =[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];

let value = arr.reduce( function( total, currentValue, currentIndex ) {
  return previousValue + currentValue;
});

console.log( value );// 55
```

- 배열의 각 요소에 대해 주어진 함수를 실행하고, 하나의 결과값을 반환한다.
- total : 초기 값 또는 이전에 반환된 함수 값이다.
- currentValue : 현재 요소의 값이다.
- currentIndex : 현재 요소의 인덱스이다.
- arr : 현재 요소가 속한 배열이다.
