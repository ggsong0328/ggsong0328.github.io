---
title: Create React App 설치
author: ggsong0328
date: 2024-02-28 12:30:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

## Node.js 설치하기

---

개발 환경을 준비하기 전에 설치 도구에 대한 정리가 필요하다.

JavaScript 패키지 관리 도구에는 NPM과 YARN이 있다.

Node Package Manager, 즉 NPM은 패키지를 관리해주는 프로그램이다.

Node.js 설치와 함께 NPM은 설치된다.

YARN은 페이스북에서 만든 패키지 관리 프로그램으로, NPM에 비해 캐싱, 보안, 신뢰성 등이 개선되었다.

Node.js 공식 웹 사이트에 접속해 원하는 버전으로 다운로드 하면 된다. (LTS - 완정화된 버전, Current - 최신 버전)

다운로드한 파일을 실행해 설치를 시작한다.

설치 도중 다음 화면에서는 [Automatically install the necessary tools]에 체크 표시를 하지 않고 [ Next ]를 클릭한다.

[ Finish ]를 눌러 설치를 완료한다.

설치가 제대로 되었는지 확인하는 방법으로는 명령 프롬프트(cmd)를 실행하고 **npm -v**를 입력한다.

그때 숫자가 나오면 성공적으로 Node.js와 NPM을 설치한 상태라고 보면 된다.

## Create React App 설치하기

---

React와 같은 라이브러리를 위해서 Create React App을 사용하면 개발 도구 설치가 아닌 코드에 집중할 수 있다!!

VSCode와 같은 개발 환경에서 커맨트 창을 열고 다음 명령을 실행한다.

```
npx create-react-app basic
```

빌드 도구 업데이트는 일반적으로 어렵고 시간이 많이 걸리는 작업입니다. Create React App의 새 버전이 출시되면 아래의 명령을 사용하여 쉽게 업그레이드할 수 있다.

```
npm install react-scripts@latest
```

## 샘플 웹앱 실행하기

---

지금까지 개발 환경을 구축했으니 드디어 코드를 작성해보자!

사용하는 프로그램은 Visual Studio Code이다!

Visual Studio Code의 장점 중 하나는 명령어로 컴퓨터를 제어할 수 있는 터미널 프로그램이 내장되어 있다는 것이다.

**View - TERMIINAL** 메뉴를 선택하면 터미널이 표시된다.

이제 앱을 한 번 실행시켜보자.

Create React App으로 개발 환경을 만들고 나면 그 다음에는 터미널에서 다음 명령어를 통해 앱을 실행 할 수 있다.

```
npm run start
```

그러면 자동으로 localhost:3000 경로의 웹 페이지가 열린다.

이러한 과정을 컴파일한다고 하고, 컴파일이란 어떤 언어의 코드 전체를 다른 언어로 바꿔주는 일련의 과정이다. 웹 개발에서의 컴파일은 개발 파일을 웹 용 파일 **HTML, CSS, Javascript**로 변경하는 것을 의미!

React에서의 컴파일은 JavaScript 파일을 통해 웹 용 파일로 변경한다.

터미널에 2개의 주소가 출려되는데, 이는 React 앱을 개발할 때 브라우저를 통해 개발 중인 앱을 확인할 수 있는 주소이다.

두 개의 URL중에서 어느 주소로 들어가도 무방!

앱의 실행을 멈추고 싶으면 터미널에서 Ctrl + C 단축키를 누르면 프로그램이 종료된다.

앱을 종료하고 나면 웹브라우저에서 새로 고침을 해도 앱이 실행되지 않는다.

다시 개발용 앱을 실행하고 싶으면 터미널에 npm run start, 혹은 npm start를 입력하면 자동으로 다시 웹 브라우저가 열리면서 앱이 실행된다.

## Javascript 코딩하기

---

이제 Create React App에서 제공하는 폴더를 수정하는 것을 출발점으로 삼아 개발을 시작해보자!

먼저 폴더 구조가 어떻게 되어있는지, 어디를 수정해야하 코딩을 할 수 있는지 알아보자!

크게 node_modules, src, 그리고 public이라는 폴더가 있다.

