---
date: '2022-01-10'
title: 'useRef'
categories: ['React', 'TIL', 'Hooks']
summary: 'useRef가 뭐지?'
thumbnail: './images/useRef.jpeg'
---

# useRef란?

useRef는 .current 프로퍼티로 전달된 인자(initialValue)로 초기화된 변경 가능한 ref 객체를 반환한다.
반환된 객체는 컴포넌트의 전 생애주기를 통해 유지된다.
본직적으로 useRef는 .current 프로퍼티에 변경 가능한 값을 담고 있는 상자와 같다.

## useRef를 언제 사용할까?

### 특정 DOM 선택하기

JavaScript를 사용할 때는, 특정 DOM을 선택해야 하는 상황에 getElementById, querySelector, 같은 DOM Selector 함수를 사용해서 DOM을 선택한다.

리액트에서는 DOM을 선택할 때 ref를 사용한다.
함수형 컴포넌트에서 ref를 사용할 때는 useRef라는 Hook 함수를 사용하고 클래스형 컴포넌트에서는 콜백 함수를 사용하거나 React.createRef 함수를 사용한다.

### 컴포넌트 안의 변수 만들기

컴포넌트 안에서 조회 및 수정할 수 있는 변수를 관리할 수 있다.

useRef로 관리하는 변수는 값이 바뀐다고 해서 컴포넌트가 리렌더링되지 않는다. 리액트 컴포넌트에서의 상태는 상태를 바꾸는 함수를 호출하고 나서 그다음 렌더링 이후로 업데이트된 상태를 조회할 수 있지만, useRef로 관리하는 변수는 설정 후 바로 조회할 수 있다.

이 변수를 사용하여 관리할 수 있는 값

- setTimeout, setInterval을 통해서 만들어진 id
- 외부 라이브러리를 사용하여 생성된 인스턴스
- scroll 위치

### 리렌더링 방지하기

컴포넌트가 렌더링 된다는 것은 함수(컴포넌트)를 호출하여 실행되는 것을 말한다. 함수가 실행될 때마다 내부에 선언되어 있던 표현식(변수나 또 다른 함수 등)도 매번 다시 선언되어 사용한다.

컴포넌트는 자신의 state가 변경되거나, 부모에게서 받는 props가 변경되었을 때마다 리렌더링 된다.

심지어 하위 컴포넌트에 최적화 설정을 해주지 않으면 부모에게서 받는 props가 변경되지 않았더라도 리렌더링 된다.

useRef로 관리하는 변수는 값이 바뀐다고 해서 컴포넌트가 리렌더링되지 않으므로 리렌더링 방지에 활용할 수 있다.

## useRef로 DOM 선택하는 방법

useRef()를 사용하여 Ref 객체를 만들고, 이 객체를 선택하고 싶은 DOM에 ref 값으로 설정한다. 그러면 Ref 객체의 .current 값은 DOM을 가리키게 된다.

## useRef로 컴포넌트 안의 변수 만드는 방법

useRef()를 사용할 때 파라미터를 넣어주면, 이 값이 .current 값의 기본값이 된다. 그리고 이값을 수정할 때는 .current 값을 수정하면 되고 조회할 때는 .current를 조회하면 된다.

## 리렌더링 방지하기

onChange 구현 부분을 ref 값으로 대체해서 리렌더링을 방지할 수 있다. state 로 event의 value에 접근하지 않고 refObject.current.value를 사용하는 방법이다.
