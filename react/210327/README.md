# 21/03/27 학습 내용

### 고차 컴포넌트(HOC)

- 

___
### styled-components

- styled-components는 CSS in JS 라이브러리 중 하나임.

  - CSS in JS는 말 그대로 자바스크립트 안에 CSS를 작성하는 것을 의미함.

  - 다른 CSS in JS 라이브러리로는 emotion, styled-jsx, jss 등이 있음.

- styled-components는 스타일을 선언함과 동시에 컴포넌트를 생성함.

- tagged template literal 문법

  - tagged template literal은 template literal 문법을 이용하여 함수의 인자를 파싱해서 넘겨줌. ([참고](https://medium.com/@yeon22/javascript-tagged-template-literals%EB%9E%80-d7dca9461a45))

    ```js
    const favColor = 'pink';
    const favCoffee = 'caffe latte';

    const getSnack = (string, color, coffee) => {
      return string[0] + color + string[1] + coffee + string[2];
    };

    const res = getSnack`I like ${favColor} and ${favCoffee}!`;

    console.log(res);
    // I like pink and caffe latte!
    ```
    
    ![image](https://user-images.githubusercontent.com/54733637/112719971-2c11ae80-8f3f-11eb-8945-83379a2d323d.png)

  - 이러한 tagged template literal을 가장 많이 사용하는 상황이 바로 styled-components 라이브러리를 사용할 때임. styled-components에서 tagged template literal은 상위 컴포넌트로부터 전달되는 props를 읽기 위해 활용됨.

