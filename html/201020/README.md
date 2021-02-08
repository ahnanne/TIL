# 20/10/20 수업 내용
### box model

- [MDN](https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/%EC%83%81%EC%9E%90_%EB%AA%A8%EB%8D%B8)은 box에 대해 다음과 같이 설명하고 있음.

  > CSS에 포함되는 모든 요소의 외장은 박스이며, 이 박스를 이해하는 것은 CSS를 통해 <b>레이아웃을 생성</b>하거나, 아이템과 다른 아이템을 <b>정렬</b>하는 것을 가능하게 하는 열쇠입니다.

- box model은 이러한 box가 동작하는 알고리즘인데, 쉽게 말해 요소의 크기 계산 기준이라고 할 수 있음.

- box model은 브라우저에서 아래의 그림과 같이 확인할 수 있음.

  ![box model](https://github.com/ahnanne/TIL/blob/main/html/img/02-box-model.png?raw=true)

  - 어떤 요소의 box-sizing 프로퍼티의 값을 위 3개의 값 중 어느 것으로 하는지에 따라, 해당 요소의 width와 height가 차지하는 범위가 달라짐.

  - default 값은 `content-box`이며, 이는 요소의 순수 너비(width, height)만으로 요소의 크기를 계산함. 즉, border의 굵기가 굵어질수록 요소의 전체적인 크기도 증가하게 됨. 이런 부분도 고려해서 너비를 지정해줘야 하기 때문에 직접 계산 방법이라고도 부름.

  - `border-box`는 이와 달리 요소의 너비를 계산할 때 padding과 border까지 포함하여 계산하기 때문에, 자동 계산 방법이라고도 부름.

  - `padding-box`는 브라우저 호환성이 떨어지므로 사용하지 않음.

___
### reflow & repaint

- 

___
### accessibility tree(접근성 트리)

- 

___
### 실습

- auto margin 기법

  - 가운데 정렬을 하기 위해 사용하는 trick

  - 방법 : 가운데 정렬하려는 box의 margin 프로퍼티의 값을 아래와 같이 지정함.

  ```css
  margin: 0 auto;
  ```

  - 가운데 정렬하려는 요소의 width 값을 연산할 수 없는 경우 또는 해당 요소가 inline 요소일 경우에는 auto margin 기법이 제대로 동작하지 않음.
