# 21/02/28 수업 내용
### props

- `props`

  ![image](https://user-images.githubusercontent.com/54733637/109410972-f7631380-79e1-11eb-90e8-05b6068a7225.png)


  - `props`는 properties의 약어로, 컴포넌트를 사용할 때 특정 값을 전달하고 싶을 경우 사용하는 것

    > React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면, <b>JSX <u>어트리뷰트</u>와 <u>자식</u>을 해당 컴포넌트에 단일 객체로 전달</b>합니다. 이 객체를 “`props`”라고 합니다. ([참고](https://ko.reactjs.org/docs/components-and-props.html#gatsby-focus-wrapper))

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

- 삼항 조건 연산자 또는 `&&` 사용

- JSX에서 `null`, `false`, `undefined`를 렌더링하게 되면 아무것도 안 나타나게 됨.

  - cf.) `0`은 그대로 출력됨.

- 어떤 `props`에 값을 안 주면 `true`로 지정한 것과 동일함.

  ```
  <Hello color="red" name="react" isSpecial={true} />
  // same as
  <Hello color="red" name="react" isSpecial />
  ```

___
### useState를 통한 동적 상태 관리

- 컴포넌트에서 이벤트 설정하기([참고](https://ko.reactjs.org/docs/handling-events.html))

  ```jsx
  function Counter() {
    const [number, setNumber] = useState(0);
  // 배열 디스트럭처링 할당
  // 💜 number: 상태
  // 💜 setNumber: number라는 상태를 변경하는 함수

    const btnStyle = {
      backgroundColor: '#59989b',
      border: 'none',
      borderRadius: 5,
      width: 38,
      height: 30,
      margin: 10
    };

    const onIncrease = () => {
    setNumber(number + 1);
    // 또는
    // 💛setNumber(prevNumber => prevNumber + 1);
  };

  const onDecrease = () => {
    setNumber(number - 1);
    // 또는
    // 💛setNumber(prevNumber => prevNumber - 1);
  };
  // 💛: "함수형 업데이트" - 성능 최적화 관련

    return (
      <div>
        <h1>0</h1>
        <button style={btnStyle} onClick={onIncrease}>+1</button>
        <button style={btnStyle} onClick={onDecrease}>-1</button>
      </div>
    )
  }
  ```

  - 위 예제에서 알 수 있듯이, 리액트에서는 이벤트를 소문자가 아니라 camel case로 작성함.

  - 문자열이 아니라 함수로 이벤트 핸들러를 전달하는데, 이때 주의해야 할 점은 함수를 <b>호출하면 안 된다</b>는 점!

    - 전달할 때 함수를 호출해버리면 렌더링할 때 함수가 실행되어버림.

___
### input 상태 관리

- 예제

  ```js
  function InputSample() {
    const [text, setText] = useState('');

    const onChange = e => {
      setText(e.target.value);
    };

    const onReset = () => {
      setText('');
    };

    return (
      <div>
        <input onChange={onChange} value={text} />
        <button onClick={onReset}>초기화</button>
        <div>
          <b>값: </b>
          {text}
        </div>
      </div>
    )
  }
  ```

- input이 여러 개일 때의 상태 관리

  ```js
  function InputSample() {
    const [inputs, setInputs] = useState({
      name: '',
      nickname: '',
    });

    const { name, nickname } = inputs;

    const onChange = e => {
      // console.log(e.target.name + ': ' + e.target.value);
      const { name, value } = e.target;
      console.log(name + ': ' + value);

      const nextInputs = {
        ...inputs,
        // 스프레드 문법
        [name]: value
        // [name]은 name이 될 수도 있고 nickname이 될 수도 있음.
      };
      console.log(nextInputs);

      setInputs(nextInputs);
    };

    const onReset = () => {
      setInputs({
        name: '',
        nickname: ''
      });
    };

    return (
      <div>
        <input
          name="name"
          {/* input 요소의 name 어트리뷰트는 name/value pair(쌍)의 일부! */}
          placeholder="이름"
          onChange={onChange}
          value={name}
        />
        <input
          name="nickname"
          placeholder="닉네임"
          onChange={onChange}
          value={nickname}
        />
        <button onClick={onReset}>초기화</button>
        <div>
          <b>값: </b>
          {name} ({nickname})
        </div>
      </div>
    );
  }
  ```

  - 리액트에서 객체를 업데이트할 때는 우선 <u>기존의 객체를 복사</u>해야 함.

  - 그리고 그 위에 새로운 값을 덮어씌우고 새로운 상태로 설정을 해줘야 함. => <b>"불변성을 지킨다!"</b>

    - 불변성을 지켜야 컴포넌트 업데이트 성능을 최적화할 수 있음.
