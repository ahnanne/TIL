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
  
    - 주의할 점 : `border-box`일 때는 width값과 height값을 아무리 작게 설정해도 요소의 전체 크기가 (padding×2) + (border×2)보다 작아지지 않음. [(참고)](https://codepen.io/ahnanne/pen/WNoxmrW)

  - `padding-box`는 브라우저 호환성이 떨어지므로 사용하지 않음.

___
### reflow & repaint

- reflow

  - reflow는 DOM node의 레이아웃 수치가 변경될 경우, 이로 인해 영향 받은 모든 node의 수치를 다시 계산(recalculate)하여 렌더 트리를 재생성하는 과정이다. (출처 : https://webclub.tistory.com/346)
  
  - 쉽게 말해, 컴퓨터 화면에서 node들이 차지하는 공간을 조정하는 것을 의미한다.
  
  - transform의 속성 중 translate과 같은 값은 reflow가 많이 발생하지 않음.
  
- repaint

  - reflow 과정이 끝난 후 재생성된 렌더 트리를 다시 그리는 과정을 repaint라고 한다.
  
  - background-color, visibility, outline 등의 스타일 변경 시에는 레이아웃 수치가 변경되지 않으므로, reflow 과정은 생략되고 repaint 과정만 일어나게 된다.

  - translate을 사용하면 브라우저가 gpu를 활용하는데, gpu는 repaint에서 압도적인 성능을 보인다. ➠ 성능 개선 !

___
### accessibility tree(접근성 트리)

- 접근성 트리는 DOM tree의 하위 집합으로서, <u>DOM tree의 요소들 중 스크린 리더와 같은 보조 기술을 사용할 때 유용한 요소들만 포함</u>됨. ([참고](https://nuli.navercorp.com/community/article/1133008))

- 어떤 요소에 `aria-hidden="true"`를 지정하면, 해당 요소 및 그 요소의 모든 자식 요소가 접근성 트리에서 제거됨!

  - 이와 같이, 순수하게 꾸미는 용도로만 사용한 요소들을 숨김으로써 정보통신 보조기기 사용자들의 접근성 및 경험을 향상시킬 수 있음.

___
### 실습

- auto margin 기법

  - 가운데 정렬을 하기 위해 사용하는 trick

  - 방법 : 가운데 정렬하려는 box의 margin 프로퍼티의 값을 아래와 같이 지정함.

  ```css
  margin: 0 auto;
  ```

  - 가운데 정렬하려는 요소의 width 값을 연산할 수 없는 경우 또는 해당 요소가 inline 요소일 경우에는 auto margin 기법이 제대로 동작하지 않음.
