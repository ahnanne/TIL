# 21/03/17 학습 내용
### 이벤트 핸들링 및 클래스 컴포넌트의 `this` 바인딩

- 정리 예정..

___
### Form 컨트롤

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

___
### 불변 객체

- 정리 예정..(https://yamoo9.gitbook.io/learning-react-app/learning-history/props-vs-state#immutable-and-set-state, https://ko.wikipedia.org/wiki/%EB%B6%88%EB%B3%80%EA%B0%9D%EC%B2%B4)

___
### Immer

- 정리 예정..(https://medium.com/@wongni/%EC%9D%B4%EB%A8%B8-immer-%EB%A5%BC-%EC%86%8C%EA%B0%9C%ED%95%B4-%EB%B6%88%EB%B3%80%EC%84%B1-%EC%89%BD%EA%B2%8C-%ED%95%98%EC%9E%90-24b00b6ff13f)
