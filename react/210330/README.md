# 21/03/30 학습 내용

### Firebase

- Firebase 사용 이점

  - Firebase SDK 인증(Auth), 데이터베이스(Cloud Firestore), 스토리지(Storage) 등의 서비스를 제공하여, 간단한 웹 애플리케이션을 만들 때 유용함.

- Firebase에서 커스텀 클레임 및 보안 규칙으로 액세스 제어하기([참고1](https://firebase.google.com/docs/auth/admin/custom-claims?hl=ko), [참고2](https://youtu.be/3hj_r_N0qMs))

  > 이 기능을 사용하면 사용자를 그룹화하여 권한을 다르게 부여할 수 있다. (ex - 글쓰기 권한이 있는 회원과 없는 회원)

  - email/pw로 로그인하든, GitHub나 Google 계정으로 로그인하든, 결국 <b>Firebase ID token</b>을 발급 받는다. 여기에 커스텀 클레임을 추가할 수 있음.

    ![image](https://user-images.githubusercontent.com/54733637/113069341-116b5e00-91fb-11eb-81f7-a4a10d2dcbbe.png)

    - 권한과 관련한 내용이 아닌, 해당 사용자에 대한 기타 정보는 Firebase ID token 내에 추가하지 말고 Cloud Fire Store 등의 DB에 저장할 것!

  - 커스텀 클레임

    - 커스텀 클레임이란 해당 사용자의 <b>권한</b>에 대한 key와 value의 쌍으로, 서버 단에서 설정할 수 있음.

    - 커스텀 클레임은 1000 바이트로 제한되어 있음.

  - 보안과 관련된 내용을 다룰 경우 커스텀 클레임을 사용하면 안되고, Firebase security rules를 이용해야 함. 커스텀 클레임은 개발자 도구 등으로 뜯어볼 수 있기 때문에 데이터 보안에 적합하지 않음.

    - 예를 들어, 글쓰기 권한에 대한 커스텀 클레임은 코드를 뜯어봐도 어차피 Firebase ID token에 글쓰기 권한이 없는 이상 글을 쓰지 못하니까 상관없음.

- Firebase 용어 정리

  - 스냅샷(snapshot)

    - 스냅샷은 단일 시점에 특정 데이터베이스 참조에 있던 데이터를 촬영한 사진이라고 생각하면 됨. ([공식 문서](https://firebase.google.com/docs/database/admin/retrieve-data#section-start))

___
### Focus Trapping for Accessibility (A11Y)

- 원문 출처 : https://medium.com/@im_rahul/focus-trapping-looping-b3ee658e5177

  - <b>키보드 네비게이션</b>은 접근성을 위한 기본적인 사항이며, 이는 시멘틱 마크업, `tabIndex`, `aria` attribute 및 자바스크립트를 사용하여 어렵지 않게 구현할 수 있다.

  - 로그인 버튼과 회원가입 버튼이 있는 로그인 페이지를 생각해보자. 각각의 버튼은 다이얼로그를 띄울 것이다. 이 상황에서 올바른 키보드 네비게이션은 아래와 같다.

    > 😣 여기서 '다이얼로그'가 바로 우리가 흔히 말하는 '모달'인데, 둘은 엄연히 다른 개념이다! `div` 요소로 다이얼로그를 만들 땐 접근성을 위해 `role="dialog"`와 `aria-modal=(true|false)`를 필수로 지정하고, `aria-label`|`aria-labelledby`, `aria-describedby`를 상황에 맞게 지정해주자.

    1. 다이얼로그가 뜨면 ~~interactable 요소들 중 첫 번째 요소에 포커스가 가야~~ 한다.

        - 임의로 auto-focus를 제공하는 것은 접근성 차원에서 또 다른 문제가 될 수 있다. 더 좋은 방법은 다이얼로그 자체(예를 들면 `aria-label` 등의 정보가 있는 다이얼로그 컨테이너 `div` 요소)에 `tabIndex=-1`을 지정하여, 맨 처음 다이얼로그가 떴을 때 포커스를 주는 것이다. (`tabIndex=-1`은 연속 키보드 탐색으로 접근할 수 없으므로, 이 경우 다이얼로그 컨테이너 자체는 다이얼로그 내 순환 탐색의 대상이 되지 않는 것이 .)

    2. 사용자는 해당 다이얼로그 내에서 `tab` 키를 사용하여 다음 interactable 요소로 이동할 수 있어야 한다.

    3. 다이얼로그가 계속 떠있는 상태에서는 `tab` 키를 계속 눌러도 포커스가 다이얼로그 바깥으로 나가면 안되고, 다이얼로그 안쪽의 interactable 요소들 사이에서 순환(loop)해야 한다.

        - `tab` 키를 누를 때는 물론이고, `shift` + `tab` 키를 누를 때도 마찬가지

        - `focusableNodeList = dialogNode.querySelectorAll( interactable 요소들 나열 );`

    4. 모바일 환경에서도 정상적으로 작동되려면, 다이얼로그가 열릴 때 다이얼로그 바깥의 모든 요소들에 `aria-hidden=true`를 지정해줘야 한다.

        - 이를 위해 가장 상위의 요소인 React root 요소에 `aria-hidden=true`를 지정해주면 됨.

    5. 다이얼로그가 닫히면, 다이얼로그를 열었던 버튼으로 다시 포커스가 가야 한다.

        - 만약 로그인 버튼을 눌렀었다면 다시 로그인 버튼으로(로그인을 완료한 상태라면 로그인 버튼이 없을테니 다른 요소로), 회원가입 버튼을 눌렀었다면 다시 회원가입 버튼으로 포커스가 가도록 해줄 것

- `tabIndex`([MDN](https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/tabindex))

  - `tabIndex`로 `1` 이상의 숫자를 주는 것은 지양하자.
  
    - 접근성 보조기술 사용자의 페이지 탐색과 조작에 방해될 수 있음.
    
    - 한번 순서를 건드리면 나머지 요소들의 `tabIndex`도 모두 조정을 해줘야 함.
    
  - 포커스가 원래 가지 않는 요소(not tabbable)에 포커스를 주려는 게 목적이라면 `tabIndex` 값으로 `음의 정수값`(보통 `-1`)이나 `0`을 주자.

    - `음의 정수값` : <u>연속 키보드 탐색으로 접근할 수는 없으나</u> 자바스크립트나 시각적(마우스 클릭)으로는 포커스 가능하도록 함.

    - `0` : <u>연속 키보드 탐색으로 요소에 접근할 수 있으며</u> 문서 소스 코드의 순서에 따라 포커스를 받음.

      - `양의 정수값`을 지정한 요소가 있는 상태라면 순서는 그 이후가 됨.
