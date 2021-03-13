# 21/03/12 수업 내용
### `setState()`

- 참고 : 공식 문서([링크1](https://ko.reactjs.org/docs/faq-state.html), [링크2](https://ko.reactjs.org/docs/react-component.html#setstate))

- state

  - state란 어떤 컴포넌트가 갖고 있는 상태를 의미함. => local data

  - state는 읽기와 쓰기가 모두 가능함.

- props

  - state가 어떤 컴포넌트가 "직접" 갖는 상태인 반면, props는 그 컴포넌트가 **상위 컴포넌트로부터 전달 받은** 속성을 의미함.

- 클래스 컴포넌트의 `setState()`

  ```js
  setState(updater, [callback])
  // 첫 번째 인자에는 객체 또는 함수를 전달할 수 있음.
  // 두 번째 인자로 전달되는 콜백 함수는 state가 갱신된 이후에 실행됨.
  ```

  > `setState()`는 컴포넌트의 <b>`state` 객체</b>에 대한 업데이트를 실행합니다. `state`가 변경되면, 컴포넌트는 리렌더링됩니다.

    - `state` 객체는 일반 자바스크립트 객체로서, `props`와 마찬가지로 <u>렌더링 결과물에 영향</u>을 주는 정보를 가짐.

  > `setState()`는 컴포넌트를 갱신하는 데에 있어 <b>즉각적인 명령이 아니라 요청</b>이라고 생각하시기 바랍니다.

    - 다시 말하면, 컴포넌트 갱신이 바로 이루어진다는 보장이 없으므로, `setState()`를 호출하자마자 `this.state`에 접근하면 문제가 될 수 있음.

    - 따라서 **갱신 이후**에 어떤 처리를 하고 싶은 경우 ①`componentDidUpdate` 또는 ②`setState`의 두 번째 인자로 전달할 수 있는 콜백 함수를 사용해야 함.

      - 둘 다 **갱신이 적용된 뒤에 실행되는 것이 보장**됨.

  > 이 메서드는 <b>이벤트 핸들러</b>와 <b>서버 응답</b> 등에 따라 UI를 갱신할 때에 가장 많이 사용하는 메서드입니다.

  - `setState()`는 일단 호출이 되면 이전 state와 새로운 state가 동일한 경우에도 리렌더링을 함.

    - 대안① : `shouldComponentUpdate()`가 `false`를 반환하도록 함. (조건부 렌더링)

    - 대안② : ①의 방법을 사용할 수 없을 경우, 새로운 state가 이전 state와 다를 때만 `setState()`를 호출하도록 함.

  - 이전 state 값을 기준으로 새로운 state 값을 설정하려면 어떻게 해야 할까?

    - `setState`의 첫 번째 인자로 객체 대신 콜백 함수를 전달 => 이 콜백 함수는 첫 번째 인자로 `state`를 전달 받고, 두 번째 인자로 `props`를 전달 받음. (이때 전달되는 `state`와 `props`는 최신값임이 보장됨.)

      ```js
      this.setState((state, props) => {
        return {counter: state.counter + props.step};
      });
      ```

(아래부터 이어서)
  - https://ko.reactjs.org/docs/state-and-lifecycle.html

  - https://ko.reactjs.org/docs/faq-state.html

___
### `static getDerivedStateFromProps`

- `static getDerivedStateFromProps`는 상위 컴포넌트로부터 전달받은 `props`와 컴포넌트 자신의 `state`를 조합하여 `state`를 갱신하거나 추가할 수 있음.

  - 리액트 공식 문서는 `static getDerivedStateFromProps` 대신 다른 대안들을 사용할 것을 권장하고 있음. => [(참고1)](https://ko.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#when-to-use-derived-state), [(참고2)](https://ko.reactjs.org/docs/react-component.html#static-getderivedstatefromprops)

- `static getDerivedStateFromProps`는 렌더링될 때마다 매번 실행되는데, **`render` 메서드가 실행되기 직전**에 실행됨.

  ![image](https://user-images.githubusercontent.com/54733637/111025093-77976900-8425-11eb-8f91-78fd226948bd.png)
  
- 클래스 컴포넌트에서만 사용 가능

___
### `shouldComponentUpdate`

- `shouldComponentUpdate`를 사용하면 특정 조건에 부합할 경우 갱신을 중단할 수 있음.

  - `false`를 반환하도록 하여 갱신 중단

- `shouldComponentUpdate` 활용 예

  - 이전 상태의 속성과 다음 상태의 속성이 같을 경우 갱신하지 않도록 설정

  - 상태가 특정 값에 도달하면 더 이상 갱신하지 않도록 설정 (즉, 상태 변경의 범위를 설정할 수 있음.)

    - ex) 카운터 예제

___
### `render`

- `render` 메서드는 어떤 컴포넌트가 존재하는 한, 해당 컴포넌트에서 업데이트가 발생할 때마다 호출됨. ([참고](https://ko.reactjs.org/docs/state-and-lifecycle.html#converting-a-function-to-a-class))

  - 업데이트란 `props`나 `state`가 갱신되는 것을 의미함.

___
### `getSnapshotBeforeUpdate`

- ...

___
### `componentDidUpdate`

- ...

___
### `componentWillUnmount`

- ...

