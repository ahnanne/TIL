# 21/03/17 학습 내용
### 클래스 컴포넌트의 `this` 바인딩

- <u>클래스 필드 정의 제안을 사용하여 클래스 필드에 화살표 함수를 할당하는 방식</u>은 기존의 `this` 바인딩을 위해 필요했던 추가적인 절차(`bind(this)` 사용)를 거치지 않아도 `this` 바인딩 문제를 해결할 수 있도록 해준다는 점에서 편리함.

  > 클래스 필드는 기본적으로 public함. (cf. private 필드 제안)

- <b>클래스 필드(class field, field, member)</b>는 "클래스가 생성할 **인스턴스의 프로퍼티**"를 가리킴.

- 클래스 안에서 `this`는 `constructor` 및 메서드들 내부에서만 유효하므로, 클래스 필드를 정의할 때는 `this`에 클래스 필드를 바인딩할 수 없음. (아래 그림 참고)

  ![image](https://user-images.githubusercontent.com/54733637/111654857-7a8ec100-884c-11eb-8368-2d864a721108.png)

- 함수도 객체니까 클래스 필드에 할당할 수 있는데, 이렇게 정의된 메서드는 **인스턴스 메서드**가 됨.

  - 왜냐하면 클래스 필드란 "클래스가 생성할 **인스턴스의 프로퍼티**"를 의미하니까!

  - 따라서 클래스 필드에 함수를 할당하여 메서드를 만드는 방식은 권장되지 않음.

    - **인스턴스 메서드**는 인스턴스가 생성될 때마다 **중복 생성**되는바, 메모리 측면에서 좋지 않기 때문임.

- 클래스 필드에 할당한 화살표 함수는 인스턴스 메서드(인스턴스 프로퍼티)이며, 결국 `constructor` 내부에서 만들어지는 인스턴스 프로퍼티와 같다고 볼 수 있음.

  - 그리고 화살표 함수는 자체의 `this` 바인딩을 갖지 않고 상위 스코프의 `this` 바인딩을 따르는데, 여기서 화살표 함수의 상위 스코프는 `constructor`가 되고 **`constructor` 내부의 `this` 바인딩은 클래스가 생성한 인스턴스를 가리키므로**, 결론은 다음과 같다.

  > 클래스 필드에 할당한 화살표 함수 내부의 `this` 또한 클래스가 생성할 인스턴스를 가리킨다. (이웅모, 모던 자바스크립트 Deep Dive(2020), p.485)

- `console.log`

  - 인스턴스 메서드 내부의 `this`가 가리키는 값을 확인해보려고 아래와 같이 클래스 필드에서 화살표 함수로 메서드(인스턴스 메서드)를 정의하고 콘솔창을 확인해보았다.

    - 코드

      ```js
      // this binding 확인용
      checkThisOut = function () {
        console.log(this);
      };

      checkThisOutToo = () => {
        console.log(this);
      };
      ```
      
    - 콘솔 출력 결과

      ![image](https://user-images.githubusercontent.com/54733637/111707615-be52ec00-8887-11eb-9f04-3829cbe44f54.png)
      
      - 밑에 하나씩 딸려서 출력되는 `undefined`는 무엇인가 했는데, 알고보니 위 check 함수들에서 `return`문이 없어서 `undefined`가 반환되는 것이었다.

  - 참고

    - 명시적으로 값을 `return`하지 않는 함수를 콘솔로 찍어보면, 아래와 같이 `undefined`가 두 번 나온다.

      ![image](https://user-images.githubusercontent.com/54733637/111707920-46d18c80-8888-11eb-9e54-485a5e8bd59e.png)
      
    - `undefined` 중 하나는 함수가 명시적으로 값을 반환하지 않아 암묵적으로 반환되는 `undefined`이며, 두 번째는 완료값(completion value)으로서의 `undefined`다.

      - 완료값(completion value) : 크롬 개발자 도구에서 표현식이 아닌 문을 실행할 때 출력되는 값 (이웅모, 모던 자바스크립트 Deep Dive(2020), p.58)


___
### Form 컨트롤

- controlled component와 uncontrolled component ([참고](https://ko.reactjs.org/docs/forms.html#controlled-components))

  - controlled component : React가 제어할 수 있는 컴포넌트

    - HTML에서는 `input`, `textarea`, `select`와 같은 폼 요소는 일반적으로 사용자의 입력을 기반으로 자신의 state를 관리하고 업데이트하지만, **React에서는 이러한 폼 요소의 state가 일반적으로 컴포넌트의 state 속성에 유지되며 `setState()`에 의해 업데이트**됨.

    - 폼을 렌더링하는 React 컴포넌트는 폼에 발생하는 사용자 입력값을 제어함. => 이렇게 제외되는 폼 요소를 <b>controlled component(제어 컴포넌트)</b>라고 함.

    - controll component에서는 이벤트 리스너가 state의 업데이트를 처리하거나 유효성 검사를 수행하기도 함.

  - uncontrolled component :  React가 제어할 수 없는 컴포넌트

    - "React가 제어할 수 없다" => 사용자가 데이터를 입력하면 React에서 별도 처리 없이 요소에 바로 반영되며, 특정 필드가 특정 속성을 갖도록 강제할 수 없음.

    - uncontrolled comp의 경우 DOM 자체에서 데이터를 다루게 되는데, <u>`ref` 속성</u>을 사용하여 DOM에서 폼 값을 가져올 수 있음.

- 폼 요소

  1. `textarea` 요소

  2. `select` 요소

  3. `file input` 요소

- React 폼 멀티플 컨트롤 핸들링

  - 하나의 이벤트 핸들러로 여러 개의 `input`을 관리할 수 있음.

  - 각각의 `input`에 `name` 속성을 주고, `e.target`으로부터 `name`과 `value`를 디스트럭처링 할당으로 끄집어내서 사용

    ```js
    /** React form multiple control handle */
    controlInput = e => {
      const { name, value } = e.target;

      this.setState((prevState) => ({
        ...prevState,
        [name]: value,
      }));
    };
    ```

- 다중 선택 컨트롤(`select`, `option`)

  - HTML과 달리 React에서는 `select` 요소의 초기 값을 설정할 때 `value` 속성을 사용하여 설정함.

  - HTML에서 다중 선택을 사용하려면 `select` 요소에 `multiple` 어트리뷰트를 추가하는데, React에서는 `select` 요소에 `multiple={true}`를 설정하고 `value`는 array 타입의 값(여러 값이 배열의 형태로 들어가기 때문)을 주면 됨.

    - 사용자가 선택한 값들을 이벤트 핸들러로 업데이트해야 함.

- controlled component와 uncontrolled component

  - controlled component : React가 제어할 수 있는 컴포넌트

  - uncontrolled component :  React가 제어할 수 없는 컴포넌트

    - "React가 제어할 수 없다" => 사용자가 데이터를 입력하면 React에서 별도 처리 없이 요소에 바로 반영되며, 특정 필드가 특정 속성을 갖도록 강제할 수 없음. 

    - uncontrolled comp의 경우 DOM 자체에서 데이터를 다루게 되는데, <i>`ref` 속성</i>을 사용하여 DOM에서 폼 값을 가져올 수 있음.
