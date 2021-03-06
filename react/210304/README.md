# 21/03/04 수업 내용
### Hook

- Hook이란? ([참고](https://ko.reactjs.org/docs/hooks-overview.html#but-what-is-a-hook))

  > Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수입니다. ([참고](https://ko.reactjs.org/docs/hooks-overview.html#but-what-is-a-hook))

- Hook을 도입한 이유 ([참고](https://reactjs.org/docs/hooks-intro.html#complex-components-become-hard-to-understand))

  > Hook은 props, state, context, refs, 그리고 lifecycle와 같은 React 개념에 **좀 더 직관적인 API를 제공**합니다. ([참고](https://ko.reactjs.org/docs/hooks-intro.html#no-breaking-changes))

  1. 재사용성 측면

    - 기존에 리액트에서는 컴포넌트들 간에 상태 로직을 재사용하기 어려웠음.

    - Hook을 사용하면 요소로부터 상태 로직을 추출하여 재사용 가능하게 함으로써 이와 같은 기존의 문제점을 개선함.

    - 즉, **Hook은 우리가 컴포넌트 계층(구조)를 변경하지 않더라도 상태 로직을 재사용할 수 있도록 함**.

  2. 컴포넌트 분리 측면

    - 또한 **Hook은 하나의 컴포넌트를 서로 연관된 부분들로만 이루어진 함수들로 쪼갤 수 있도록 해줌**.

    - Hook 도입 이전에는 *lifecycle methods*를 기준으로 컴포넌트를 나누었고 상태 로직들이 이곳저곳 흩어져있었기 때문에 컴포넌트를 이런 식으로 쪼개는 것이 어려웠음.

      - 이는 컴포넌트들을 복잡하게 만들어 사용자들이 컴포넌트를 쉽게 이해하지 못하게 했음.

  3. 클래스 관련 측면 ([참고](https://reactjs.org/docs/hooks-intro.html#classes-confuse-both-people-and-machines))

    > Hook은 class 안에서는 동작하지 않습니다. 대신 class 없이 React를 사용할 수 있게 해주는 것입니다. (하지만 이미 짜놓은 컴포넌트를 모조리 재작성하는 것은 권장하지 않습니다. 대신 새로 작성하는 컴포넌트부터는 Hook을 이용하시면 됩니다.) ([참고](https://ko.reactjs.org/docs/hooks-overview.html#but-what-is-a-hook))

    > 함수 컴포넌트를 사용하던 중 state를 추가하고 싶을 때 클래스 컴포넌트로 바꾸곤 했을 겁니다. 하지만 이제 함수 컴포넌트 안에서 Hook을 이용하여 state를 사용할 수 있습니다. ([참고](https://ko.reactjs.org/docs/hooks-state.html#whats-a-hook))

    - Hook은 리액트의 많은 기능들을 **클래스를 사용하지 않고도** 이용할 수 있도록 함.

    - 기존에는 클래스 컴포넌트와 함수 컴포넌트를 각각 어떤 때 사용하는 게 좋은 지에 대해서 의견이 분분하기도 했고, 클래스가 사용자들에게 혼란을 주기도 하고 *minify*하기가 어렵다는 점 등, 클래스와 관련하여 리액트를 사용하는 데 몇 가지 걸림돌이 있었음.

- 내장 Hook

  - 앞서 학습한 `useState` 역시 React가 제공하는 내장 Hook의 하나임.

    > `useState`는 state를 함수 컴포넌트 안에서 사용할 수 있게 해줍니다. ([참고](https://ko.reactjs.org/docs/hooks-state.html#whats-a-hook))

  - 컴포넌트들 간에 상태 로직을 재사용하기 위해 Hook을 직접 만드는 것도 가능하나, 우선은 내장 Hook에 대해서 먼저 살펴보자.

  1. State Hook

    - `useState`

  2. Effect Hook

    - `useEffect`

      > `useEffect`는 함수 컴포넌트 내에서 이런 side effects를 수행할 수 있게 해줍니다. React class의 `componentDidMount` 나 `componentDidUpdate`, `componentWillUnmount`와 같은 목적으로 제공되지만, 하나의 API로 통합된 것입니다. ([참고](https://ko.reactjs.org/docs/hooks-overview.html#effect-hook))

  3. 기타

    - https://ko.reactjs.org/docs/hooks-reference.html 참고

- Hook 사용 규칙([참고](https://ko.reactjs.org/docs/hooks-overview.html#rules-of-hooks))

  - Hook을 사용할 때는 아래의 두 가지 규칙을 준수해야 함.

  1. **최상위**에서만 Hook을 호출해야 함.

    - 반복문, 조건문, 중첩 함수 내에서 Hook을 실행하지 말 것!

  2. **리액트 함수 컴포넌트** 내에서만 Hook을 호출해야 함.

    - 일반 자바스크립트 함수에서는 호출하지 말 것!

  - cf.) custom Hook 내부에서도 Hook을 호출할 수 있다고 함.

___
### `useEffect`

- 리액트 공식 문서 [참고](https://ko.reactjs.org/docs/hooks-effect.html)

- side effects

  - 리액트 컴포넌트에는 일반적으로 두 종류의 side effects가 있음.

    1. 정리(clean-up)가 필요하지 않은 것 => return문 X

    2. 정리(clean-up)가 필요한 것 => return문 O

- 정리(clean-up)를 이용하지 않는 Effects

  > 리액트가 DOM을 업데이트한 뒤 추가로 코드를 실행해야 하는 경우가 있습니다. 네트워크 리퀘스트, DOM 수동 조작, 로깅 등은 정리(clean-up)가 필요 없는 경우들입니다. 이러한 예들은 실행 이후 신경 쓸 것이 없기 때문입니다.

  > 리액트는 **effect가 수행되는 시점에 이미 DOM이 업데이트되었음**을 보장합니다.


- 정리(clean-up)를 이용하는 Effects

  - 어떤 동작을 **추가**하는 코드와 **제거**하는 코드는 결합도가 높기 때문에 `useEffect`는 두 가지를 함께 다루게 되어있음.

  - effect가 return문으로 반환하는 함수는 '정리가 필요한 때'에 실행됨.

  - 모든 effect는 이와 같은 '정리를 위한 함수'를 반환할 수 있으며, 결국 어떤 동작의 **추가**와 **제거**가 하나의 effect를 구성함.

    - 물론 정리가 필요하지 않은 경우에는 아무것도 반환하지 않아도 됨.

- `useEffect`를 컴포넌트 안에서 불러내는 이유

  - `useEffect`를 컴포넌트 안에 두면, API 없이도 effect를 통해 state 변수 또는 props에 접근할 수 있음.

  - effect란 `useEffect`의 인수로 전달한 함수를 의미함.

- `useEffect`는 **마운팅**(=첫 번째 렌더링)과 이후의 모든 **업데이트**에서 수행됨.

(https://ko.reactjs.org/docs/hooks-effect.html#detailed-explanation 부터 이어서..)

___
### `useEffect` 사용 실습

- `useEffect`를 사용하면, 우리가 만든 컴포넌트가 화면에 나타나게 될 때와 화면에서 사라지게 될 때 특정 작업을 할 수 있고, 컴포넌트의 props나 state가 업데이트 될 때도 특정 작업을 할 수 있음. 리렌더링 될 때마다 수행할 작업을 등록할 수도 있음.

- **mount**는 컴포넌트가 나타나는 것을 의미하고, **unmount**는 컴포넌트가 사라지는 것을 의미함.
