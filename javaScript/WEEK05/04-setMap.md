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

- Map 객체는 <b>키(key)와 값(value)의 쌍</b>으로 이루어진 컬렉션으로, 일반적인 객체와 유사하지만 몇 가지 차이점이 있음.

  1. 일반 객체와 달리 Map 객체에선 <b>객체를 포함한 모든 값</b>을 키로 사용할 수 있음. (cf. 일반 객체는 문자열 또는 심벌 값만 키로 사용할 수 있음.)

  2. 일반 객체와 달리 Map 객체는 언제나 <b>이터러블</b>임.

  3. 일반 객체의 경우 <b>요소 개수를 확인</b>할 때 `length` 프로퍼티를 이용하는 반면, Map 객체는 `size` 프로퍼티를 이용함.

### Map 객체 생성

- Map 객체는 Map 생성자 함수로 생성함.

  ```js
  const myMap = new Map();
  console.log(myMap); // Map(0) {}

  const myStrMap = new Map('hello');
  console.log(myStrMap); //TypeError: Iterator value h is not an entry object

  const myCuteMap = new Map([['a', 'Anne'], ['b', 'blue'], ['c', 'cute']]);
  console.log(myCuteMap);
  // Map(3) { 'a' => 'Anne', 'b' => 'blue', 'c' => 'cute' } 🧙‍♂️
  ```

  - Map 생성자 함수에는 이터러블을 인수로 전달하는데, 아무런 인수도 전달하지 않으면 빈 Map 객체가 생성됨.

  - 이터러블을 인수로 전달할 때, 이터러블은 키와 값의 쌍으로 이루어진 요소(`['키', '값']`)들로 구성되어야 함.

  - 중복된 키를 갖는 요소를 전달하면 가장 나중에 전달하는 요소로 덮어써짐. => Map 객체에는 중복된 키를 갖는 요소가 존재하지 않음.

### 요소 개수 확인

- Map 객체의 요소 개수를 확인할 때는 `Map.prototype.size` 프로퍼티를 사용함.

  - Set 객체의 경우와 마찬가지로, `size` 프로퍼티에는 setter 함수가 없으므로 재할당할 수 없음.

### 요소 추가

- Map 객체의 요소를 추가할 때는 `Map.prototype.set` 메서드를 사용함.

  ```js
  myCuteMap.set('d', 'Drake');
  console.log(myCuteMap);
  // Map(4) { 'a' => 'Anne', 'b' => 'blue', 'c' => 'cute', 'd' => 'Drake' } 😎
  ```

- `set` 메서드는 새로운 요소가 추가된 Map 객체를 반환함. => 메서드 체이닝 가능

### 요소 취득

- Map 객체에서 특정 요소를 취득할 때는 `Map.prototype.get` 메서드를 사용함.

- `get` 메서드의 인수로는 키를 전달하는데, 해당 키를 갖는 요소가 <u>존재하면</u> 그 요소를 반환하며 만약 그런 요소가 <u>존재하지 않으면</u> `undefined`를 반환함.

### 요소 존재 여부 확인

- Map 객체에서 특정 요소가 존재하는지 확인할 때는 `Map.prototype.has` 메서드를 사용함.

- `has` 메서드는 불리언 값을 반환함.

### 요소 삭제

- Map 객체에서 특정 요소를 삭제할 때는 `Map.prototype.delete` 메서드를 사용함.

- `delete` 메서드는 불리언 값을 반환하는데, 이는 삭제 성공 여부를 나타냄.

  ```js
  console.log(myCuteMap.delete('b')); // true
  console.log(myCuteMap); // Map(3) { 'a' => 'Anne', 'c' => 'cute', 'd' => 'Drake' }

  console.log(myCuteMap.delete('e')); // false -> 에러가 발생하지는 않음.
  ```

### 요소 일괄 삭제

- Map 객체에서 요소를 일괄 삭제할 때는 `Map.prototype.clear` 메서드를 사용함.

- `clear` 메서드는 언제나 `undefined`를 반환함.

### 요소 순회

- Map 객체를 순회할 때는 `Map.prototype.forEach` 메서드를 사용함.

  - 배열 고차 함수 `forEach`와 비슷하지만, 배열 고차 함수 `forEach`가 콜백 함수의 첫 번째 인수와 두 번째 인수로 각각 현재 순회 중인 요소와 현재 그 요소의 인덱스를 전달하는 것과 달리, `Map.prototype.forEach` 메서드는 콜백 함수의 첫 번째 인수와 두 번째 인수로 각각 현재 순회 중인 요소의 <b>값</b>과 현재 그 요소의 <b>키</b>를 전달받음.

- Map 객체는 <b>이터러블</b>인바 아래와 같은 작업들도 가능함.

  - <for...of문>으로 순회

  - 스프레드 문법 사용

  - 배열 디스트럭처링 할당
