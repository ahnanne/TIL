# 클래스
## 들어가기 전..

- 클래스(class)는 객체 생성 메커니즘 중 하나로, ES6에 새롭게 도입되었음.

- 클래스를 사용하는 이유 : 인스턴스를 생성하기 위함. => 따라서 반드시 `new` 연산자와 함께 호출해야 함.

- 클래스도 생성자 함수와 마찬가지로 프로토타입 기반의 인스턴스를 생성하지만, 생성자 함수보다 더 엄격하며 추가적인 기능들도 제공함.

  1. `new` 연산자

    - **생성자 함수**의 경우 `new` 연산자 없이 호출하면 일반 함수로서 호출됨.

    - **클래스**는 내부 메서드 `[[Call]]`이 없기 때문에 `new` 연산자 없이 호출할 경우 에러가 발생함.

  2. `extends`, `super` 키워드

    - 생성자 함수와는 달리 클래스에는 `extends`, `super` 키워드가 있음.

  3. 호이스팅

    - **생성자 함수**는 함수 호이스팅 및 변수 호이스팅 발생함.

    - **클래스**는 호이스팅이 발생하지 않는 것<u>처럼</u> 동작함.

  4. strict mode

    - 생성자 함수와 달리 클래스는 암묵적으로 strict mode가 지정되어 실행되며, 해제가 불가능함.

  5. 프로퍼티 어트리뷰트 `[[Enumerable]]`
    - 클래스의 모든 메서드들(`constructor`, 프로토타입 메서드, 정적 메서드)은 `[[Enumerable]]`의 값이 `false`인바 <u>열거되지 않음</u>.

___
## 클래스 정의

- 클래스는 `class` 키워드를 사용하여 정의함.

- 클래스 이름은 생성자 함수의 이름을 지을 때와 마찬가지로, 일반적으로 **파스칼 케이스**를 사용함.

- 표현식으로도 클래스를 정의할 수는 있긴 하나 일반적이지는 않음.

  - 클래스는 함수이므로 일급 객체이며, 따라서 값으로 사용할 수 있음.

- 클래스 몸체에는 다음의 메서드들만 정의할 수 있음. (0개 이상)

  - `constructor` (생성자로서, `constructor`로 정의)

  - 프로토타입 메서드 (그냥 정의)

  - 정적 메서드 (`static` 키워드로 정의)

  > cf.) 인스턴스 메서드를 만드는 방식은 생성자 함수의 경우와 동일하나, 굳이 인스턴스 메서드를 만들어야 하는 경우는 많지 않음.

___
## 클래스 호이스팅

- 모든 선언문은 런타임 이전에 먼저 실행되므로, 클래스도 런타임 이전에 함수 객체를 생성하기는 하지만, 클래스 정의 이전에 참조는 할 수 없음. => TDZ

___
## 메서드

- 클래스에서 정의한 메서드의 특징

  1. 메서드 축약 표현(ES6) 사용

  2. 메서드 축약 표현으로 정의되었으므로 non-constructor인바, `new` 연산자와 함께 호출할 수 없음.

### `constructor`

- `constructor`는 인스턴스를 생성하고 초기화하기 위한 특수한 메서드

  - `constructor`는 이름을 변경할 수 없음.

- `constructor`는 클래스 내에 최대 1개만 존재할 수 있음.

- `constructor`는 생략 가능함.

  - 생략할 경우에는 빈 `constructor`가 암묵적으로 정의되고, 이렇게 비어있는 `constructor`에 의해 **빈 객체**가 생성됨.

  - 인스턴스를 초기화하려는 경우에는 `constructor`를 생략할 수 없음.

- `constructor`는 별도의 반환문을 갖지 않아야 함. (그 이유는 생성자 함수의 경우와 마찬가지)

### 프로토타입 메서드

- 클래스 몸체에서 정의한 메서드는 기본적으로 프로토타입 메서드가 됨.

  - cf.) 생성자 함수의 경우, 프로토타입 메서드를 정의하려면 해당 생성자 함수의 `prototype` 프로퍼티에 메서드를 추가해줘야 함.

### 정적 메서드

- 클래스 몸체에서 `static` 키워드를 붙여 정의한 메서드는 정적 메서드가 됨.

  - cf.) 생성자 함수의 경우, 해당 생성자 함수에 직접 추가한 메서드가 정적 메서드가 됨.

- 정적 메서드는 클래스에 바인딩된 메서드가 됨.

___
## 클래스의 인스턴스 생성 과정

```js
class Test {
  // 생성자
  constructor(dateStr) {
    // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
    console.log(this); // Test {}
    console.log(Object.getPrototypeOf(this) === Test.prototype); // true

    // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
    this.date = new Date(dateStr);

    // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
  }
}

const test = new Test('2021-03-15');
```

