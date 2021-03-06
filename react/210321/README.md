# 21/03/21 학습 내용
### `useRef()`

- 이하의 내용은 리액트 공식 문서의 설명을 참고하였음. ([링크](https://reactjs.org/docs/hooks-reference.html#useref))

- `useRef()`는 변경 가능한 ref 객체를 반환하는데, 이 ref 객체가 갖는 `current` 프로퍼티는 `useRef()`의 인자로 전달한 값을 초기값으로 갖게 됨.

- 기본적으로 `useRef()`는 마치 상자같다. 이 상자는 자신의 안에 있는 `current` 프로퍼티를 통해 변경 가능한 값을 지니게 된다.

- useRef로 관리하는 값은, 값이 바뀌어도 컴포넌트가 리렌더링이 되지 않는다!

  - 즉, `current` 프로퍼티의 값을 바꾼다고 해도 리렌더링이 일어나지 않는다.

- `useRef`는 언제 사용하나?

  - 실제 DOM 노드를 참조할 경우 사용한다.

  - 참조 대상을 변경해야 할 경우 `current` 프로퍼티의 값을 변경하면 된다.

___
### ref

- 이하의 내용은 리액트 공식 문서의 설명을 참고하였음. ([링크](https://ko.reactjs.org/docs/refs-and-the-dom.html))

> Ref는 render 메서드에서 생성된 DOM 노드나 React 엘리먼트에 접근하는 방법을 제공합니다.

- Ref 사용 사례

  - **바람직한 경우**

    - 포커스, 텍스트 선택 영역, 미디어 재생 등을 관리할 때

    - 애니메이션을 직접적으로 실행시킬 때

    - 3rd party DOM library를 리액트와 함께 사용할 때

  - **바람직하지 않은 경우**

    - 선언적으로 해결될 수 있는 문제에 대해서는 사용 지양

      - ex) `Dialog` 컴포넌트(모달)를 열고 닫을 때는 `open()`, `close()` 메서드를 두는 대신, `isOpen`이라는 prop을 넘겨주는 게 좋음.

- 클래스 컴포넌트에서는 `React.createRef()`를 통해 Ref 객체를 생성하고, 함수 컴포넌트에서는 `useRef()`를 통해 Ref 객체를 생성함.

  ![image](https://user-images.githubusercontent.com/54733637/111910553-2fbbb600-8aa5-11eb-85d5-77d21dfe8902.png)

  - 이렇게 생성된 Ref 객체는 `current`라는 프로퍼티를 가지며, `ref` 어트리뷰트를 통해 리액트 엘리먼트에 부착됨.

- Ref 객체가 부착된 리액트 엘리먼트 → 이 노드에 대한 참조는 `current` 프로퍼티에 담기게 됨.

  - **이때!!!** Ref 객체를 부착할 수 있는(=`ref` 어트리뷰트를 설정할 수 있는) 리액트 엘리먼트는 **①HTML 엘리먼트** 또는 **②클래스 컴포넌트**임.

    - **함수 컴포넌트는 <u>인스턴스가 없으므로</u>, 함수 컴포넌트에는 `ref` 어트리뷰트를 사용할 수 없음.**

  - Ref 객체가 **①HTML 엘리먼트**에 부착될 경우 → 해당 엘리먼트로 생성된 DOM 엘리먼트에 대한 참조가 Ref 객체의 `current` 프로퍼티 값이 됨.

  - Ref 객체가 **②클래스 컴포넌트**에 부착될 경우 → 해당 클래스 컴포넌트 출신의, 마운트된 인스턴스에 대한 참조가 Ref 객체의 `current` 프로퍼티 값이 됨.

![image](https://user-images.githubusercontent.com/54733637/111910731-ecae1280-8aa5-11eb-8b59-d73d686104d5.png)

___
### 기타

- Hook 사용 시 주의할 점

  - Hook은 함수형 컴포넌트 안에서만 사용할 수 있음.

  - Hook은 컴포넌트의 `반복문`, `조건문`, `중첩 함수` 내에서는 **사용할 수 없음**.

- 함수형 컴포넌트의 `useState`는 클래스형 컴포넌트에서 state를 다루는 것과 달리, 데이터(상태)를 개별적으로 관리해줘야 함.

  - 하지만 `useState`에 객체를 전달해주면 하나의 state 안에 여러 정보를 관리할 수 있음.

    ```js
    const [title, setTitle] = useState('Learn React');
    const [day, setDay] = useState('Wed');

    // ↓ 두 개의 상태를 하나의 객체 안에서 관리
    const [state, setState] = useState({
      title: 'Learn React',
      day: 'Wed',
    });
     ```

- 지연된 초기화(lazy initialization)

  - 리액트에서는 `useState`의 인자로 함수를 전달함으로써 어떤 값에 대해 지연된 초기화를 구현할 수 있음.

    - 리액트에서의 지연된 초기화란 `useState`에 전달된 함수가 실행되는 것을 의미함.

  - 지연된 초기화란? ([참고](https://ko.wikipedia.org/wiki/%EC%A7%80%EC%97%B0%EB%90%9C_%EC%B4%88%EA%B8%B0%ED%99%94))

    > 지연된 초기화란 컴퓨터 프로그래밍에서 객체 생성, 값 계산, 또는 일부 기타 비용이 많이 드는 과정을 처음 필요한 시점까지 지연시키는 기법이다.

- `useEffect`

  - `useEffect`는 클래스 컴포넌트의 life cycle methods 중 `commit 단계`에 해당하는 `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`를 하나의 API로 통합한 Hook이다.

  - `useEffect`는 **첫 번째 인자**로 콜백 함수(effect)를 받는다. **두 번째 인자**로는 종속성 배열`[]`(deps)을 전달 받는데, 이는 옵션이다.

  - `useEffect`의 콜백 함수(effect)는 렌더링 직후 실행된다.

  - `useEffect`의 콜백 함수는 두 번째 인자로 전달된 배열의 요소에 의존하여 호출된다.

    - 종속성 배열의 요소로는, effect가 참조하고 있는 값(들)이 들어가야 한다.

    - 두 번째 인자로 빈 배열이 전달 되면, 이는 곧 의존하고 있는 대상이 아무 것도 없다는 것이므로 `useEffect`는 마운트(=최초 렌더링) 직후에만 단 한 번 실행되고 그 뒤로는 실행되지 않는다. => 즉, 이 경우 클래스 컴포넌트의 life cycle methods 중 `componentDidMount`와 동일하게 동작

  - 해당 컴포넌트가 제거될 때(unmount 될 때) 실행시키고 싶은 함수가 있으면, `useEffect`의 콜백 함수의 **반환문**에 넣어주면 된다.

- `useContext`

  - `useContext`는 Context 객체의 현재 값을 소비할 수 있도록 설정함.

  - `useContext`는 클래스 컴포넌트의 `static contextType` 또는 `Context.Consumer`과 동일함.

    - 즉, context를 읽고 구독하는 것만 가능함.
