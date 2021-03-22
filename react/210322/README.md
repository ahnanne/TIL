# 21/03/22 학습 내용
### 불변 객체

- 정리 예정..(https://yamoo9.gitbook.io/learning-react-app/learning-history/props-vs-state#immutable-and-set-state, https://ko.wikipedia.org/wiki/%EB%B6%88%EB%B3%80%EA%B0%9D%EC%B2%B4)

___
### Immer

- 정리 예정..(https://medium.com/@wongni/%EC%9D%B4%EB%A8%B8-immer-%EB%A5%BC-%EC%86%8C%EA%B0%9C%ED%95%B4-%EB%B6%88%EB%B3%80%EC%84%B1-%EC%89%BD%EA%B2%8C-%ED%95%98%EC%9E%90-24b00b6ff13f)

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

___
### 컴포넌트

- 정리 예정..(https://ko.reactjs.org/docs/components-and-props.html)
