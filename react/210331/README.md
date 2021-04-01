# 21/03/31 학습 내용

### React Router

#### `<Link>` ([참고](https://reactrouter.com/web/api/Link))

- `a` 태그 대신 리액트 라우터의 `<Link>`를 사용하면 페이지를 리로드하지 않고도 원하는 페이지로 이동할 수 있음.

#### `<NavLink>` ([참고](https://reactrouter.com/web/api/NavLink))

- `<NavLink>`는 `<Link>`의 특별한 버전으로서, 현재 URL과 `to`의 목적지가 일치할 경우 스타일링을 부여함.

  - `acitveClassName`을 주고 `activeStyle`을 직접 주거나, 모듈 CSS를 사용하여 해당 `acitveClassName`에 스타일링하면 됨.

___
### Cloud Firestore(DB)

- Firebase의 Firestore는 NoSQL 데이터베이스를 지원해주며, 실시간(realtime) 데이터베이스도 지원함.

  - 실시간 데이터베이스 : 실시간으로 데이터베이스에 내용을 저장할 수 있고, 모든 클라이언트에서 실시간으로 데이터가 동기화됨.

- 구조

  ![image](https://user-images.githubusercontent.com/54733637/113275103-60a7b080-9319-11eb-8fd9-c10e9568c5b6.png)
  
    - firestore에선 data를 field라고 부름.
