# 21/03/30 학습 내용

### Firebase

- Firebase 사용 이점

  - Firebase SDK 인증(Auth), 데이터베이스(Cloud Firestore), 스토리지(Storage) 등의 서비스를 제공하여, 간단한 웹 애플리케이션을 만들 때 유용함.

- Firebase에서 커스텀 클레임 및 보안 규칙으로 액세스 제어하기([참고](https://firebase.google.com/docs/auth/admin/custom-claims?hl=ko))

___
### Focus Trapping for Accessibility (A11Y)

- 원문 출처 : https://medium.com/@im_rahul/focus-trapping-looping-b3ee658e5177

  - <b>키보드 네비게이션</b>은 접근성을 위한 기본적인 사항이며, 이는 시멘틱 마크업, `tabIndex`, `aria` attribute 및 자바스크립트를 사용하여 어렵지 않게 구현할 수 있다.

  - 로그인 버튼과 회원가입 버튼이 있는 로그인 페이지를 생각해보자. 각각의 버튼은 다이얼로그를 띄울 것이다. 이 상황에서 올바른 키보드 네비게이션은 아래와 같다.

    > 😣 여기서 '다이얼로그'가 바로 우리가 흔히 말하는 '모달'인데, 둘은 엄연히 다른 개념이다! `div` 요소로 다이얼로그를 만들 땐 접근성을 위해 `role="dialog"`와 `aria-modal=(true|false)`를 필수로 지정하고, `aria-label`|`aria-labelledby`, `aria-describedby`를 상황에 맞게 지정해주자.

    1. 다이얼로그가 뜨면 interactable 요소들 중 첫 번째 요소에 포커스가 가야 한다.

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
