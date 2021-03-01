# Set과 Map
## Set

- Set 객체는 서로 중복되지 않는 <b>값(value)</b>들의 집합(set)으로, 배열과 유사하게 생긴 객체지만 <u>배열과 달리</u> ①동일한 값을 중복하여 포함할 수 없으며 ②요소 순서에 의미가 없고, ③index가 존재하지 않기 때문에 index로 요소에 접근할 수 없음.

- 대괄호가 아닌 중괄호로 감싼 배열처럼 생겼음!

- Set은 수학적 집합을 구현하기 위한 자료구조임. => 교집합, 합집합, 차집합, 여집합 등 구현 가능

### Set 객체 생성

- Set 객체는 Set 생성자 함수로 생성함.

  - Set 생성자 함수에는 이터러블을 인수로 전달하는데, 아무런 인수도 전달하지 않으면 빈 Set 객체가 생성됨.

  - 이터러블을 인수로 전달할 때, 이터러블의 중복된 값은 Set 객체에 요소로 저장되지 않음.

  - 이처럼 중복을 허용하지 않는 Set 객체의 특성을 활용하여, 배열에서 중복된 요소를 제거할 수 있음.

    ```js
    // 중복 요소 제거하기
    const arr = [2, 3, 4, 2, 3, 1, 3, 6, 7];

    // 방법1: Set 사용하기
    const newArrBySet = [...new Set(arr)].sort();

    console.log(newArrBySet); // [ 1, 2, 3, 4, 6, 7 ] -> EZ!🍭

    // 방법2: Set 사용하지 않기
    const newArr = arr.filter((elem, idx) => arr.indexOf(elem) === idx).sort();

    console.log(newArr); // [ 1, 2, 3, 4, 6, 7 ]
    ```

### 요소 개수 확인

- Set 객체의 요소 개수를 확인할 때는 `Set.prototype.size` 프로퍼티를 사용함.

  ```js
  const myStrSet = new Set('hello');
  console.log(myStrSet); // Set(4) { 'h', 'e', 'l', 'o' }
  
  console.log(myStrSet.size); // 4
  ```

- `size` 프로퍼티는 접근자 프로퍼티인데, setter 함수 없이 getter 함수만 존재하므로 새로운 값을 할당할 수 없음.

### 요소 추가

- Set 객체에 새로운 요소를 추가할 때는 `Set.prototype.add` 메서드를 사용함.

  ```js
  const myStrSet = new Set('hello');
  console.log(myStrSet);
  // Set(4) { 'h', 'e', 'l', 'o' }

  myStrSet.add('Anne', 'h');
  console.log(myStrSet);
  // Set(5) { 'h', 'e', 'l', 'o', 'Anne' } -> 기존 요소와 중복되는 요소는 에러없이 무시됨.
  ```

- Set 객체에는 자바스크립트의 모든 값을 요소로 저장할 수 있음.

### 요소 존재 여부 확인

- Set 객체에 특정 요소가 존재하는지 확인할 때는 `Set.prototype.has` 메서드를 사용함.

- `has` 메서드는 불리언 값을 반환함.

### 요소 삭제

- Set 객체의 특정 요소를 삭제할 때는 `Set.prototype.delete` 메서드를 사용함.

- `delete` 메서드는 불리언 값을 반환하는데, 이는 삭제 성공 여부를 나타냄.

- 사용 방법

  `Set객체.delete(삭제하려는 값);`

  - 즉, 삭제하려는 **요소값 자체**를 인수로 전달해야 함.

  - 인수로 전달한 값이 해당 Set 객체에 존재하지 않더라도, 아무런 에러 없이 그냥 무시됨.

### 요소 일괄 삭제

- Set 객체를 일괄 삭제할 때는 `Set.prototype.clear` 메서드를 사용함.

- `clear` 메서드는 언제나 `undefined`를 반환함.

### 요소 순회

- Set 객체를 순회할 때는 `Set.prototype.forEach` 메서드를 사용함.

  - 배열 고차 함수 `forEach`와 비슷하지만, 배열 고차 함수 `forEach`가 콜백 함수의 첫 번째 인수와 두 번째 인수로 각각 현재 순회 중인 요소와 현재 그 요소의 인덱스를 전달하는 것과 달리, `Set.prototype.forEach` 메서드는 콜백 함수의 첫 번째 인수와 두 번째 인수 모두 현재 순회 중인 요소를 전달받음. => 즉, 첫 번째 인수와 두 번째 인수는 늘 같음!

- Set 객체는 <b>이터러블</b>인바 아래와 같은 작업들도 가능함.

  - <for...of문>으로 순회

  - 스프레드 문법 사용

  - 배열 디스트럭처링 할당

### 집합 연산

1. 교집합

2. 합집합

3. 차집합

4. 부분 집합과 상위 집합

___
## Map

- 