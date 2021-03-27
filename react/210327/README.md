# 21/03/27 학습 내용

### 고차 컴포넌트(HOC)

- 

___
### styled-components

- styled-components는 CSS in JS 라이브러리 중 하나임.

  - CSS in JS는 말 그대로 자바스크립트 안에 CSS를 작성하는 것을 의미함.

  - 다른 CSS in JS 라이브러리로는 emotion, styled-jsx, jss 등이 있음.

- styled-components는 스타일을 선언함과 동시에 컴포넌트를 생성함.

#### tagged template literal 문법

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

    ```js
    import React from 'react';
    import styled, { css } from 'styled-components';

    const Circle = styled.div`
      width: 5rem;
      height: 5rem;
      background-color: ${props => props.color};
      border-radius: 50%;
      ${props => props.huge && css` // 💛
        width: 10rem;
        height: 10rem;
      `}
    `;

    export default function StyledComp() {
      return (
        <>
          <Circle color="#181818" huge />
          <Circle color="thistle" />
        </>
      );
    }
    ```

    - template literal 안에서 또 tagged template literal을 써야 한다면, 위 예시 코드에서와 같이 `styled-components`로부터 `{ css }`를 import 해오고 💛 표시한 부분과 같이 써주면 됨. (위 코드에서는 내부에서 또 tagged template literal을 굳이 쓰지 않아도 됐음.)

#### polished

- CSS in JS를 사용하면 `darken`, `lighten`, `opacify` 등 Sass 내장 함수들을 사용할 수 없음. ([참고](https://john015.netlify.app/polished-js%EB%A1%9C-js%EC%97%90%EC%84%9C-css%EB%A5%BC-%EC%9E%91%EC%84%B1%ED%95%A0-%EB%95%8C-sass-style-functions-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0))

  - Sass 내장 함수!? 😮

    - Sass에는 기본 제공되는 내장 함수들이 있음. 물론 일일이 다 외울 필요는 없고, 어떤 것들이 있다 정도로만 알아뒀다가 나중에 필요할 때 찾아서 쓰면 됨. → [참고(HEROPY)](https://heropy.blog/2018/01/31/sass/)

    - 위에서 언급된 내장 함수들만 우선 보자면, `darken`은 더 어두운 색을, `lighten`은 더 밝은 색을 만드는 역할을 하며, `opacify` 또는 `fade-in`은 색상을 더 불투명하게 만듦.

    - 이 외에도 인수로 전달한 두 가지 색상을 섞는 `mix` 함수, 인수로 전달한 색상을 반전시키는 `invert` 함수 등 다양한 함수가 있음.

    - 또한, 기존의 css 함수인 `rgba()`와 이름과 모양은 같지만 전달 받는 인수가 다른 `rgba()` 함수도 있음.

      - 전자는 4개의 인수를 전부 다 받는 반면, 후자는 첫 번째 인수로 색상 값, 두 번째 인수로 알파 값 이렇게 두 가지만 받으므로 투명도를 설정하기가 더 편리함.

- [polished](https://polished.js.org/docs/)를 사용하면 이와 같은 Sass 내장 함수들을 사용할 수 있음.