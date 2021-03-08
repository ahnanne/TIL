# 21/03/08 수업 내용
### `Context API`를 사용한 전역 값 관리

- `Context API`를 사용하면 여러 컴포넌트 간 props를 전달하고 또 전달하는 과정(아래 그림에서 노란색 화살표)을 간단하게(아래 그림에서 보라색 화살표) 할 수 있음.

  ![image](https://user-images.githubusercontent.com/54733637/110290759-7da8d680-802e-11eb-9c79-62f76cb76183.png)

- `React.createContext`

  ```js
  const MyContext = React.createContext(defaultValue);
  ```

  - `React.createContext`는 Context 객체를 만들어냄.

  (https://ko.reactjs.org/docs/context.html#reactcreatecontext 부터 계속..)
  (https://ko.reactjs.org/docs/hooks-reference.html#usecontext 부터 계속..)

___
### `useCallback` Hook

- 