node_modules는 Node.js 폴더이고, public은 웹으로 보이는 폴더 그리고 src는 React 소스 폴더이다.

여기서 public이라는 폴더 안에는 index.html이 존재한다.

이 index.html은 Create React App을 실행하면 나오는 첫 화면이다!

```html
<!--public/index.html-->
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>basic :: React App</title>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```

이 html 파일은 Create React App의 기본 HTML이다. 컴파일하지 않고 로컬로 따로 연다면 빈 페이지가 표시된다.

manifest.json 파일은 사용자의 디바이스에 컴파일과 빌드를 할 때 사용되는 메타데이터를 제공한다.

```html
<link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
```

%PUBLIC_URL% 경로는 컴파일과 빌드가 되는 과정에서 public 폴더의 URL로 대체된다. public 폴더 내부의 파일만 HTML에서 참조할 수 있다.

예를 들어 '/favicon.ico' 또는 'favicon.ico' 경로과 다르게 '%PUBLIC_URL%/favicon.ico'는 사용자의 모든 경로에서 올바르게 작동한다.

이 HTML 파일에 웹 폰트, 메타 태그를 추가할 수도 있다. 또한 번들 스크립트를 <body> 태그에 배치할 수도 있다.

컴파일을 시작하려면 'npm run start' 또는 'yarn run start'를 실행하고, 빌드하려면 'npm run build' 또는 'yarn build'를 실행한다.

중요한 부분은 다음 코드이다.

```html
<div id="root"></div>
```

앞으로는 React를 통해 컴포넌트를 만들어 나갈 것이다. 그리고 그 컴포넌트들은 id가 root인 div 요소 안에 들어가게 Create React App이 정한 것이다.

물론 들어가는 위치는 변경이 가능하다!!

Create React App을 실행한 첫 화면에서 개발자 모드의 Elements 탭을 확인해 보자.

id가 root인 요소 안쪽에 React를 통해 만든 태그가 들어 있는 모습을 볼 수 있다.

id가 root인 이 태그 안쪽에 들어가는 컴포넌트들은 src, 즉 소스를 타나내는 디렉터리 안에 있는 파일들을 수정해서 만들 수 있다.

이제 앞으로 React 프로그래밍을 하게 되면 대부분 src 안에서 작업을 할거고, 여기서 엡의 집입점 역할을 하는 파일은 index.js 이다!

```javascript
// src/index.js

import React from "react";
// React의 전반적인 명령어를 사용하기 위해 React 패키지 로드
import ReactDOM from "react-dom/client";
// 화면 렌더링을 담당하는 ReactDOM 패키지 로드
import "./index/css";
// index.css 파일을 로드. 상대 경로를 사용
import App from "./App";
// App 컴포넌트 로드
import reportWebVitals from "./reportWebVitals";

const root = ReactDOM.createRoot(document.getElementById("root"));
// React 구성 요소를 표시하는 root를 참조

root.render(<App />);

reportWebVitals();
```

<React.StrictMode></React.StrictMode> 태그는 어플리케이션의 잠재적 문제를 알아내기 위한 도구이다. 하지만 생명주기 함수를 여러 번 실행하는 원인이 되므로 사용하지 않는다.

reportWebVital()은 앱의 성능을 축정하기 위해 로그로 확인할 수 있는 명령어이다.

```javascript
reportWebVitals(console.log);
```

개발에 용이하도록 index.css를 Reset CSS로 바꿔준다.

```css
/*src/index.css*/
body,
h1,
h2,
h3,
h4,
h5,
h6,
p,
ul,
ol,
table,
dl,
dd {
  margin: 0;
  padding: 0;
}
h1 {
  font-size: 16px;
}
a {
  text-decoration: none;
  color: #000;
}
ul,
ol {
  list-style: none;
}
img {
  max-width: 100%;
  vertical-align: top;
  border: none;
}
```

```javascript
// src/App.js
import React from "react";
import "./App.css";

class App extends React.Component {
  render() {
    return <div className="App">Hello React</div>;
  }
}

export default App;
// App 컴포넌트를 상위 컴포넌트에 전달하기 위해 export 구문을 사용
```
