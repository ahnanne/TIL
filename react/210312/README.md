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

___
### `constructor`

```js
constructor(props)
```

- 이하의 내용들은 공식 문서를 참고했음. ([링크](https://ko.reactjs.org/docs/react-component.html#constructor))

> <b>메서드를 바인딩하거나 state를 초기화하는 작업이 없다면, 해당 React 컴포넌트에는 생성자(constructor)를 구현하지 않아도 됩니다.</b>

- 어떤 컴포넌트의 `constructor`는 해당 컴포넌트가 마운트되기 전에 호출됨.

- `constructor`를 구현할 때, 다른 구문에 앞서 제일 먼저 `super(props);`부터 호출해야 함.

  - `constructor` 내에 `this.props`를 정의하기 위함.

- `constructor` 사용 목적

  1. `this.state`에 객체를 할당하여 지역 상태를 초기화하기 위함.

  2. 인스턴스에 이벤트 처리 메서드를 바인딩하기 위함.

- 다른 메서드 내에서는 `this.state`를 직접 할당할 수 없고 `this.setState()`를 사용해야 하지만, `constructor` 내에서만큼은 `this.state`를 직접 할당할 수 있음. => 초기 상태

  - 단, `constructor` 내에서는 `setState()`를 호출하면 안됨.

- 주의할 점

  - `constructor` 내에서는 `setState()`를 호출하면 안됨.

  - `constructor` 내에서는 부수 효과를 발생시키거나 <i>구독 작업(subscription)</i>을 수행하면 안됨.

    - 해당 작업들이 필요한 경우 `componentDidMount`에서 처리할 것

  - state에 props를 복사하면 안 됨.

    ```js
    // Bad
    constructor(props) {
      super(props);
      // 이렇게 하지 마세요!
      this.state = { color: props.color };
    }
    ```

    - **props의 갱신을 의도적으로 무시해야 할 때만** 저렇게 할 것

___
### `static getDerivedStateFromProps`

```js
static getDerivedStateFromProps(props, state)
```

- `static getDerivedStateFromProps`는 첫 번째 인자로 `props`를 전달 받고, 두 번째 인자로 `state`를 전달 받음.

  ![image](https://user-images.githubusercontent.com/54733637/111113348-fb2b9400-85a4-11eb-96a2-a02ae2884204.png)

- `static getDerivedStateFromProps`는 상위 컴포넌트로부터 전달받은 `props`와 컴포넌트 자신의 `state`를 조합하여 `state`를 갱신하거나 추가할 수 있음.

  - 리액트 공식 문서는 `static getDerivedStateFromProps` 대신 다른 대안들을 사용할 것을 권장하고 있음. => [(참고1)](https://ko.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#when-to-use-derived-state), [(참고2)](https://ko.reactjs.org/docs/react-component.html#static-getderivedstatefromprops)

- `static getDerivedStateFromProps`는 렌더링될 때마다 매번 실행되는데, **`render` 메서드가 실행되기 직전에** 실행됨.

  ![image](https://user-images.githubusercontent.com/54733637/111025093-77976900-8425-11eb-8f91-78fd226948bd.png)

___
### `shouldComponentUpdate`

- `shouldComponentUpdate`를 사용하면 특정 조건에 부합할 경우 갱신을 중단할 수 있음.

  - `false`를 반환하도록 하여 갱신 중단

  - `false`를 반환할 경우, `render`와 `componentDidUpdate`가 호출되지 않음.

- 사용 목적 : **성능 최적화** ([참고](https://ko.reactjs.org/docs/react-component.html#shouldcomponentupdate))

  - 즉, 렌더링이 <u>불필요한 경우</u>에는 렌더링을 하지 않음으로써 성능을 최적화할 수 있지만, 그런 경우가 아니라면 버그로 이어질 수도 있음.

- `shouldComponentUpdate` 활용 예

  - 이전 상태의 속성과 다음 상태의 속성이 같을 경우 갱신하지 않도록 설정

  - 상태가 특정 값에 도달하면 더 이상 갱신하지 않도록 설정 (즉, 상태 변경의 범위를 설정할 수 있음.)

    - ex) 카운터 예제

___
### `render`

- 이하의 내용들은 공식 문서를 참고했음. ([링크](https://ko.reactjs.org/docs/react-component.html#render))

- **클래스 컴포넌트**를 구현할 때, 다른 생명 주기 메서드들은 필수가 아니지만 **`render` 메서드는 필수**로 구현되어야 함.

- `render` 메서드는 아래의 것들 중 하나를 반환해야 함.

  1. **React 엘리먼트**

      - 보통 JSX를 사용하여 생성함.

  2. **배열, Fragment**

      - 배열을 사용하면 여러 개의 엘리먼트가 반환됨.

  3. **Portal** ([참고](https://ko.reactjs.org/docs/portals.html))

      - *별도의 DOM 하위 트리에 자식 엘리먼트를 렌더링함.*

  4. **문자열, 숫자**

      - DOM 상에 **텍스트 노드**로서 렌더링됨.

  5. **Boolean, `null`**

      - render nothing

- `render` 메서드는 **순수**해야 함.

  - "순수하다" ?

    - 컴포넌트의 state를 변경하지 않는다.

    - 호출될 때마다 동일한 결과를 반환해야 한다.

    - *브러우저와 직접적으로 상호작용을 하지 않는다.* => cf.) 브라우저와 상호작용하는 작업은 `componentDidMount` 등에서 수행할 것

- `render` 메서드는 어떤 컴포넌트가 존재하는 한, 해당 컴포넌트에서 업데이트가 발생할 때마다 호출됨. ([참고](https://ko.reactjs.org/docs/state-and-lifecycle.html#converting-a-function-to-a-class))

  - 업데이트란 `props`나 `state`가 갱신되는 것을 의미함.

  - 하지만 `shouldComponentUpdate`가 `false`를 반환하는 경우에는 `render`가 호출되지 않음.

___
### `getSnapshotBeforeUpdate`

> `getSnapshotBeforeUpdate()`는 <b>가장 마지막으로 렌더링된 결과</b>가 DOM 등에 반영되었을 때에 호출됩니다. 이 메서드를 사용하면 컴포넌트가 DOM으로부터 스크롤 위치 등과 같은 정보를 이후 변경되기 전에 얻을 수 있습니다. <b>이 생명주기가 반환하는 값은 `componentDidUpdate()`에 인자로 전달</b>됩니다. ([참고](https://ko.reactjs.org/docs/react-component.html#getsnapshotbeforeupdate))

- 활용 예 : 채팅 화면 - 스크롤 위치를 처리하는 작업이 필요한 UI

- `getSnapshotBeforeUpdate`는 ①스냅샷 값 또는 ②`null`을 반환함.

  - 스냅샷 값이란, `getSnapshotBeforeUpdate`가 반환한 값을 의미함.

___
### `componentDidUpdate`

- `componentDidUpdate`는 **갱신이 일어난 직후에** 호출됨.

  - **최초 렌더링에서는 호출되지 않음!**

> 컴포넌트가 갱신되었을 때 <b>DOM을 조작</b>하기 위하여 이 메서드를 활용하면 좋습니다. 또한, <b>이전과 현재의 props를 비교하여 네트워크 요청을 보내는 작업</b>도 이 메서드에서 이루어지면 됩니다. (가령, props가 변하지 않았다면 네트워크 요청을 보낼 필요가 없습니다.) ([참고](https://ko.reactjs.org/docs/react-component.html#componentdidupdate))

- `componentDidUpdate`에 인자로 전달되는 것들

  ```js
  componentDidUpdate(prevProps, prevState, snapshot) {
    // 이때 세 번째 인자로 전달되는 snapshot은
    // getSnapshotBeforeUpdate가 반환한 값임.
    // (getSnapshotBeforeUpdate의 반환값이 없을 경우에는 undefined)
  }
  ```
  
- 활용 예 ([출처](https://ko.reactjs.org/docs/react-component.html#componentdidupdate))

  ```js
  componentDidUpdate(prevProps) {
    // 전형적인 사용 사례 (props 비교를 잊지 마세요)
    if (this.props.userID !== prevProps.userID) {
      this.fetchData(this.props.userID);
    }
  }
  ```
  
- 주의할 점

  - `shouldComponentUpdate`가 `false`를 반환할 경우, `componentDidUpdate`는 호출되지 않음.

  - 조건문으로 감싸지 않으면 무한 반복이 발생할 수 있음.

  - 추가적인 렌더링을 유발할 수 있음.

  - prop을 state에 저장 및 복사하는 것은 버그를 유발할 수 있으므로, 전달 받은 prop을 직접 사용하는 것이 좋음. ([참고](https://ko.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html))

___
### `componentWillUnmount`

- `componentWillUnmount`는 컴포넌트가 **제거되기 직전에** 호출됨. ([참고](https://ko.reactjs.org/docs/react-component.html#componentwillunmount))

- 활용 예

  > 이 메서드 내에서 타이머 제거, 네트워크 요청 취소, `componentDidMount()` 내에서 생성된 구독 해제 등 필요한 모든 정리 작업을 수행하세요.

___
### 리렌더링될 때 메서드 호출 순서

1. `static getDerivedStateFromProps`

2. `shouldComponentUpdate`

3. `render`

4. `getSnapshotBeforeUpdate`

5. `componentDidUpdate`
