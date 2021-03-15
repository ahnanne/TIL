# 21/03/15 학습 내용
### `forceUpdate()`

- 이하의 내용들은 공식 문서를 참고했음. ([링크](https://ko.reactjs.org/docs/react-component.html#forceupdate))

- 원래는 어떤 컴포넌트의 state나 props가 변경되면 해당 컴포넌트가 리렌더링되는 것이 기본 동작임. 하지만 그 컴포넌트의 **`render()` 메서드가 state나 props가 아닌 다른 데이터값에 의존하는 경우**, `forceUpdate()`를 호출하여 `render()`가 호출되어 리렌더링 되도록 할 수 있음.

- `forceUpdate()`를 호출하면 [`shouldComponentUpdate()`](https://github.com/ahnanne/TIL/tree/main/react/210312#shouldcomponentupdate)는 건너뛰고 `render()`를 호출함.

___
### 클래스 컴포넌트와 context

- 이하의 내용들은 공식 문서를 참고했음. ([링크](https://ko.reactjs.org/docs/context.html))
