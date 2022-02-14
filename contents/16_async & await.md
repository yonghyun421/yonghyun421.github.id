---
date: '2022-01-12'
title: 'async & await'
categories: ['React', 'TIL', 'async&await']
summary: 'async 그리고 await'
thumbnail: './images/async.png'
---

# async & await

## async/await 키워드를 통한 비동기 코딩

Promise의 불편한 점들을 해결하기 위해 ES7에서 async/await 키워드가 추가되었다. async/await 키워드를 사용하면 비동기 코드를 마치 동기 코드처럼 보이게 작성할 수 있다.

함수 선언부를 보면 async 키워드가 function 앞에 붙는다는 것과 Promise를 리턴하는 모든 비동기 함수 호출부 앞에는 await 키워드가 추가되었다는 것을 확인할 수 있다.

await 키워드는 async 키워드가 붙어있는 함수 내부에서만 사용할 수 있으며 비동기 함수가 리턴하는 promise로부터 결과값을 추출해준다. 즉 await 키워드를 사용하면 일반 비동기처리처럼 바로 실행이 다음 라인으로 넘어가는 것이 아니라 결과값을 얻을 수 있을 때까지 기다려 준다. 따라서 일반적인 동기 코드 처리와 동일한 흐름으로 (함수 호출 후 결과값을 변수에 할당하는 식으로) 코드를 작성할 수 있으며, 따라서 코드를 읽기도 한결 수월해진다.

한가지 주의할점은 async 키워드가 붙어있는 함수를 호출하면 명시적으로 promise 객체를 생성하여 리턴하지 않아도 promise 객체가 리턴된다. 하지만 만약 이 호출부가 또 다른 async 키워드가 붙어있는 함수의 내부에 있다면 동일한 방식으로 await 키워드를 사용하여 promise가 제공할 값에 바로 접근할 수 있다.

## 예외 처리

동기/비동기 구분없이 try/catch로 일관되게 예외 처리를 할 수 있는 부분도 async/await를 사용해서 코딩했을 때의 큰 이점 중 하나이다.
