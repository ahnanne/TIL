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

- 직접 실습해보기 : **Sea 예제**

  ![image](https://user-images.githubusercontent.com/54733637/111294879-20e09800-868e-11eb-99da-f7d4e9a5e4bc.png)

  ```
  [컴포넌트]
  1. Sea - 바다
  2. Boat - 바다를 항해하고 있는 배
  3. Captain - 바다를 항해하고 있는 배의 선장

  [상황]
  Sea 컴포넌트는 weather이라는 상태를 지닌다.
  weather는 "sunny" 또는 "rainstorm" 두 가지 중 하나의 값을 갖는다.
  "날씨 바꾸기!" 버튼을 클릭하면 weather가 "sunny" 또는 "rainstorm"으로 toggle된다.

  Boat 컴포넌트는 Sea 컴포넌트로부터 weather prop을 전달 받는데,
  이 배는 weather이 "sunny"일 땐 사람을 태울 수 있고,
  "rainstorm"일 땐 사람을 태우지 못한다..

  Captain 컴포넌트는 Boat 컴포넌트로부터 또 weather prop을 전달 받는데,
  이 선장은 weather이 "sunny"일 땐 배를 타고 갈 수 있고,
  "rainstorm"일 땐 배를 탈 수 없어 헤엄을 쳐서 가야 한다.
  ```
  
  - 코드

    ```js
    // Sea.js
    import { Component, createContext } from 'react';
    import Boat from '../Boat/Boat';
    import { sea, button, span } from './Sea.module.scss';

    export default class Sea extends Component {
      constructor(props) {
        super(props);
        this.state = {
          weather: "sunny",
          // or "rainstorm"
        };
      }

      changeWeather = () => {
        this.setState((prevState) => ({
          ...prevState,
          weather: this.state.weather === "sunny" ? "rainstorm" : "sunny",
        }));
      };

      render() {
        const { weather } = this.state;

        return (
          <>
            <div className={sea}>
              <Boat weather={weather} />
            </div>
            <button className={button} type="button" onClick={this.changeWeather}>날씨 바꾸기!</button>
            <span className={span}>현재 날씨: {weather}</span>
          </>
        );
      }
    }
    ```
    ```js
    // Boat.js
    import { Component, createContext } from 'react';
    import Captain from '../Captain/Captain';
    import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
    import { faShip } from '@fortawesome/free-solid-svg-icons';
    // import {} from '@fortawesome/free-solid-svg-icons';
    import styles, { boat } from './Boat.module.scss';

    export default class Boat extends Component {
      render() {
        const { weather } = this.props;

        return (
          <div className="boat">
            <FontAwesomeIcon
              className={boat}
              icon={faShip}
              size="6x"
            />
            <div className={styles[`${weather}DayCaptain`]}>
              <Captain weather={weather} />
            </div>
          </div>
        );
      }
    }
    ```
    ```js
    // Captain.js
    import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
    import { faUserNinja, faSwimmer } from '@fortawesome/free-solid-svg-icons';

    export default function Captain({ weather }) {
      if (weather === "sunny") {
        return (
          <FontAwesomeIcon
            icon={faUserNinja}
            size="3x"
          />
        );
      } else {
        return (
          <FontAwesomeIcon
            icon={faSwimmer}
            size="3x"
          />
        );
      }
    }
    ```

  - context를 사용하지 않으면 prop을 위와 같이 일일이 넘겨줘야 해서 번거로울 수 있다. 궁극적으로 prop을 전달받아야 하는 하위 컴포넌트가 깊은 곳에 있을수록 그 과정은 무척 번거로울 것이다.

  - 그럼 이제 위의 예제를 context를 사용하여 바꿔보자.
  
  - 코드

    ```js
    ```

- context를 사용하여 상태 관리의 복잡함을 해결할 수는 있지만, 컴포넌트를 재사용하기가 어려워진다는 단점이 있다. 따라서 보다 더 좋은 방법은 Redux와 같은 **상태 관리 시스템** 라이브러리를 활용하는 것이다.

  - 상태 관리 시스템 : 리액트 애플리케이션의 모든 상태를 하나의 저장소(store)에서 통합적으로 관리하는 시스템

  - 상태 관리 시스템 라이브러리에는 Redux, Mobx, Vuex 등이 있다.

___
### React에서 Font Awesome 아이콘 사용하는 방법

- React에서 Font Awesome의 아이콘들을 컴포넌트로서 바로바로 `import`해서 사용할 수 있다. 어떻게?

  - [🎈여기!](https://fontawesome.com/how-to-use/on-the-web/using-with/react)에서 Font Awesome이 친절히 설명해주고 있다.

- 안내페이지에 나와있듯이, 우선 패키지 매니저인 npm이나 yarn을 통해 @fortawesome 패키지들을 설치한 뒤, 아이콘을 사용하려는 자바스크립트 파일에서 `FontAwesomeIcon`을 `import` 해와서 사용하면 된다. (위 링크로 들어가 보면 단계별로 자세히 안내하고 있으니 참고바람.)

- 아이콘 크기 설정하는 방법 참고 ([링크](https://fontawesome.com/how-to-use/on-the-web/using-with/react#features))

- Font Awesome Pro Plan(유료 아이콘 플랜) 사용자는 Pro package를 추가로 설치해야 한다.

