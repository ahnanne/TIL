# 21/03/30 학습 내용

### Firebase

- Firebase 사용 이점

  - Firebase SDK 인증(Auth), 데이터베이스(Cloud Firestore), 스토리지(Storage) 등의 서비스를 제공하여, 간단한 웹 애플리케이션을 만들 때 유용함.

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
