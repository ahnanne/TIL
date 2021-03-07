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