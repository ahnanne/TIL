# 21/03/08 수업 내용
### Context API를 사용한 전역 값 관리

- context ([참고](https://ko.reactjs.org/docs/context.html))

  > context는 React 컴포넌트 트리 안에서 <b>전역적(global)</b>이라고 볼 수 있는 데이터를 공유할 수 있도록 고안된 방법입니다.
 
  > context의 주된 용도는 다양한 레벨에 네스팅된 많은 컴포넌트에게 데이터를 전달하는 것입니다. <b>context를 사용하면 컴포넌트를 재사용하기가 어려워지므로</b> <u>꼭 필요할 때만</u> 쓰세요.

    - context를 사용하면 편리한 경우 : 선호 로케일, 테마, 데이터 캐시 등을 관리하는 경우

    - 대안 : 컴포넌트 합성 ([참고1](https://ko.reactjs.org/docs/composition-vs-inheritance.html), [참고2](https://ko.reactjs.org/docs/context.html#before-you-use-context))

  - context를 이용하면 컴포넌트 전체가 데이터를 공유받도록 할 수 있음. => 즉, 일일이 props를 넘겨주지 않아도 됨.

    > context를 사용하면 중간에 있는 엘리먼트들에게 props를 넘겨주지 않아도 됩니다.

- Context API를 사용하면 여러 컴포넌트 간 props를 전달하고 또 전달하는 과정(아래 그림에서 노란색 화살표)을 간단하게(아래 그림에서 보라색 화살표) 할 수 있음.

  ![image](https://user-images.githubusercontent.com/54733637/110290759-7da8d680-802e-11eb-9c79-62f76cb76183.png)

  - `React.createContext`

    ```js
    const MyContext = React.createContext(defaultValue);
    ```

    - `React.createContext`는 Context 객체를 만들어냄.

      > <i>Context 객체를 구독하고 있는 컴포넌트</i>를 렌더링할 때 React는 트리 상위에서 가장 가까이 있는 짝이 맞는 `Provider`로부터 현재값을 읽습니다.
      > `defaultValue` 매개변수는 트리 안에서 적절한 `Provider`를 찾지 못했을 때만 쓰이는 값입니다.

  - `Context.Provider`

    ```js
    <MyContext.Provider value={/* 어떤 값 */}>
    ```
    
    - `Provider`는 Context 객체에 포함된 컴포넌트로서, context를 구독하는 컴포넌트들에게 **context의 변화를 알리는 역할**을 함.

      > `Provider` 컴포넌트는 `value` prop을 받아서 이 값을 하위에 있는 컴포넌트에게 전달합니다. 값을 전달받을 수 있는 컴포넌트의 수에 제한은 없습니다. `Provider` 하위에 또 다른 `Provider`를 배치하는 것도 가능하며, 이 경우 하위 `Provider`의 값이 우선시됩니다.
      > `Provider` 하위에서 context를 구독하는 모든 컴포넌트는 `Provider`의 `value` prop가 바뀔 때마다 다시 렌더링 됩니다.
    
    - context 값이 바뀌었는지 여부는 `Object.is`([참고](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/is#%EC%84%A4%EB%AA%85))와 동일한 알고리즘을 사용하여 이전 값과 새로운 값을 비교해서 측정하기 때문에, 만약 `value` 값으로 객체를 전달하는 경우에는 문제가 생길 수 있음. ([참고](https://ko.reactjs.org/docs/context.html#caveats))

  - `Class.contextType` (?)

    > `React.createContext()`로 생성한 Context 객체를 원하는 클래스의 `contextType` 프로퍼티로 지정할 수 있습니다. 이 프로퍼티를 활용해 클래스 안에서 `this.context`를 이용해 해당 Context의 가장 가까운 `Provider`를 찾아 그 값을 읽을 수 있게 됩니다.
    
    - 예제 코드

      ```js
      class MyClass extends React.Component {
        componentDidMount() {
          let value = this.context;
          /* MyContext의 값을 이용한 코드 */
        }
        componentDidUpdate() {
          let value = this.context;
          /* ... */
        }
        componentWillUnmount() {
          let value = this.context;
          /* ... */
        }
        render() {
          let value = this.context;
          /* ... */
        }
      }
      MyClass.contextType = MyContext;
      ```
      
    > 이 API를 사용하면 하나의 context만 구독할 수 있습니다. 여러 context를 구독하기 위해서는 [여러 context 구독하기](https://ko.reactjs.org/docs/context.html#consuming-multiple-contexts)를 참조하세요.

  - `Context.Consumer`

    ```js
    <MyContext.Consumer>
      {value => /* context 값을 이용한 렌더링 */}
    </MyContext.Consumer>
    ```

    > `Context.Consumer`의 자식(=하위 요소)은 <b>함수</b>여야합니다. 이 함수는 <u>context의 현재값</u>(=위 코드에서 `value`)을 받고 React 노드를 반환(=render)합니다.
    
    > 이 함수가 받는 `value` 매개변수 값은 해당 context의 `Provider` 중 상위 트리에서 가장 가까운 `Provider`의 `value` prop과 동일합니다. 상위에 `Provider`가 없다면, `value` 매개변수 값은 `createContext()`에 보냈던 `defaultValue`와 동일할 것입니다.

    - `Context.Consumer`는 context 변화를 구독하는 React **컴포넌트**로서, 함수 컴포넌트 안에서 context를 구독할 때 사용함.

  - `Context.displayName`

    - `displayName`은 Context 객체의 문자열 프로퍼티인데, 해당 Context 객체가 React DevTools에 어떤 이름으로 보여질지를 설정함. ([참고](https://blog.logrocket.com/react-reference-guide-context-api/#contextdisplayname))

    - 예제

      ```js
      import { createContext } from 'react';

      const MyContext = createContext('defaulttt');
      MyContext.displayName = 'AESPA';

      return (
        <>
        <MyContext.Consumer>
          {value => <div>{value}</div>}
        </MyContext.Consumer>
        </>
      )
      ```

      - 출력 결과

        ![image](https://user-images.githubusercontent.com/54733637/110485820-61409300-812f-11eb-901a-f40c16655d1c.png)
