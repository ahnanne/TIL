# 21/03/15 학습 내용
### `forceUpdate()`

- 이하의 내용들은 공식 문서를 참고했음. ([링크](https://ko.reactjs.org/docs/react-component.html#forceupdate))

- 원래는 어떤 컴포넌트의 state나 props가 변경되면 해당 컴포넌트가 리렌더링되는 것이 기본 동작임. 하지만 그 컴포넌트의 **`render()` 메서드가 state나 props가 아닌 다른 데이터값에 의존하는 경우**, `forceUpdate()`를 호출하여 `render()`가 호출되어 리렌더링 되도록 할 수 있음.

- `forceUpdate()`를 호출하면 [`shouldComponentUpdate()`](https://github.com/ahnanne/TIL/tree/main/react/210312#shouldcomponentupdate)는 건너뛰고 `render()`를 호출함.

___
### 클래스 컴포넌트와 context

- 이하의 내용들은 공식 문서를 참고했음. ([링크](https://ko.reactjs.org/docs/context.html))

> context를 이용하면 단계마다 일일이 props를 넘겨주지 않고도 컴포넌트 트리 전체에 데이터를 제공할 수 있습니다.
> context를 사용하면 중간에 있는 엘리먼트들에게 props를 넘겨주지 않아도 됩니다.

___
### React에서 Font Awesome 아이콘 사용하는 방법

- React에서 Font Awesome의 아이콘들을 컴포넌트로서 바로바로 `import`해서 사용할 수 있다. 어떻게?

  - [🎈여기!](https://fontawesome.com/how-to-use/on-the-web/using-with/react)에서 Font Awesome이 친절히 설명해주고 있다.

- 안내페이지에 나와있듯이, 우선 패키지 매니저인 npm이나 yarn을 통해 @fortawesome 패키지들을 설치한 뒤, 아이콘을 사용하려는 자바스크립트 파일에서 `FontAwesomeIcon`을 `import` 해와서 사용하면 된다. (위 링크로 들어가 보면 단계별로 자세히 안내하고 있으니 참고바람.)

- 아이콘 크기 설정하는 방법 참고 ([링크](https://fontawesome.com/how-to-use/on-the-web/using-with/react#features))

- Font Awesome Pro Plan(유료 아이콘 플랜) 사용자는 Pro package를 추가로 설치해야 한다.

