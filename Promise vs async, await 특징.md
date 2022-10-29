## Promise

Promise는 자바스크립트에서 비동기 처리에 사용되는 객체이다.**내용은 실행 되었지만 결과를 아직 반환하지 않은 객체**라고 이해해도 좋다.

Promise 에는 3가지 상태가 있는데

- **Pending** (대기)
- **Fulfilled** (이행)
- **Rejected** (실패)

비동기 처리가 완료 되지 않았다면 Pending, 완료 되었다면 Fulfilled, 실패하거나 오류가 발생하였다면 Rejected 상태를 갖는다.

### Promise 사용 예시

```coffeescript
const condition = true;
const promise = new Promise((resolve, reject) => {
  if (condition) {
    resolve('resolved');
  } else {
    reject('rejected');
  }
});

promise
  .then((res) => {
    console.log(res);
  })
  .catch((error) => {
    console.error(error);
  });
```

condition 값의 따라 promise의 반환 값이 결정 되고 있다.

값이 참이면 resolve 를 호출하고, 아닐시에는 reject 를 호출한다.resolve 한 반환 값에 대해서는 then() 을 통해 결과 값을 반환 받을 수 있고 reject 의 반환 값에 대해서는 catch() 를 통해 반환 받는다.

then() 과 catch() 문의 체이닝을 통해 비동기 로직의 성공 여부에 따른 분기 처리가 가능하다.

## async / await

가장 최근의 나온 비동기 처리 문법으로 기존의 callback 이나 Promise 의 단점을 해소하고자 만들어졌다.

callback 이나 Promise 의 경우에 단점은 꼬리에 꼬리를 무는 코드가 나올 수도 있다는 부분이다. 흔히들 콜백 지옥, then() 지옥이라고 부른다.

await 를 통해 Promise 반환 값을 받아 올 수 있다.

```
const variable =  await promise;
// promise의 반환 값을 받아 variable
```

하지만 async/await 를 사용하기 위해서는 선행되어야 하는 조건이 있는데, await 는 async 함수 안에서만 동작한다.

사용 예시를 한번 보자.

### async / await 사용예시

```clojure
(async () => {
  const condition = true;
  const promise = new Promise((resolve, reject) => {
    if (condition) {
      resolve('resolved');
    } else {
      reject('rejected');
    }
  });

  try {
    const result = await promise;
    console.log(result);
  } catch (err) {
    console.error(err);
  }
})();
```

위의 Promise 사용 코드를 async/await 를 사용하여 코드를 변경하였다.익명 함수 패턴을 활용하였다. async 함수 내의 await 를 통해 Promise 의 반환 값을 result 변수에 담아 콘솔에 출력하는 코드이다.

그리고 주의할 점은 async/await 은 Promise 와는 다르게 에러를 핸들링 할 수 있는 기능이 없다. 따라서 try-catch() 문을 활용하여 에러를 핸들링 하여 주어야 한다.

## 차이점

- **에러 핸들링**
    - Promise 를 활용할 시에는 .catch() 문을 통해 에러 핸들링이 가능하지만, async/await 은 에러 핸들링 할 수 있는 기능이 없어 try-catch() 문을 활용해야 한다
- **코드 가독성**
    - Promise의 .then() 지옥의 가능성
    - 코드가 길어지면 길어질수록, async/await 를 활용한 코드가 가독성이 좋다.
    - async/await 은 비동기 코드가 동기 코드처럼 읽히게 해준다. 코드 흐름을 이해 하기 쉽다.
