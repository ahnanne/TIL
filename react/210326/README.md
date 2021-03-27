# 21/03/26 학습 내용

### `useReducer` 사용 방법

#### 1. `useReducer`를 사용하기 위해 준비할 재료

  1) **reducer 함수** → `useReducer`의 첫 번째 인자

      - 순수 함수여야 함.

      - `(state, action) => newState` 형태여야 함.

      - 보통 <switch문>을 사용함.

        - <switch문>의 `case`를 정의할 때는, 문자열을 직접 하드코딩하는 것보다 <u>미리 상수를 선언</u>해두면 ①typo를 방지할 수도 있고 ②유지보수도 편리하다는 장점이 있음.

  2) **initial state(초기 상태)** → `useReducer`의 두 번째 인자

      - 보통은 숫자나 문자열 등의 원시 타입보다는, <b>참조형 데이터(객체, 배열)</b>를 상태로서 관리함. (원시 타입, 즉 비교적 단순한 상태를 관리할 목적이면 `useState`를 사용하는 것이 더 나은 선택일 수 있음.)

      - 그러므로 초기 상태로 전달할 객체나 배열이 필요함.

#### 2. `useReducer`를 호출하고, 그 반환값을 배열 디스트럭처링 할당으로 받아오기

  ```js
  const [state, dispatch] = React.useReducer(reducer, initialState)
  ```

  - 만약 지연된 초기화를 사용하고 싶다면, `useReducer`의 세 번째 인자로는 지연된 초기화를 하기 위한 로직(함수)을 전달하면 됨.

  - 이렇게 호출한 `useReducer`는 두 개의 요소를 갖는 배열을 반환하는데, <b>첫 번째 요소</b>는 `useReducer`가 관리하게 되는 상태이며 <b>두 번째 요소</b>는 dispatch 역할을 하는 함수임.

    - dispatch 함수는 action 객체를 인자로 전달 받고, 이를 reducer 함수에 전달하여 reducer 함수가 호출됨.

    - dispatch 함수가 인자로 받는 action 객체는 하나 이상의 프로퍼티를 가짐.

      - `type`(필수) : reducer 함수의 <switch문>에서, 이 type 값이 뭔지에 따라서 새로운 state를 반환하게 됨.

      - 나머지 payloads : 새로운 state를 만들 때 필요한 값이 있다면 나머지 인자로서 전달해주면 됨. (이름은 상관 없음.)

#### 3. 엘리먼트의 이벤트 핸들러로 dispatch 함수 등록하기

#### 4. 잘 동작하는지 확인하기🙄

___
### `componentDidCatch(error, info)` 메서드

- `componentDidCatch` 메서드는 클래스형 컴포넌트의 life cycle method 중 하나로, 하위 컴포넌트에서 아직 발견하지 못한 에러가 발생할 경우 사용자에게 에러가 발생했음을 알려줄 수 있음.

- `componentDidCatch` 메서드는 하위 컴포넌트에서 에러가 발생했을 때 호출되는데, 이때 다음의 두 가지 인자를 전달 받음.

  1. `error` : 발생한 에러

  2. `info` : 어떤 컴포넌트가 에러를 발생 시켰는지에 대한 정보(`componentStack` 프로퍼티)를 갖고 있는 객체

    - `info.componentStack`은 에러 로그 기록을 위해 사용할 수 있음.

- Sentry

  - Sentry([링크](https://sentry.io/welcome/))는 애플리케이션에서 에러가 발생했을 때, 해당 에러에 대한 정보를 외부로 보내서 실시간으로 확인할 수 있게 도와주는 에러 모니터링 플랫폼임.

  - 사용 방법 [참고](https://react.vlpt.us/basic/26-componentDidCatch-and-sentry.html)