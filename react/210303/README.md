# 21/03/03 수업 내용
### `useRef`로 컴포넌트 안의 변수 만들기

- 컴포넌트 내부에서 `let` 키워드로 변수를 선언한다고 가정해보자. 리렌더링될 때 그 변수값은 초기화된다.

- 만약 계속 유지하고 싶은 어떤 값을 관리하려면 `useState`를 사용해야 하는데, `useState`는 상태를 바꾸면 컴포넌트가 리렌더링 됨. 굳이 리렌더링할 필요가 없는 경우에도!

  - 그래서 `useState` 대신 `useRef`를 사용한다.

- `ref`를 사용해야 할 때 이 `useRef`라는 hook을 사용한다고 했는데, `useRef`는 이 외에도 컴포넌트가 리렌더링될 때마다 "계속 기억해야 하는 값"을 관리할 때도 사용할 수 있다.

  - "계속 기억해야 하는 값"에는 ① `setTimeout`, `setInterval`의 timer id, ② 외부 라이브러리를 사용하여 생성된 인스턴스, ③ Scroll 위치 등등 다양한 값이 있을 것이다.

- `useRef`로 관리하는 값은, **값이 바뀌어도 컴포넌트가 리렌더링이 되지 않는다**!

  ```js
  const nextId = useRef(4);

  const onCreate = () => {
    console.log(nextId.current);

    // 새로운 항목 만들때마다 새로운 아이디값 만들기
    nextId.current += 1;
    // nextId 값이 바뀐다고 해서 컴포넌트가 리렌더링 되지는 않음.
    // nextId는 useRef로 관리하기 때문!
  };
  ```

  > `useRef` returns a mutable ref object whose `.current` property is initialized to the passed argument (`initialValue`). The returned object will persist for the full lifetime of the component.

  > Note that `useRef()` is useful for more than the `ref` attribute. It’s handy for keeping any mutable value around similar to how you’d use instance fields in classes.

___
### 배열에 항목 추가하기

- 이벤트 핸들러(또는 이벤트 리스너)는 이벤트가 발생했을 때 브라우저에 호출을 위임한 함수인데, 이러한 이벤트 핸들러를 등록하는 방식에는 3가지가 있음.

  1. **이벤트 핸들러 어트리뷰트 방식**

  2. 이벤트 핸들러 프로퍼티 방식

  3. `addEventListener` 메서드 방식

- 자바스크립트에서는 "[겸손한 자바스크립트(unobtrusive javascript)](https://blog.martinwork.co.kr/javascript/2017/07/23/unobstrusive-javascript.html)" 방식에 따라 위의 2번과 3번 방식을 주로 사용했지만, React를 비롯하여 Angular, Svelte, Vue.js와 같은 **CBD(Component Based Development)** 프레임워크 및 라이브러리에서는 **이벤트 핸들러 어트리뷰트** 방식으로 이벤트를 처리함!

  - **겸손한 자바스크립트 방식**은 HTML/CSS/JS는 각각 역할과 목표가 다르므로 혼재하지 않아야 한다는 입장인 반면, **CBD**는 HTML/CSS/JS 모두 뷰를 구성하기 위한 구성 요소로 보기 때문에 공통의 관심사를 갖는다는 입장임.

- 여러 개의 input 값을 관리할 때는 `useState`를 사용하며 객체 형태로 상태를 만들어주면 됨.

- 기존의 배열을 바꾸지 않으면서, 기존 배열을 복사한 새로운 배열을 만들어서 그 새로운 배열에 변화를 주는 방식으로 구현해야 함.

  - 즉, 배열의 불변성을 지켜야 함.

  - 배열을 복사하기 위해 스프레드 문법(ES6)이나 `concat` 메서드(ES5)를 사용 

    - `concat` 메서드는 인수로 전달된 값(배열 또는 배열이 아닌 값)(들)을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환하는 accessor method임.

    - `concat` 메서드에 인수로 전달하는 값이 **배열**인 경우에는, 인수로 전달된 배열을 **해체**하여 새로운 배열의 요소로 추가함! (중첩 배열을 전달할 경우에는 1단계까지만 해체)

    - `concat` 메서드에는 0개 이상의 인수를 전달할 수 있는데, 만약 인수를 전달하지 않으면 원본 배열을 그대로 복사함.

      ```js
      const arr = [1, 2, 4, 7];

      const _arr = arr.concat();
      console.log(_arr); // [ 1, 2, 4, 7 ]
      ```

      - 원본 배열을 변경하는 mutartor method인 `push`는 사용하면 안됨.

        ```js
        // good
        const arr1 = [1, 2, 4, 7];

        const _arr1 = arr1.concat(3);
        console.log(_arr1); // [ 1, 2, 4, 7, 3 ]

        console.log(arr1); // [ 1, 2, 4, 7 ] → 불변

        // bad
        const arr2 = [1, 2, 4, 7];

        arr2.push(3);
        console.log(arr2); // [ 1, 2, 4, 7, 3 ]
        ```

___
### 배열에 항목 제거하기

- 이벤트 핸들러 등록 관련

  ![image](https://user-images.githubusercontent.com/54733637/109794797-95144800-7c59-11eb-81e0-3c3ce90312cf.png)
  
- 배열에서 특정 요소를 제거할 때는 `filter` 메서드가 유용함.

___
### 배열에 항목 수정하기

- 계정을 클릭했을 때 텍스트 컬러 바꾸는 기능 구현하기

  - 각 user에 `active`라는 프로퍼티를 추가적으로 부여하고 이를 이용해 control해보자.

  - 삼항 조건 연산자 사용하기

    ![image](https://user-images.githubusercontent.com/54733637/109797190-7794ad80-7c5c-11eb-95c0-9f61c5cae6e1.png)
  
  - `active` 값 토글하는 함수 만들고 이벤트 핸들러 등록해주기

- 배열 안에 있는 요소를 업데이트 할 때는 `map` 메서드가 유용함.

___
### `useState`

- 참고 : https://ko.reactjs.org/docs/hooks-state.html#declaring-a-state-variable

- `useState()`를 콘솔창에 찍어보면, 요소가 두 개인 배열임을 알 수 있음.

  ![image](https://user-images.githubusercontent.com/54733637/109800550-a876e180-7c60-11eb-8a17-5d7e29829a6a.png)

    1. 첫 번째 요소 : **state 변수**(상태 변수)

    2. 두 번째 요소 : 첫 번째 요소(state 변수)를 **갱신하는 함수**

      - 이 함수의 인수로는 **상태 변수를 갱신할 값** 자체를 전달해야 함.

      - cf.) 클래스형 컴포넌트에서는 `this.setState`를 쓴다고 함.

- `useState()`의 인수로는 state 변수의 **초기값**으로 설정할 값을 전달해야 함.

  - 즉, state 변수의 선언과 함께 최초로 할당하려는 값을 전달할 것
