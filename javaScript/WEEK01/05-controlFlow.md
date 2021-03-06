# 제어문
## 들어가기 전..

- 제어문이란, 코드의 순차적인 실행 흐름(일반적으로 위에서 아래로 실행)을 특정한 조건에 따라 통제하는 명령을 의미함.

- 제어문은 직관적인 코드의 흐름을 혼란스럽게 하여 가독성을 해친다는 문제가 있음.

___
## 블록문(block statement/compound statement)

- 블록문이란, 0개 이상의 문을 중괄호`{}`로 묶은 것을 의미함.

- 자바스크립트는 블록문을 하나의 실행 단위로 취급함.

- 블록문은 일반적으로 제어문이나 함수를 정의할 때 사용함.

- 블록문은 언제나 문의 종료를 의미하는 <b>자체 종결성(self closing)</b>을 갖기 때문에, 블록문의 끝에는 세미콜론`;`을 붙이지 않음.

___
## 조건문(conditional statement)

- 조건문은 주어진 조건식의 평가 결과(`true`/`false`)에 따라 블록문의 실행을 결정함.

  - 조건식

    - 불리언 값으로 평가될 수 있는 표현식 => 즉, 불리언 값을 반환하게 되는 표현식!

    - 조건식은 조건에 따라 실행이 달라지게 할 때(분기) 쓰임.

- 자바스크립트에는 두 가지 조건문이 있음.

  1. <if...else문>

    - 대부분의 경우 <if...else문>은 삼항 조건 연산자로 바꿔 쓸 수 있음.

    - 코드 블록 내의 문이 하나만 있는 경우에는 중괄호 생략 가능함.

  2. <switch문>

    ```js
    switch (표현식) {
      case 표현식1:
        switch 문의 표현식과 표현식1이 일치하면 실행될 문;
        break;
      case 표현식2:
        switch 문의 표현식과 표현식2가 일치하면 실행될 문;
        break;
      default:
        switch 문의 표현식과 일치하는 표현식을 갖는 case 문이 없을 때 실행될 문;
    }
    ```
    - <switch문>의 표현식은 불리언 값보다는 문자열이나 숫자 값인 경우가 많음.

    - <switch문>은 이름 그대로 다양한 상황(case)에 따라 실행할 코드 블록을 결정할 때 사용함.
___
## 반복문(loop statement)

  - 자바스크립트에는 세 가지 반복문이 있음.

    1. <for문>

      - 조건식이 거짓으로 평가될 때까지 코드 블록을 반복 실행함.

      - <for문>의 형태

        ```js
        for (변수 선언문 또는 할당문; 조건식; 증감식) {
          조건식이 참인 경우 반복 실행될 문;
        }
        
        // 예제
        for (var i = 0; i < 2; i++) {
	        console.log(i);
        }
        // 0
        // 1
        ```
        
        - 변수 선언문은 단 한번만 실행됨.

    2. <while문>

      - <for문>은 반복 횟수가 명확할 때 주로 사용하는 반면, <while문>은 반복 횟수가 명확하지 않을 때 주로 사용함.

    3. <do...while문>

       ```js
       do {
        console.log(count);
        count++;
       } while (count < 3); // 0 1 2
       ```

      - <do...while문>은 코드 블록을 먼저 실행하고 조건식을 평가함. => 즉, 코드 블록은 무조건 한 번 이상 실행됨.

___
## break문

- <break문>은 레이블 문, 반복문, <switch문>의 코드 블록을 탈출함.

  - 이러한 경우 외에 <break문>을 사용할 경우 SyntaxError 발생

___
## continue문

- <continue문>은 반복문의 코드 블록 실행을 현 지점에서 중단하고, 반복문의 <b>증감식</b>으로 실행 흐름을 이동시킴.

- 가독성 측면에서 사용함.

  - 어떤 <if문>을 쓰면서 <continue문>을 사용하지 않으면 <if문> 내에 코드들을 작성해야 하는데, 만약 그 코드가 길다면 들여쓰기가 한 단계 더 깊어지게 되고 가독성이 나빠짐. 그래서 <continue문>으로 한 번 끊어주고 가는 것임.
