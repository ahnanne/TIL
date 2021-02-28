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