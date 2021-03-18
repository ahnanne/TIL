# 21/03/17 학습 내용
### 클래스 컴포넌트의 `this` 바인딩

- <u>클래스 필드 정의 제안을 사용하여 클래스 필드에 화살표 함수를 할당하는 방식</u>은 기존의 `this` 바인딩을 위해 필요했던 추가적인 절차(`bind(this)` 사용)를 거치지 않아도 `this` 바인딩 문제를 해결할 수 있도록 해준다는 점에서 편리함.

  > 클래스 필드는 기본적으로 public함. (cf. private 필드 제안)

- <b>클래스 필드(class field, field, member)</b>는 "클래스가 생성할 **인스턴스의 프로퍼티**"를 가리킴.

- 클래스 안에서 `this`는 `constructor` 및 메서드들 내부에서만 유효하므로, 클래스 필드를 정의할 때는 `this`에 클래스 필드를 바인딩할 수 없음. (아래 그림 참고)

- 함수도 객체니까 클래스 필드에 할당할 수 있는데, 이렇게 정의된 메서드는 **인스턴스 메서드**가 됨.

  - 왜냐하면 클래스 필드란 "클래스가 생성할 **인스턴스의 프로퍼티**"를 의미하니까!

  - 따라서 클래스 필드에 함수를 할당하여 메서드를 만드는 방식은 권장되지 않음.

    - **인스턴스 메서드**는 인스턴스가 생성될 때마다 **중복 생성**되는바, 메모리 측면에서 좋지 않기 때문임.

- 클래스 필드에 할당한 화살표 함수는 인스턴스 메서드(인스턴스 프로퍼티)이며, 결국 `constructor` 내부에서 만들어지는 인스턴스 프로퍼티와 같다고 볼 수 있음.

  - 그리고 화살표 함수는 자체의 `this` 바인딩을 갖지 않고 상위 스코프의 `this` 바인딩을 따르는데, 여기서 화살표 함수의 상위 스코프는 `constructor`가 되고 **`constructor` 내부의 `this` 바인딩은 클래스가 생성한 인스턴스를 가리키므로**, 결론은 다음과 같다.

  > 클래스 필드에 할당한 화살표 함수 내부의 `this` 또한 클래스가 생성할 인스턴스를 가리킨다. (이웅모, 모던 자바스크립트 Deep Dive(2020), p.485)

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

___
### 불변 객체

- 정리 예정..(https://yamoo9.gitbook.io/learning-react-app/learning-history/props-vs-state#immutable-and-set-state, https://ko.wikipedia.org/wiki/%EB%B6%88%EB%B3%80%EA%B0%9D%EC%B2%B4)

___
### Immer

- 정리 예정..(https://medium.com/@wongni/%EC%9D%B4%EB%A8%B8-immer-%EB%A5%BC-%EC%86%8C%EA%B0%9C%ED%95%B4-%EB%B6%88%EB%B3%80%EC%84%B1-%EC%89%BD%EA%B2%8C-%ED%95%98%EC%9E%90-24b00b6ff13f)
