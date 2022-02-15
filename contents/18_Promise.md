---
date: '2021-12-14'
title: 'Promise'
categories: ['React', 'TIL', 'Javascript', 'Promise']
summary: 'Callback Hell에서 빠져나오기 위한 방법.'
thumbnail: './images/promise.jpg'
---

# Promise

- 자바스크립트 비동기 처리에 사용되는 객체
  > #### 비동기 처리
  >
  > 특정 코드의 연산이 끝날 때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 자바스크립트의 특성을 의미한다.

## Promise의 3가지 상태(states)

상태는 프로미스의 처리과정을 의미.

1. Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태.
2. Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태.
3. Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태.

## Producer

- 새로운 Promise가 만들어질때는 우리가 전달한 executor라는 함수가 자동적으로 실행이 된다.

```js
const promise = new Promise((resolve, reject) => {
  // doing some heavy work (network, read files)
  setTimeout(() => {
    resolve('yonghyun') // 성공한 경우
    reject(new Error('에러 발생 이유')) // 실패한 경우
  }, 2000)
})
```

=> 어떤 일을 2초정도 하다가 resolve라는 콜백함수를 호출하면서 yonghyun이라는 값을 전달해주는 Promise

## Consumers : then, catch, finally

### then

Promise가 정상적으로 잘 수행이 되어서 마지막에 최종적으로 resolve라는 콜백함수를 통해서 전달한 값이 value에 parameter로 전달된다.

```js
promise
  .then(value => {
    // 성공한 값
    console.log(value) // yonghyun이 출력
  })
  .catch(error => {
    // 실패한 에러
    console.log(error)
  })
  .finally(() => {
    // 성공, 실패 여부에 상관없이 무조건 실행
    console.log('finally')
  })
```

## Promise chaining

```js
const fetchNumber = new Promise((resolve, reject) => {
  setTimeout(() => resolve(1), 1000)
})

fetchNumber
  .then(num => num * 2)
  .then(num => num * 3)
  .then(num => {
    return new Promise((resolve, reject) => {
      setTimeout(() => resolve(num - 1), 1000)
    })
  })
  .then(num => console.log(num))
```

## Error Handling

```js
const getHen = () =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve('닭'), 1000)
  })
const getEgg = hen =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve(`${hen} => 계란`), 1000)
  })
const cook = egg =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve(`${egg} => 사탕`), 1000)
  })

getHen()
  .then(getEgg)
  .catch(error => {
    return '빵'
  }) // 에러가 발생한 걸 바로 잡아낼 수 있다.
  .then(cook)
  .then(console.log)
  .catch(console.log)
```
