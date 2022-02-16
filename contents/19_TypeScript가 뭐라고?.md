---
date: '2021-12-04'
title: 'TypeScript가 뭐라고?'
categories: ['React', 'TIL', 'Typescript', 'JavaScript']
summary: 'TypeScript 맛좀 봅시다!'
thumbnail: './images/ts.png'
---

# TypeScript

2012년 마이크로소프트사에서 오픈소스로 공개한 컴파일 투 자바스크립트 언어.
타입스크립트 프로그램은 자바스크립트로 트랜스파일 해야 브라우저나 자바스크립트 엔진에서 실행된다.
타입스크립트는 자바스크립트의 상위 집합으로 모든 ECMA 버전의 자바스크립트 파일을 사용할 수 있다.

## JS와 TS 차이점

타이핑은 프로그램 변수에 타입을 정의하는 것을 말하는데, 타입스크립트가 `정적 타이핑`을 지원하는 반면, 자바스크립트 집합은 `동적 타이핑`만을 지원한다.
정적 타입 프로그래밍 언어는 변수를 사용하기 전 타입을 반드시 할당해야 한다. 그렇기 때문에 타입스크립트는 변수의 타입을 선언한 후 이를 다른 타입으로 바꾸게 되면 컴파일 오류가 발생한다. 자바스크립트는 프로그램이 실행 중인 런타임에서도 변수 타입에 대해 알지 못하기 때문에, 변수 타입을 변경 할 수 있다.

## TypeScript 사용해보기

### 새 타입스크립트 프로젝트 시작

새 타입스크립트 프로젝트를 시작하려면 원하는 위치에서 명령어 `tsc --init` 을 입력한다. 컴파일러의 모든 옵션이 주석 처리되어 있는 `tsconfig.json` 이 생성될 것이다. 여기서 필요한 설정만 주석처리를 해제하고 작업을 시작한다.

### ts 파일 js로 변환하기

main.ts 파일을 만들고 잘못된 타입이 입력된 상태로

```bash
tsc main
```

다음과 같은 명령어를 실행하면 컴파일 오류가 발생함에도 불구하고 자바스크립트 파일이 생성된다. 자바스크립트 관점에서 보면 main.js 파일은 유효하기 때문이다. 그러나 실제 타입스크립트 프로젝트에서는 오류가 있는 파일을 생성할 수 없다. 그렇기 때문에

```bash
tsc main --noEmitOnError true
```

위와 같이 명령어를 사용할 경우 타입스크립트 컴파일러는 모든 오류가 고쳐질 때까지 이전에 생성된 자바스크립트 파일을 덮어 쓰지 않는다.

## 기본 타입과 커스텀 타입

타입스크립트는 변수 선언 후, 타입과 함께 세미콜론을 붙인다.

```ts
let firstName: string
let age: number
```

### 주요 타입

- string - 문자열
- bloolean - true/false
- number - 숫자
- symbol - Symbol 생성자를 호출해 생성된 고유값
- any - 모든 타입을 허용하는 타입
- unknown - any와 비슷하나 먼저 타입을 지정하거나 좁히지 않으면 조작이 허용되지 않음
- never - 도달할 수 없는 코드를 나타냄
- void - 값이 없음

any 타입을 사용하면 타입 체크의 장점을 잃고 코드 가독성도 떨어지기 때문에 되도록이면 사용하지 않는 것이 좋다.

타입스크립트 내 타입 표기는 선택사항이다. 일부 변수에 타입 표기가 없다면 타입스크립트의 타입 검사기는 해당 타입을 유추한다.

```ts
let name1 = 'John Smith' // 타입 없이 변수를 선언 및 초기화
let name2: string = 'Jogh Smith' // 타입을 추가해 변수를 선언 및 초기화
```

### Union Type

유니온은 OR 연산자처럼 변수에 지정할 수 있는 타입이 여러 개일 경우 사용한다. 아래와 같이 문자열 또는 숫자를 허용하는 변수를 선언할 수 있다.

```ts
let nickName: string | number
```

> #### typeof와 instanceof
>
> 조건문을 적용해 변수 타입을 세분화하는 것을 타입 축소라고 한다.
> typeof는 타입스크립트 내장 타입에 사용되며, instanceof은 사용자가 만든 타입에 사용된다는 차이가 있다.

### 커스텀 타입

타입스크립트는 type, interface, enum 키워드 및 클래스 선언으로 커스텀 타입을 만들 수 있다.

#### type 키워드

type 키워드는 새로운 타입을 선언하거나 타입 별칭을 사용해 이미 존재하는 타입에 다른 이름을 붙여 사용할 수 있다.

```ts
type Hand = number
type Weight = number

type Patient = {
  name: string
  height: Hand // Hand 타입 별칭 사용
  weight: Weight // Weight 타입 별칭 사용
}

let patient: Patient = {
  name: 'Kim',
  height: 3,
  weight: 50,
}
```

만약 해당 프로퍼티가 필수가 아닌 옵션 사항일 경우에는 프로퍼티 이름에 ?를 붙여 조건부 프로퍼티임을 선언한다. 이렇게 하면 해당 프로퍼티가 없어도 그에 따른 오류가 발생되지 않는다.

#### class 내 커스텀 타입 사용

```ts
class Person {
  constructor(
    public firstName: string,
    public lastName: string,
    public age: number,
  ) {}
}

const p = new Person('Kim', 'Mike', 30)
```

#### readonly

변경 불가능한 상수를 나타내는 constt 키워드와 비슷ㅅ하지만, const는 클래스 프로퍼티에 사용할 수 없다.

#### interface를 사용한 커스텀 타입

```ts
interface Person {
  firstName: string
  lastName: string
  age: number
}
```

> #### type, interface, class를 언제 사용해야 할까?
>
> 런타임 동안 객체를 인스턴스화한다면 interface 또는 type을 사용하고, 그 반대의 경우는 class를 사용한다. 즉 값을 나타내는 데 사용해야 하는 경우 class를 사용한다.
> type과 interface는 자바스크립트 코드로 컴파일되지 않으므로 런타임 코드 용량이 더 작아지지만 class는 자바스크립트 코드로 컴파일되기 때문에 용량이 커진다.
> 또한 type 키워드는 interface와 동일한 기능뿐만 아니라 더 많은 기능을 사용할 수 있다.

> #### 타입 가드 in
>
> 타입 가드 in 키워드는 타입 범위를 축소하는 표현이다. 예를 들어 유니온 타입 인자를 가진 함수는 호출하는 동안 실제 값을 체크할 수 있다.

```ts
interface A {
  a: number
}
interface B {
  b: string
}
function foo(x: A | B) {
  if ('a' in x) {
    return x.a
  }
  return x.b
}
```