- `Object.getPrototypeOf()`

  - 지정된 객체의 프로토타입의 값(내부 슬롯 `[[Prototype]]`의 값)을 반환함. ([MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf))

  - cf.) 대부분의 브라우저에서 지원하고 있는 접근자 프로퍼티인 `__proto__`로도 위의 값을 확인할 수 있지만, `__proto__`는 deprecated 됐으므로 `Object.getPrototypeOf()`을 사용할 것을 권장함.

    - [참고1](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/proto), [참고2](https://ko.javascript.info/prototype-methods)

___
## 프로퍼티

- 인스턴스 프로퍼티

  - 인스턴스 프로퍼티는 `constructor` 내부에서 정의해야 함.

  - 인스턴스 프로퍼티는 언제나 public함.

    - cf.) private 필드 정의 제안

- **클래스 필드 정의 제안(Class field declarations)**

  - 클래스 기반 객체지향 언어에서 클래스 필드란 **클래스가 생성할 인스턴스의 프로퍼티**를 가리킴.

  - 앞서 살펴보았듯이, 자바스크립트의 클래스 몸체에서는 원래는 **메서드**만을 선언할 수 있으며, **프로퍼티(=클래스 필드)**를 선언할 경우에는 SyntaxError가 발생함.

  - 하지만 최근, 최신 브라우저나 최신 Node.js에서 클래스 필드 정의를 지원하면서, 클래스 몸체에서도 인스턴스의 프로퍼티를 정의할 수 있게 됨.

  - 이 방식으로 인스턴스 메서드를 정의하는 것도 가능함. (함수는 일급 객체인바 함수를 클래스 필드에 할당함으로써 정의) => 권장하지 않음.

    - 모든 클래스 필드는 인스턴스 프로퍼티가 됨.

  - 이처럼 클래스 필드 정의를 사용하는 경우에는 해당 클래스 필드에 `this` 바인딩을 할 수 없음.

    - `this`는 클래스 몸체에서 정의된 메서드(`constructor`, 프로토타입 메서드, 정적 메서드) 내에서만 유효하기 때문

  - 따라서 인스턴스를 생성할 때, 매개변수를 통해 전달 받은 외부의 값으로 클래스 필드를 초기화할 필요가 있다면 `constructor`에서 클래스 필드를 초기화해줘야 함.

    - 즉, 이럴 경우 어차피 `constructor`를 써야 하기 때문에, 굳이 클래스 필드 정의를 사용할 필요가 없음.

  - 결론 : <u>클래스 필드를 초기화할 필요가 없는 경우</u>에는 `constructor`를 쓰는 기존 방식과 클래스 필드 정의 방식 모두 사용할 수 있음.

- **private 필드 정의 제안**

  - private 필드 정의를 사용하면 클래스 외부에서 private 필드에 직접 접근하는 것을 방지할 수 있음.

  - 사용 방법
  
    - private 필드의 선두에 `#`를 붙여주면 private 필드를 정의할 수 있으며, 이를 참조할 때도 선두에 `#`를 붙여주면 됨.

  - 주의할 점

    - private 필드는 반드시 클래스 몸체에 정의해야 하며, `constructor` 내부에 정의할 경우 에러 발생함.

  - 예제

    ```js
    // 기본적으로 클래스 필드는 public함.
    // (즉, 외부에서 클래스 필드를 참조할 수 있음.)
    class Test {
      constructor(favColor) {
        this.color = favColor;
      }
    }

    const test = new Test('orange');

    console.log(test.color); // orange
    ```
    ```js
    // private 필드 정의 사용
    class Test {
      #color = '';

      constructor(favColor) {
        this.#color = favColor;
        this.publicProp = 'Kim';
      }
    }

    const test = new Test('orange');

    console.log(test); // Test { publicProp: 'Kim' }
    // private 필드 정의를 사용하여 정의한 클래스 필드는
    // 외부에 공개되지 않음. => 외부에서 참조할 수 없음!
    ```

- **static 필드 정의 제안(public class fields syntax)**

  - static 필드 정의를 사용하면, `static` 키워드를 사용하여 **정적 메서드**를 정의하는 것처럼, `static` 키워드를 사용하여 **정적 프로퍼티**도 정의할 수 있음.

    - 정적 프로퍼티 : 클래스에 바인딩된 프로퍼티

  - 예제

    ```js
    class Test {
      static classProp = 'tester!';

      constructor(favColor) {
        this.color = favColor;
        this.publicProp = 'Kim';
      }

      static shout() {
        console.log(this.classProp);
      }
    }

    console.log(Test.classProp); // tester!
    Test.shout(); // tester!
    ```

___
## 상속에 의한 클래스 확장

- 

___
## 개념 정리..

- 클래스(class)란?

  - 인스턴스를 생성하기 위한 생성자 함수

- 정적 메서드(static method)란?

  - 인스턴스를 생성하지 않아도 호출할 수 있는 메서드

- 클래스 필드(class field)란?

  - 클래스 기반 객체 지향 프로그래밍 언어에서, 클래스가 생성할 인스턴스의 프로퍼티를 클래스 필드라고 함.

