# 20/10/19 수업 내용
### HTML5

- 현재 표준 : HTML5, XHTML 1.0, HTML 4.01

- HTML5의 콘텐츠 모델(content model)

  ![content model](https://github.com/ahnanne/TIL/blob/main/html/img/01-content-model.png?raw=true)
  ##### 참고 https://html.spec.whatwg.org/multipage/dom.html#content-models

  - Metadata content

    - base, link, meta, noscript, script, style, template, title

  - Flow content

    - 문서의 body 부분에 작성되는 거의 대부분의 요소들이 flow content로 분류됨.

  - Sectioning content

    - article, aside, nav, section

    - 섹셔닝 콘텐츠는 대부분 HTML5에서 새롭게 추가된 요소들이며, 이 콘텐츠들은 헤딩과 푸터의 범위를 정의함.

    - 섹셔닝 콘텐츠는 각각 암묵적으로 헤딩과 아웃라인을 포함함.

  - Heading content

    - h1, h2, h3, h4, h5, h6, hgroup

      - `<hgroup>` [(MDN)](https://developer.mozilla.org/ko/docs/Web/HTML/Element/hgroup)

        - 이 태그는 HTML5 완성 전에 W3C HTML에서 제거됐으나 여전히 WHATWG 명세의 일부이며, 대부분의 브라우저에서 부분적으로나마 지원하고 있음.

        - 문서 구획의 다단계 제목을 나타내며, 다수의 h1~h6 요소를 묶을 때 사용함.
      - cf.) `<header>`는 보통 제목을 포함하긴 하지만, 헤딩 콘텐츠는 아님.

    - 헤딩 콘텐츠는 섹션의 헤딩을 정의하며, 문서의 암묵적인 아웃라인을 형성함.

  - Phrasing content

    ![phrasing content](https://github.com/ahnanne/TIL/blob/main/html/img/01-phrasing-content.png?raw=true)

    - 문서의 텍스트 및 그 텍스트들을 마크업하는 요소들을 의미함.

    - [HTML Living Standard](https://html.spec.whatwg.org/multipage/dom.html#sectioning-content-2)에 의하면 <b>대부분의 phrasing content 내부에는 phrasing content만이 들어올 수 있음.</b>

      > Most elements that are categorized as phrasing content can only contain elements that are themselves categorized as phrasing content, not any flow content.

  - Embedded content

    - audio, canvas, embed, iframe, img, math, object, picture, svg, video

    - HTML 문서 밖의 resources를 HTML 문서에 집어넣거나, 이와 연관된 작업들을 하는 데 사용되는 콘텐츠를 의미함. [(출처)](https://fromyou.tistory.com/447)

  - Interactive content

    - a, audio, button, details, embed, iframe, img, input, label, select, textarea, video

    - '대화형 콘텐츠'라고도 하며, user interaction을 위한 콘텐츠를 의미함.

    - <b>interactive 요소 내에는 또 다른 interactive 요소가 올 수 없음.</b>

- HTML5로 넘어오면서 API가 등장함. (자바스크립트의 영역)

  - Web Socket

  - Web Storage

    - 서버가 아닌, 클라이언트 사이드에 데이터를 저장할 수 있도록 지원하는 기능

    - 쿠키와 기능 자체는 유사하나, 쿠키는 약 4KB까지 밖에 저장공간을 이용하지 못하는 반면, web storage는 약 5MB까지 저장공간을 이용할 수 있음. [(출처)](https://untitledtblog.tistory.com/47)

  - Web SQL Database

    - 클라이언트 단에도 데이터를 저장할 수 있게 하는 기능

    - 브라우저에 Database 엔진을 심어 로컬에서 자바스크립트로 사용할 수 있도록 함.

    - web storage와의 차이점 : web storage는 비교적 적은 양의 <u>간단한 데이터</u>를 저장하기에 적합한 로컬 저장소인 반면, web SQL database는 보다 구조적이고 체계화된 <u>관계형 데이터</u>를 대량으로 저장하기에 적합함. [(출처)](https://iamawebdeveloper.tistory.com/98)

  - Indexed Database [(출처)](https://developer.mozilla.org/ko/docs/Web/API/IndexedDB_API)

    - 파일이나 블롭 등 많은 양의 구조화된 데이터를 클라이언트에 저장하기 위한 로우 레벨 API로, 인덱스를 사용하여 데이터를 고성능으로 탐색할 수 있음.

    - web storage와의 차이점 : web storage는 적은 양의 데이터를 저장할 때는 유용하지만, 많은 양의 구조화된 데이터는 적합하지 않은데, 이런 상황에서 indexed db를 사용할 수 있음.

  - Application Cache

    - 웹 응용 프로그램을 cache하여, 인터넷 접속 없이 사용자가 접근할 수 있게 해줌. 웹 응용 프로그램의 오프라인 버전을 만들 때 이를 이용할 수 있음.

    - cache(캐시) : 캐시란, 자주 사용하는 데이터나 값을 미리 복사해놓는 임시 장소를 의미하며, 저장공간이 작고 비용이 비싼 대신 빠른 성능을 제공함. [(출처)](https://mangkyu.tistory.com/69)

  - Geolocation

  - File API

  - Drag&Drop

- outline algorithm

  - outline algorithm이란 정보 구조를 명확히 할 수 있도록 하는 개념을 의미함.

  - 이는 기존에도 있었던 개념이지만, HTML5에선 기존의 암묵적 방식이 아닌 명시적인 방식이 도입됨.

  - 특히 `<section>`과 `<article>`은 콘텐츠 그룹을 명확히 구분하기 위해 도입됨.

  - Chrome 확장 프로그램 중 [headingsMap](https://chrome.google.com/webstore/detail/headingsmap/flbjommegcjonpdmenkdiocclhjacmbi?hl=ko)과 [Web Developer](https://chrome.google.com/webstore/detail/web-developer/bfbameneiokkgbdmiekhjnmfkcnldhhm?hl=ko)을 사용하면 웹 페이지의 구조를 확인할 수 있음.

___
### Markup Language(마크업 언어)

- HTML은 마크업 언어임.

- 마크업 언어란?

  - mark, 즉 tag로 둘러싸인 언어로, 문서의 골격에 해당하는 부분을 작성하는 데 사용함.

- 마크업 언어에는 HTML뿐만 아니라 JSON, XML, SGML 등이 있음.

___
### WAI-ARIA

##### 참고 : [레진 WAI-ARIA 가이드라인에 대한 소개](https://tech.lezhin.com/2018/04/20/wai-aria)

- WAI-ARIA란?

  - WAI(Web Accessibility Initiative) : W3C에서 웹 접근성을 담당하는 조직

  - ARIA : RIA(Rich Internet Application) 기술에 대한 접근성 명세를 의미함. 즉 새로운 기술에 대응하는 접근성 명세라고 할 수 있음.

  - 웹 페이지를 구조화할 때도 다음과 같이 WAI-ARIA 기법을 사용하여 각 `<div>`의 역할을 구분지어줄 수도 있음.

    ```html
    <div role="banner">

    <!--페이지의 시작 부분에 오는 콘텐츠-->
    <!--header 태그와 동일한 의미-->
    ```

    - 하지만 굳이 이렇게 하는 것보단 HTML5의 시맨틱 태그들을 이용하는 것이 더 효율적임.

    - 전체 구조를 건드리지 않고 유지보수해야 하는 상황에서는 이와 같은 방법을 쓰기도 함.

  - role 어트리뷰트

    - role 어트리뷰트는 웹 접근성 차원에서 위젯, 구조 및 동작에 대한 정보를 올바르고 명확하게 전달하기 위해 등장했음.

      - role 어트리뷰트의 다양한 값들 : [클릭!](https://happycording.tistory.com/entry/HTML-Role-왜-사용해야만-하는가)
  
    - 예를 들어, a 태그를 button 태그처럼 사용하는 경우에는 아래와 같이 role 어트리뷰트를 사용하여 버튼임을 표시할 수 있음.

      ```html
      <a role="button">
      ```

  - 이 외에도 WAI-ARIA에 대해선 매 수업 시간마다 언급되었던 내용을 바탕으로 조금씩 정리해나갈 예정임.

___
### 실습

- 설계

  - 코드를 짜기 전에는 늘 설계✨를 먼저 해야 함.

  - 웹 접근성에 대한 고려

    - 웹 접근성을 위해 markup 단에서 신경써야 하는 부분이 많음.

      - 대표적인 예로 skip navigation 기능을 첫 머리에 달아놓아야 함.

    - WCAG 2.1(웹 접근성 지침) by W3C : 직전 표준인 WCAG 2.0에서는 데스크톱 환경 위주의 웹 접근성을 다루었다면, 2.1 표준에서는 스마트폰, 태블릿과 같은 모바일 환경에서의 웹 접근성을 다루고 있음.

  - 마크업 과정

    >1. 구조 고민
    >
    >2. 논리적 순서 고민
    >
    >3. 시맨틱 마크업 고민
    >
    >4. 네이밍 고민
    >
    ><i>※ 마크업 과정에선 디자인에 대한 고민은 잠시 접어두자.</i>

    1. 구조

      - 3단 vs 4단

        ![3단 구조와 4단 구조 비교](https://github.com/ahnanne/TIL/blob/main/html/img/01-mark-up1.png?raw=true)

        - 각 영역의 <b>배치</b>를 변경하고 싶을 경우 HTML의 구조를 변경하지 말고 CSS를 이용하면 됨.

        - 실습에서는 3단 구조를 선택했음.

    2. 논리적 순서

      - 구조를 짤 때는 늘 논리적인 순서를 고민해야 함.

      - 논리적인 순서대로 마크업을 하고, 배치 등의 디자인은 CSS로 하면 됨.

      - 레이아웃을 마크업할 땐 더 이상 table 요소를 이용하지 않음. table 요소는 단순히 데이터를 보여주기 위한 마크업이며, 배치하기 위한 용도로 쓰이면 안됨.

      - <b>서로 독립적인 콘텐츠</b>들일 경우, 논리적 순서는 위에서 아래로, 왼쪽에서 오른쪽으로 가는 순서로 구성해도 됨.

    3. 시맨틱 마크업

      - 시맨틱 마크업이란, 기계가 처리할 수 있고 동시에 사람도 이해할 수 있는 마크업을 의미함.

    4. 네이밍

      - 영어권의 trendy한 naming을 따를 것을 권장함.

- 실습 구조(기본 골격) 짜기

  ![실습 구조](https://github.com/ahnanne/TIL/blob/main/html/img/01-mark-up2.png?raw=true)

  - multi class naming(멀티 클래스 네이밍)

    - 하나의 요소에 여러 클래스를 부여하는 것

    - 띄어쓰기로 구분

  - main은 한 페이지에서 딱 한 번만 사용 가능!

    - cf.) header, footer는 한 페이지 안에서도 여러번 사용 가능함.

  - 메인페이지의 파일 이름은 index.html로 지음.

    - root directory에 접근했을 때 가장 먼저 보여지도록 하기 위함.

  - language code

    ```html
    <html lang="ko-KR">
    ```

    - primary code : `ko`(korean)

    - subcode : `-KR`(Korea, Republic)

  - title

    - title 태그에는 핵심 키워드가 포함되어야 함.

    - title은 접근성 및 SEO(Search Engine Optimization, 검색 엔진 최적화)와 관련있음.

- CSS

  - CSS의 3가지 주요 개념

    - 겹침(cascade)

    - 상속

    - 우선순위

  - 네이밍할 때는 id보다는 class명을 지어주는 것이 재사용 측면에서 용이함.

    - 네이밍 방법론 : SMCSS, OOCSS, BEM

- font

  - font-family property [(MDN)](https://developer.mozilla.org/ko/docs/Web/CSS/font-family)

    - `serif` vs `sans-serif` : 전자는 삐침이 있는 글씨체, 후자는 삐침이 없는 글씨체

  - 한글 폰트

    - 한글 폰트는 압축 용량이 크기 때문에 성능 이슈가 있을 수 있으므로, 너무 용량이 큰 것은 사용을 지양할 것

    - 아시아권을 위해 제작된 폰트를 사용하는 것이 좋음.

      - ex) Noto Sans, [Spoqa Han Sans](https://spoqa.github.io/spoqa-han-sans/ko-KR/)

    - line-height 프로퍼티를 사용하는 경우, 영어권과 달리 한글의 경우 `line-height: 1;`로 설정하면 폰트에 따라 일부분이 짤려서 출력될 수도 있으므로 `line-height: 1.5;`로 지정하는 것을 권장

  - font-weight 프로퍼티는 `bold` 등의 값을 주기 보다는 그냥 숫자로 지정하는 것이 좋음. (호환성 이슈)

  - 브라우저에서 font 적용 여부 확인하는 방법

    ![font 적용 여부 확인 스크린샷](https://github.com/ahnanne/TIL/blob/main/html/img/01-font.png?raw=true)

    - 위 스크린샷과 같이, Status=200 뜨면 해당 글꼴이 정상적으로 적용되었음을 의미함.

- [Normalize.css](https://necolas.github.io/normalize.css/)

- vendor prefix

  ![vendor prefix](https://github.com/ahnanne/TIL/blob/main/html/img/01-prefix.png?raw=true)

- height 프로퍼티 값은 필수적으로 고정해야 하는 경우가 아니라면, 가급적이면 고정하지 않는 것이 좋음.
