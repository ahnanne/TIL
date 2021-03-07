# 21/03/07 수업 내용
### `useMemo`

- `useMemo` Hook을 사용하면 이전에 연산된 **값**을 재사용할 수 있으며 성능을 최적화할 수 있음.

- `useMemo`는 특정 값이 바뀌었을 때만 특정 함수를 실행하여 연산하도록 처리함.

  - 해당 값에 대한 변화없이 리렌더링되는 경우에는, 이전의 연산 결과를 재사용함.

- `useMemo`는 첫 번째 인수로 콜백함수를 전달 받고, 두 번째 인수로 deps(dependencies)를 전달받음.

  ```js
  const count = useMemo(() => countActiveUsers(users), [users]);
  // deps로 전달한 인수에 따라, users 값의 변화가 있을 때만 콜백함수를 실행함.
  ```

> deps의 요소에는 함수도 포함할 수 있음.

___
### `useCallback` Hook

- `useCallback`을 사용하면 이전에 만들었던 **함수**를 재사용할 수 있음.

- 우리가 만든 실습파일에선 `onChange`, `onCreate`, `onRemove`, `onToggle` 등 함수들이 컴포넌트가 리렌더링 될 때마다 새로 생성되고 있음.

  - 이렇게 함수들이 여러번 새로 생성된다고 해서 부하가 걸리는 건 아니지만, 추후 virtual DOM 관련해서 함수도 재사용하는 구조로 만들어야 함.

- `useCallback`도 `useMemo`와 마찬가지로, 첫 번째 인수로는 콜백 함수를 전달하고 두 번째 인수로는 deps를 전달해줘야 함.

  - 그러면 첫 번째 인수로 전달된 함수는 두 번째 인수(deps)로 전달된 값들(배열의 요소들)이 변경될 때만 새로 생성됨.

  - 우리가 만들었던 함수들을 아래와 같은 형태로 바꾸어줌.

  ```js
  // 변경 전
  const onChange =  e => {
    const { name, value } = e.target;

    setInputs({
      // 새로운 내용 등록되면 덮어씌우기
      ...inputs,
      [name]: value,
      // computed property name(ES6)
    });
  };
  ```

  ```js
  // 변경 후
  const onChange = useCallback(e => {
    const { name, value } = e.target;

    setInputs({
      // 새로운 내용 등록되면 덮어씌우기
      ...inputs,
      [name]: value,
      // computed property name(ES6)
    });
  }, [inputs]);
  ```

___
### React Developer Tools

- 크롬 확장 프로그램인 React Developer Tools 설치하기

  - [바로가기](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi/related?hl=ko)

  - 'Highlight updates when components render.'에 체크

    ![image](https://user-images.githubusercontent.com/54733637/110235526-d23b4b80-7f73-11eb-8079-4ae5e297eb3e.png)
    
    - 그러면 렌더링될 때마다 아래와 같이 실선으로 표시됨.

      ![image](https://user-images.githubusercontent.com/54733637/110235568-162e5080-7f74-11eb-831a-39aae16332ed.png)

___
### `React.memo`

- `React.memo`를 사용하면, 컴포넌트에서 리렌더링이 불필요한 경우 이전에 렌더링했던 결과를 재사용할 수 있으며 컴포넌트의 리렌더링 성능을 최적화할 수 있음.

  - `React.memo`를 사용하면 props가 바뀐 경우에만 리렌더링됨.

- 사용 방법

  ```js
  // CreateUser.js
  
  // 변경 전
  export default CreateUser;
  
  // 변경 후
  export default React.memo(CreateUser);

  // 최적화 끝! 🥞
  ```

___
### `useState`에서의 함수형 업데이트

- `useState`가 관리하는 state에 대해 함수형 업데이트('함수적 갱신')를 하게 되면, deps에 해당 state를 제외시킬 수 있음.

___
### `useReducer`

- `useState` 말고도 `useReducer`라는 Hook을 이용하여 상태를 업데이트할 수도 있음.

- `useState` vs `useReducer`

  - `useState`

    - 설정하고 싶은 다음 상태를 직접 지정해주는 방식으로 상태를 업데이트함.

  - `useReducer`

    - **action**이라는 객체를 기반으로 상태를 업데이트함.

- **action** 객체

  - 업데이트할 때 참조하는 객체로, 업데이트할 때 필요한, 참조하고 싶은 다른 값이 있다면 이 객체 안에 넣어줄 수 있음.

- `useReducer`를 사용하면 상태 업데이트 로직을 해당 컴포넌트 밖으로 분리시킬 수 있음. (아예 다른 파일에 작성하여 불러오는 것도 가능함.)

- 리액트 공식 문서 내용 ([참고](https://ko.reactjs.org/docs/hooks-reference.html#usereducer))

  ```js
  const [state, dispatch] = useReducer(reducer, initialArg, init);
  ```

  - 첫 번째 인수로 전달되는 reducer는 콜백 함수로, `(state, action) => newState`의 형태임.

  - 두 번째 인수로는 state의 초기값으로 설정할 값을 전달할 수 있음. (옵션)

  - *세 번째 인수로는 초기화 지연을 위한 함수를 전달할 수 있음.* (옵션)

    - 참고 : https://ko.reactjs.org/docs/hooks-reference.html#lazy-initialization

  - `dispatch`는 함수 컴포넌트로서, action을 발생시킴.

  - 보통 어떤 때 쓸까?

    > 다수의 하윗값을 포함하는 복잡한 정적 로직을 만드는 경우나 **다음 state가 이전 state에 의존적인 경우**에 보통 `useState`보다 `useReducer`를 선호합니다.
