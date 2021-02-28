# 21/02/28 수업 내용
### props

- `props`

  ![image](https://user-images.githubusercontent.com/54733637/109410972-f7631380-79e1-11eb-90e8-05b6068a7225.png)


  - `props`는 properties의 약어로, 컴포넌트를 사용할 때 특정 값을 전달하고 싶을 경우 사용하는 것

  - 사용 방법

    1. 매개변수로 `props` 쓰기

        ```js
        function Hello(props) {
          console.log(props);

          return <div style={{
            color: props.color
          }}>안녕하세요 {props.name}</div>;
        }
        ```

    2. 디스트럭처링 문법 사용하기

        ```js
        function Hello({ color, name }) {
          console.log(color, name);

          return <div style={{
            color
          }}>안녕하세요 {name}</div>;
        }
        ```

  - `defaultProps`

    ```js
    Hello.defaultProps = {
      name: '이름없음'
    };
    ```

    - 특정 값(위 예제에선 name)을 빠트렸을 때 기본적으로 사용할 값을 지정해놓기 위함.

  - `props.children` ([출처](https://ko.reactjs.org/docs/glossary.html#propschildren))

    - `props.children`은 컴포넌트의 여는 태그와 닫는 태그 사이의 내용을 담음.

      - 클래스로 정의된 컴포넌트에서는 `this.props.children`을 사용함.

    - 예제

      ```js
      <Welcome>Hello world!</Welcome>
      ```

      - `Welcome` 컴포넌트의 `props.children`은 `Hello world!` 문자열임.

      ```js
      function Welcome(props) {
        return <p>{props.children}</p>;
      }
      ```

___
### 조건부 렌더링

- 조건부 렌더링이란 특정 조건이 참인지 거짓인지에 따라 다른 결과를 보여주는 것을 의미함.

