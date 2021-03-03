# 21/02/27 수업 내용
### Intro

- DOM

  - DOM은 각 HTML 요소에 대한 정보를 지니고 있는 자바스크립트 객체이다.

- Virtual DOM

  - Virtual DOM은 가상의 DOM으로서, 브라우저에서 실제로 보여지는 DOM이 아니라 메모리에 가상으로 존재하는 DOM이며 속도가 빠름.

- 컴포넌트

  - 일종의 UI 조각

___
### 개발 환경 준비

- 터미널에서 `npx create-react-app begin-react` 입력하여 리액트 프로젝트 생성

- 오류 발생!
```
There might be a problem with the project dependency tree.
It is likely not a bug in Create React App, but something you need to fix locally.
 
The react-scripts package provided by Create React App requires a dependency:
 
  "webpack": "x.xx.x"
 
Don't try to install it manually: your package manager does it automatically.
However, a different version of webpack was detected higher up in the tree:
 
  /Users/moditt/node_modules/webpack (version: x.xx.x) 
 
Manually installing incompatible versions is known to cause hard-to-debug issues.
 
If you would prefer to ignore this check, add SKIP_PREFLIGHT_CHECK=true to an .env file in your project.
That will permanently disable this message but you might encounter other issues.
 
To fix the dependency tree, try following the steps below in the exact order:
 
  1. Delete package-lock.json (not package.json!) and/or yarn.lock in your project folder.
  2. Delete node_modules in your project folder.
  3. Remove "webpack" from dependencies and/or devDependencies in the package.json file in your project folder.
  4. Run npm install or yarn, depending on the package manager you use.
 
In most cases, this should be enough to fix the problem.
If this has not helped, there are a few other things you can try:
 
  5. If you used npm, install yarn (http://yarnpkg.com/) and repeat the above steps with it instead.
     This may help because npm has known issues with package hoisting which may get resolved in future versions.
 
  6. Check if /Users/moditt/node_modules/webpack is outside your project directory.
     For example, you might have accidentally installed something in your home folder.
 
  7. Try running npm ls webpack in your project folder.
     This will tell you which other package (apart from the expected react-scripts) installed webpack.
 
If nothing else helps, add SKIP_PREFLIGHT_CHECK=true to an .env file in your project.
That would permanently disable this preflight check in case you want to proceed anyway.
 
P.S. We know this message is long but please read the steps above :-) We hope you find them helpful!
```

  - 해결 방법

    - 위 안내 내용 중 7번까지 확인해봤지만 해결되지 않음.

    - 7번 아래의 안내(`If nothing else helps, add SKIP_PREFLIGHT_CHECK=true to an .env file in your project.`)에 따라 프로젝트 루트 디렉토리에 `.env`라는 이름의 파일을 생성한 후 `SKIP_PREFLIGHT_CHECK=true`를 써놓고 저장함.

    ![image](https://user-images.githubusercontent.com/54733637/109408659-d47b3400-79ce-11eb-9848-d3332c0f58b2.png)
##### 해결!

___
### 실습

- 컴포넌트는 두 가지 방법으로 만들 수 있음.

  1. 함수 형태로 만들기

  2. 클래스 형태로 만들기

- 실습에서는 함수 형태로 만들기로 함.

- JSX

  - JSX는 자바스크립트를 확장한 언어로, 출력하고 싶은 HTML 구조를 그대로 작성하면 되므로 코드를 직관적으로 작성하고 파악할 수 있음.

  - JSX를 사용하면 컴포넌트를 만들 때마다 `React.createElement()`를 호출하지 않고도 간단하게 컴포넌트를 만들 수 있음.

  - 문 끝에 세미콜론(`;`)은 붙여도 되고 안 붙여도 된다고 함.

    ![image](https://user-images.githubusercontent.com/54733637/109408897-2fae2600-79d1-11eb-8747-408c7b90348e.png)
    
  - JSX가 자바스크립트로 제대로 변환이 되려면 아래와 같이 몇 가지 문법을 준수해야 함.

    1) 태그는 <b>반드시 닫아주어야</b> 함. (`<img>` => X, `<img />` => O) 

    2) 두 개 이상의 태그는 꼭 하나의 태그로 <b>감싸져 있어야</b> 함.

      - 단순히 wrapping을 위해 불필요한 `<div>` 요소를 만들지 않고도, 아래와 같이 fragment를 사용하여 태그들을 묶을 수 있음. ([참고](https://ko.reactjs.org/docs/fragments.html#short-syntax))

        ```js
        return (
          <React.Fragment>
            <ChildA />
            <ChildB />
            <ChildC />
          </React.Fragment>
        );
        
        // 단축 문법
        return (
          <>
            <td>Hello</td>
            <td>World</td>
          </>
        );
        ```
        
        - 소괄호(`()`)는 사용하지 않아도 문법적으로 오류는 없지만 가독성을 위해 사용함.

  - JSX로 쓴 구문 내부에서 자바스크립트를 사용하고 싶으면 중괄호(`{}`)를 쓰고 그 안에 자바스크립트를 작성하면 됨.

    > JSX의 중괄호(`{}`) 안에는 유효한 모든 JavaScript 표현식을 넣을 수 있습니다. ([참고](https://ko.reactjs.org/docs/introducing-jsx.html#embedding-expressions-in-jsx))

  - JSX로 스타일과 클래스 설정하기

    ```js
    function App() {
      const name = 'react';
      const style = {
      backgroundColor: '#181818',
      color: `#09a2aa`,
      fontSize: 24,
      fontWeight: 700,
      padding: '1rem'
    };

      return (
        <div>
          <Hello />
          <div style={style}>{name}</div>
          <div className="gray-box"></div>
        </div>
      );
    }
    ```

    - 스타일 설정하는 방법

      - 객체를 만들어 주어야 함. (그냥 문자열로 넣어주면(`<div style="color: red">`) 동작 안함.)

        - 위와 같이 객체를 미리 만들어 놓고 그 객체를 가리키는 변수를 전달해줘도 되고, 아래와 같이 직접 객체를 전달해주는 것도 가능함.

          ```js
          <div style={{
            backgroundColor: '#181818',
            color: `#09a2aa`,
            fontSize: 24,
            fontWeight: 700,
            padding: '1rem'
          }}>
          ```
          
          - 중괄호가 두 번 쓰였는데, 겉에 중괄호는 자바스크립트를 작성하기 위한 중괄호, 안의 중괄호는 객체를 감싸는 중괄호임.

      - 객체를 만들 때, `background-color`와 같이 kebab case로 된 스타일 이름은 camel case로 바꿔줘야 함.

      - 스타일 프로퍼티의 값이 숫자일 경우(ex: `fontSize`) 단위를 생략하면 기본 단위는 `px`이 됨.

      - 단위를 따로 설정해주고 싶다면 문자열로 작성하면 됨. (ex: `'1rem'`)

    - 클래스 설정하는 방법

      - HTML에서는 클래스를 설정하려는 요소에 `class` 어트리뷰트를 사용하여 클래스를 지정하지만, JSX에서는 `className`을 사용함.

        > JSX는 HTML보다는 JavaScript에 가깝기 때문에, React DOM은 <u>HTML 어트리뷰트 이름 대신 **camelCase 프로퍼티 명명 규칙을 사용**</u>합니다.
        > 예를 들어, JSX에서 `class`는 `className`가 되고 `tabindex`는 `tabIndex`가 됩니다. ([참고](https://ko.reactjs.org/docs/introducing-jsx.html#specifying-attributes-with-jsx))

  - 주석 작성하는 방법

    - `{/* 내용 */}`

    - 태그 내에도 아래와 같이 주석을 작성할 수 있으며, 이 방법으로 작성한 주석은 화면에 나타나지 않음.

      ```js
      <Hello
        // self-closing 태그 내에 주석 작성하는 방법
      />
      ```
    
- `<noscript>` 요소

  ![image](https://user-images.githubusercontent.com/54733637/109408996-3721ff00-79d2-11eb-899f-c39c011f1672.png)
  
  - `index.html` 파일에 기본으로 작성되어 있는 내용 중 `<noscript>` 태그가 있길래 어떤 때 사용하는 태그인지 찾아봄.

  - `<noscript>` 요소는 브라우저에서 스크립트가 비활성화되어 있을 경우에 보여질 내용을 담는데, 스크립트를 지원하는 경우에는 표시되지 않음. ([참고](https://webdir.tistory.com/322))



