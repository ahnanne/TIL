# 21/03/22 학습 내용

### Immer(immer.js) 라이브러리

- 리듀서를 작성할 때 immer를 사용하면, 현재 상태에 상대적으로 가할 변경에 대해서만 고려하면 되기 때문에 리듀서를 보다 더 간단히 작성할 수 있음. ([참고](https://medium.com/@wongni/%EC%9D%B4%EB%A8%B8-immer-%EB%A5%BC-%EC%86%8C%EA%B0%9C%ED%95%B4-%EB%B6%88%EB%B3%80%EC%84%B1-%EC%89%BD%EA%B2%8C-%ED%95%98%EC%9E%90-24b00b6ff13f))

  - 즉, immer를 사용하면 불변성을 지키는 코드를 비교적 쉽고 간단하게 작성할 수 있음.

- 리액트는 기본적으로 얕은 비교를 해서 리렌더링을 하므로, 참조 타입(객체, 배열)의 참조값이 바뀌었는지 여부를 판단하지 그 내부의 차이까지는 확인하지 않음. 따라서 리액트에서 코드를 작성할 땐 객체 내부에만 변화를 주는 방식(ex - mutator method)으로는 원하는 결과를 얻을 수 없음.([참고](https://kyounghwan01.github.io/blog/React/immer-js/#immer-js))

  - 하지만 immer를 사용하면, 변경을 줄 부분에 대한 코드만 작성하면 되고 상태 자체의 재할당은 고려하지 않아도 되기 때문에 코드 작성이 편리해짐.

  - 다시 말해, immer를 사용하면 불변성을 해치는 코드를 작성해도 immer가 대신해서 불변성을 유지해줌!

    - redux에서 immer 쓰기 예제 ([링크](https://kyounghwan01.github.io/blog/React/immer-js/#redux%EC%97%90%EC%84%9C-immer-%EC%93%B0%EA%B8%B0))

- 사용 방법 ([참고](https://medium.com/@wongni/%EC%9D%B4%EB%A8%B8-immer-%EB%A5%BC-%EC%86%8C%EA%B0%9C%ED%95%B4-%EB%B6%88%EB%B3%80%EC%84%B1-%EC%89%BD%EA%B2%8C-%ED%95%98%EC%9E%90-24b00b6ff13f))

  ```js
  import produce from "immer";

  const nextState = produce(currentState, draft => {
    // currentState에 대해 가할 변경
    // 주의할 점! 이 안에서는 currentState가 아니라
    // draft를 참조해야 함.
  });
  ```

    - produce 함수는 <b>첫 번째 인자</b>로는 수정하려는 상태(현재 상태), <b>두 번째 인자</b>로는 producer 함수(현재 상태를 변경하는 함수)를 전달함.

      - producer 함수는 인자로 <b>draft</b>를 전달 받는데, 이는 "현재 상태의 proxy"임.

      - producer 함수는 <u>아무것도 반환하지 않음</u>.

      - draft에 가해지는 수정은 다음 상태(위 코드에서 `nextState`)를 만들어 내는 데 사용됨. 만약 producer 함수가 아무것도 수정하지 않으면 `nextState`와 `currentState`는 동일함. 즉, 참조값이 같음.

___
### 엘리먼트 렌더링

- JSX나 `React.createElement`는 **리액트 엘리먼트**를 생성함.

  - Babel은 JSX를 `React.createElement` 호출로 컴파일 함. ([참고](https://ko.reactjs.org/docs/introducing-jsx.html#jsx-represents-objects))

- 엘리먼트는 일반 객체이며, 리액트 앱의 가장 작은 단위임. ([참고](https://ko.reactjs.org/docs/rendering-elements.html))

- 리액트 DOM은 리액트 엘리먼트와 일치하도록 DOM을 업데이트함.

- DOM에 엘리먼트 렌더링하기([참고](https://ko.reactjs.org/docs/rendering-elements.html#rendering-an-element-into-the-dom))

  - **루트(root) DOM 노드**

    ```js
    <div id="root"></div>

    // 이 안에 들어가는 모든 엘리먼트를 React DOM에서 관리하기 때문에 이것을 “루트(root)” DOM 노드라고 부릅니다.
    ```

  > React로 구현된 애플리케이션은 일반적으로 하나의 루트 DOM 노드가 있습니다.

  - 루트 DOM 노드에 엘리먼트를 렌더링하려면, `ReactDOM.render()`의 **첫 번째 인자**로 엘리먼트를, **두 번째 인자**로 루트 DOM 노드를 전달하면 됨.

    ```js
    const element = <h1>Hello, world</h1>;
    
    ReactDOM.render(element, document.getElementById('root'));
    ```

