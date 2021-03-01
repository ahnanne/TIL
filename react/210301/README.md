# 21/03/01 수업 내용
### 특정 DOM 선택하기

- ref

  - 리액트에서는 DOM을 선택하기 위해 ref라는 것을 사용함.

  - 함수형 컴포넌트에서 ref를 사용할 때는 `useRef`라는 Hook 함수를 사용함.

    - cf.) 클래스형 컴포넌트에서는 `React.createRef()`라는 것을 사용함.

- 실습

  - ref를 사용해서 focus 요소 제어하기

    1. `useRef` 불러오기

      ```js
      import React, { useState, useRef } from 'react';
      ````

    2. `useRef` 호출하기
    
      ```js
      const nameInput = useRef();
      ```

    3. 원하는 DOM에 ref 설정해주기

    ```js
    <input name="name" placeholder="이름" onChange={onChange} value={name} ref={nameInput} />
    ```

    4. 필요할 때(ex: event handler 내부에서) 해당 DOM 선택하기

    ```js
    nameInput.current.focus();
    ```

- `useRef`는 DOM을 선택하는 것 말고도, 렌더링과 전혀 관계없는 변수를 관리할 때도 사용할 수 있음.

___
### 배열 렌더링하기

- 하나의 컴포넌트 파일에 두 개의 컴포넌트를 선언해도 됨.

- 예제

  ```js
  function User(props) {
    console.log(props);

    return (
      <div>
          <b>{props.character.name}</b> <span>{props.character.team}</span>
      </div>
    );
  }

  function UserList() {
    const characters = [
      {
        id: 1,
        name: 'Hanzo',
        team: 'red'
      },
      {
        id: 2,
        name: 'Sombra',
        team: 'blue'
      },
      {
        id: 3,
        name: 'Ana',
        team: 'red'
      }
    ];

    return (
      <div>
        {
          characters.map(elem => {
            console.log(elem);
            return (<User character={elem} />);
          })
        }
        {[1, 2, 3]}
        {/* 중괄호 안의 배열은 렌더링될 때 풀림. */}
      </div>
    );
  }
  ```