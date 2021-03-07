# 21/03/07 수업 내용
### `useMemo`

- `useMemo` Hook을 사용하면 이전에 연산된 값을 재사용할 수 있으며 성능을 최적화할 수 있음.

- `useMemo`는 특정 값이 바뀌었을 때만 특정 함수를 실행하여 연산하도록 처리함.

  - 해당 값에 대한 변화없이 리렌더링되는 경우에는, 이전의 연산 결과를 재사용함.

- `useMemo`는 첫 번째 인수로 콜백함수를 전달 받고, 두 번째 인수로 deps를 전달받음.

  ```js
  const count = useMemo(() => countActiveUsers(users), [users]);
  // deps로 전달한 인수에 따라, users 값의 변화가 있을 때만 콜백함수를 실행함.
  ```

___
### `useCallback` Hook

- 