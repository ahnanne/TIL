# 20/11/02 수업 내용
### 반응형 웹 디자인(Responsive Web Design)

- 반응형 웹 디자인(Responsive Web Design)

  - 반응형 웹 디자인을 할 땐 CSS 전처리기를 많이 사용함.

  - OSMU(one source multi use) : 디바이스별로 페이지를 만드는 것이 아니라, 하나의 페이지를 각각의 디바이스에 맞게 레이아웃만 변화시키는 것

  - 설계

    - mobile first로 설계하는 것을 권장하지만, 현업에서는 보통 desktop first로 설계함. (desktop에서 이미 서비스를 하고 있는 경우가 많기 때문)

    - desktop first 방식으로 하게 되면 성능 issue가 발생할 수도 있음. (덮어쓰는 방식이기 때문)

  - 960 design에서 컨텐츠 너비는 900 => 총 0.9375만큼의 영역을 차지함.

  - CSS media query(미디어 쿼리) 활용

    - 미디어 쿼리란 참 또는 거짓을 나타내는 논리적 표현식임. ([참고](https://www.w3.org/TR/css3-mediaqueries/#media0))

      - 만약 미디어 쿼리의 미디어 타입(media type)이 기기의 미디어 타입과 일치한다면 그 미디어 쿼리는 참이 되고, 그 미디어 쿼리의 모든 내용도 참이 됨.

    - 미디어 쿼리는 반응형 웹을 만들 때 주로 사용하며, 미디어 쿼리의 미디어 타입에는 총 4가지가 있음.

        1. `all` : **모든 디바이스**를 대상으로 하는 조건임을 의미

        2. `print` : **프린트 미리보기 모드** 또는 **PDF**에 대한 조건임을 의미

        3. `screen` : **컴퓨터 스크린**을 대상으로 하는 조건임을 의미

        4. `speech` : **음성 합성기**(speech synthesizer)를 대상으로 하는 조건임을 의미

    - 아래의 중단점(breakpoint)마다 재정의

      ![image](https://user-images.githubusercontent.com/54733637/110613452-a23eb300-81d4-11eb-9940-cfb806c383dc.png)

  - 반응형 웹에서 이미지 요소에 `max-width: 100%;`를 지정해주면, 이미지가 커지더라도 원본 이상으로는 커지지 않음.
