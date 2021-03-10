# 20/10/22 수업 내용
### 애니메이션 작업

- 애니메이션 작업을 할 때 제일 먼저 할 일 : **시나리오 짜기** !

    1. 애니메이션 이름을 정한다.

    2. 원하는 변화에 맞춰 설계해본다.

- 애니메이션 효과 중 이동하는 효과를 주고 싶을 땐, `transform` 속성의 `translate`를 사용하는 것이 성능 상 가장 좋음.

- `animation` 속성

  - `duration`은 필수, `delay`는 옵션 ! (그래서 단축 속성으로 쓸 때는 먼저 오는 게 `duration` 값임.)

  - `transition-timing-function`

    - 애니메이션의 자연스러움을 조절할 수 있음.

    - 보통은 `linear`를 많이 쓰고, 만약 `cubic-bezier`를 쓰고 싶을 땐 아래 사이트에서 값을 직접 커스터마이징할 수 있음.

      - [cubic-bezier.com](https://cubic-bezier.com/)

### 마진 병합 현상(margin collapse)

- 마진 병합 현상은 마진 중복이라고도 하며, 인접하는 블록요소의 **상하단**의 마진이 병합되는 현상을 의미함. ([참고](https://velog.io/@ursr0706/%EB%A7%88%EC%A7%84margin))

  1. 형제 요소 간 `margin-top`, `margin-bottom`이 만날 때 발생

  2. 부모 요소와 자식 요소의 `margin-top`들이 만날 때 발생

  3. 부모 요소와 자식 요소의 `margin-bottom`들이 만날 때 발생

- 마진 병합 현상을 응용하기도 함.

- 마진 병합 현상 제거하기

  - 부모-자식 간 마진 병합 현상만 제거하기

    1. 공간을 차지하는 요소를 추가하여 제거하는 방법 (일명 "선긋기" 방법 ㅎㅎ)

        - 예를 들어 부모 요소에 `border` 속성 또는 `padding` 속성 부여

    2. 부모 요소에 `float: left;`를 지정하는 방법

        - 원리 : 부모 요소를 기준으로 BFC가 만들어지기 때문

    3. 부모 요소에 `overflow: hidden;`을 지정하는 방법

  - 전체 마진 병합 현상 제거하기

    1. 자식 요소에 `display: inline-block;` 지정하는 방법

    2. 자식 요소에 `float: left;` 지정하는 방법

### 기타

- 
