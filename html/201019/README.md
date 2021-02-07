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

- 

___
### 실습

- 
