# 20/10/21 수업 내용
### navigation(메인메뉴)

- `nav` 태그

  - `nav` 태그는 주로 <b>메인메뉴</b>에 쓰임. => 2개 이하로 사용할 것을 권장함.

- 메뉴를 wrapping할 때, ①menu를 눌러 다른 페이지로 넘어가려는 경우에는 `a` 태그로 wrapping하고, ②마우스오버할 때 하위 메뉴를 보여주려는 목적으로 사용하는 경우에는 `button` 태그로 wrapping하여 접근성 향상

  - 이와 같이 `a` 태그를 버튼으로 쓸 때는 `role="button"` 지정해 줄 것

  - `button` 태그는 `box-sizing`의 기본값이 `border-box`이며, `a` 태그의 기본값은 `content-box`임.

  - cf.) `span`/`div`로 wrapping하는 경우에는 접근성 측면에서 `role="button"`과 `tabindex="0"`(대화형 컨텐츠가 아니므로 `tabindex` 지정하지 않으면 포커싱 받지 않음)을 추가할 것

    - 메뉴는 보통 내부 컨텐츠가 text(인라인 요소)이므로 `div` 보다는 `span`으로 감싸는 게 더 자연스러움.

- `button` 태그

  - `button` 태그의 attribute 중 `type`에는 아래의 3가지 값이 옴.

    1. `button` : 일반적인 버튼

    2. `reset` : 초기화를 위한 버튼

    3. `submit` : 서버로 데이터를 제출하기 위한 버튼 => type 명시 안 해줄 경우 기본값

  - `button` 태그는 focus를 받으면 outline이 생기는데, CSS에서 아래 방법으로 제거할 수 있음.

    ```css
    button:focus {
     outline: none;
    }
    ```
    
- line-heigth trick(수직 정렬)

  - 수직 정렬하려는 요소에, 그 요소를 감싸고 있는 바깥 요소의 `height`와 동일한 값으로 `line-height`를 지정하면 수직 정렬한 것과 같은 효과가 나타남.

  - 이 방법 외에도, 수직 정렬하려는 요소의 위·아래에 패딩 값을 주는 방법도 있음.

- 구분선 넣기

  - 구분선(divider)을 넣는 방법으로는 여러가지가 있음.

    1. `border` 속성 이용하기

    2. `background` 속성 이용하기

    3. `box-shadow` 속성 이용하기

    4. 가상 선택자 이용하기

- shadow 속성

  - `box-shadow`, `text-shadow` 등 shadow 속성을 활용하여, 선명한 선 뿐만 아니라 다양한 스타일의 윤곽선을 만들 수 있음.

  - shadow는 여러 번 깔 수 있는데, 이를 응용하여 아래와 같이 text에 윤곽선 효과를 줄 수도 있음.

    ![image](https://user-images.githubusercontent.com/54733637/109491432-e5aa6a80-7acc-11eb-8c1f-182bdc5d97be.png)

- `currentColor`

  - CSS의 색상 관련 속성들의 값으로 `currentColor`를 사용할 수 있는데, 이는 현재 text color와 동일한 색을 쓰겠다는 것을 의미함.

- `cursor` 속성

  - 마우스 커서를 변경함.

  - `cursor: pointer;` => 마우스 커서 모양을 손모양으로 변경

    - cf.) `cursor: hand;`는 비표준(IE6에서만 동작)

### `.a11y-hidden` 기법

- `a11y`는 accessibility를 의미함.

- 사용 목적 : 숨김 콘텐츠를 만드는 기법으로, 접근성 측면에서는 필요하지만 시각적으로는 표현될 필요가 없는 요소에 대해서 사용함.

- 클래스 명을 `a11y-hidden` 대신 `readable-hidden` 또는 `offscreen` 등으로 네이밍하기도 함.

- 사용 방법([참고](https://codepen.io/ahnanne/pen/gOMwJWv?editors=1100))

  ![image](https://user-images.githubusercontent.com/54733637/109480218-9bba8800-7abe-11eb-9dac-7b5ece57d2c6.png)
  
  - `clip-path`

    - 요소의 클리핑 범위를 지정하는 속성으로, 클리핑 범위 안의 부분은 보여지고, 바깥 부분은 숨겨짐. ([MDN](https://developer.mozilla.org/ko/docs/Web/CSS/clip-path))

    - CSS clip-path maker 사이트 : https://bennettfeely.com/clippy/([바로가기](https://bennettfeely.com/clippy/))

      - 사용 방법

        ![image](https://user-images.githubusercontent.com/54733637/109481739-77f84180-7ac0-11eb-9b24-5ec2d60eacca.png)

___
### 그라디언트

- CSS Gradient Generator([바로가기](https://www.colorzilla.com/gradient-editor/))와 같은 사이트에서 원하는 그라디언트를 만들고 코드를 붙여넣어서 사용할 수 있음.

  ![image](https://user-images.githubusercontent.com/54733637/109490061-0ec9fb80-7acb-11eb-86aa-2401e2e04475.png)

___
### 기타 실습 관련 내용

- `position: absolute;`

  - 요소를 배치하기 위해 `position: absolute;`를 사용하면, 해당 요소는 <b>normal flow</b>를 벗어나므로 페이지 레이아웃에 공간을 차지하지 않게 됨.

  - `position: absolute;`를 지정한 요소는 `position: static;`이 아닌 가장 가까운 상위 요소의 위치를 기준으로 상대적으로 배치됨.

    - 단, 조상 요소가 모두 `position: static;`이라면, 원래 해당 요소가 normal-flow에서 갖는 위치를 기준으로 배치됨.

- 아이콘

  - 아이콘을 마크업할 때는 `i` 태그 보다는 `span` 태그를 쓰는 게 좋음.

  - 단순히 꾸미는 용도로 아이콘을 쓰는 경우에는 접근성 측면에서 `aria-hidden="true"`를 지정해줘야 함.

- `white-space` 속성

  - 상세 설명 참조 : [MDN](https://developer.mozilla.org/ko/docs/Web/CSS/white-space)

  - `white-space` 속성은 요소가 공백 문자를 처리하는 법을 지정함.

  - 속성 값 예제는 [코드펜](https://codepen.io/ahnanne/pen/qBNqrag?editors=1100) 참고

  - 실습에서 본 속성을 활용한 이유

    ![image](https://user-images.githubusercontent.com/54733637/109494864-cf52dd80-7ad1-11eb-8806-e1844119877a.png)
    
    - 현업에서는 이 속성을 활용하는 대신, `width` 값을 늘리는 임시방편을 쓰기도 하나 비추

- 마크업 문법 검사

  - W3C html validator 이용 ([링크](https://validator.w3.org/))

  - Web developer 기능 이용

    - 작업 중인 html 파일을 VS Code의 라이브 서버로 오픈한 후, 아래 그림에서 표시한 기능을 클릭

      ![image](https://user-images.githubusercontent.com/54733637/109495519-bc8cd880-7ad2-11eb-9d20-fc2771cb8ecd.png)


___
### BFC(Block Formatting Context)

- BFC(Block Formatting Context) ([참고](https://blueshw.github.io/2020/05/17/know-css-block-formatting-context/))

  - float으로 생성된 BFC는 자식 요소를 데리고 함께 부유함.

  - BFC는 언제 생기는가?

    1. float을 지정한 요소에 생긴다.

    2. `overflow:hidden;`을 지정한 요소에 생긴다.

    3. `position: absolute;`을 지정한 요소에 생긴다.

    4. `position: relative;`을 지정한 요소에 생긴다.

    5. `position: fixed;`을 지정한 요소에 생긴다.
