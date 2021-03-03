# 21/03/03 수업 내용
### useRef로 컴포넌트 안의 변수 만들기

- 컴포넌트 내부에서 let 키워드로 변수를 선언한다고 가정해보자. 리렌더링될 때 그 변수값은 초기화된다.

- 만약 계속 유지하고 싶은 어떤 값을 관리하려면 `useState`를 사용해야 하는데, `useState`는 상태를 바꾸면 컴포넌트가 리렌더링 됨. 굳이 리렌더링할 필요가 없는 경우에도!

  - 그래서 `useState` 대신 `useRef`를 사용한다.

- `ref`를 사용해야 할 때 이 `useRef`라는 hook을 사용한다고 했는데, `useRef`는 이 외에도 컴포넌트가 리렌더링될 때마다 "계속 기억해야 하는 값"을 관리할 때도 사용할 수 있다.

  - "계속 기억해야 하는 값"에는 ① `setTimeout`, `setInterval`의 timer id, ② 외부 라이브러리를 사용하여 생성된 인스턴스, ③ Scroll 위치 등등 다양한 값이 있을 것이다.

- `useRef`로 관리하는 값은, **값이 바뀌어도 컴포넌트가 리렌더링이 되지 않는다**!

  ```js
  const nextId = useRef(4);

  const onCreate = () => {
    console.log(nextId.current);
    // 초기값 조회 → useRef로 준 초기값 조회하고 싶으면 위와 같이 해당 변수의 current 값을 조회하면 됨.

    // 새로운 항목 만들때마다 새로운 아이디값 만들기
    nextId.current += 1;
    // nextId 값이 바뀐다고 해서 컴포넌트가 리렌더링 되지는 않음.
    // nextId는 useRef로 관리하기 때문!
  };
  ```

  > `useRef` returns a mutable ref object whose `.current` property is initialized to the passed argument (`initialValue`). The returned object will persist for the full lifetime of the component.

  > Note that `useRef()` is useful for more than the `ref` attribute. It’s handy for keeping any mutable value around similar to how you’d use instance fields in classes.

___
### 배열에 항목 추가하기

- 