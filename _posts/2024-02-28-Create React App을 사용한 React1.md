---
title: Create React App을 사용한 React
author: ggsong0328
date: 2024-02-28 18:30:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

## 기본 구조 이해하기

---

```javascript
// src/index.js

import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<App />);

reportWebVitals();
```

```css
/*src/App.css*/

.container {
  padding: 10px;
}

.container h1 {
  font-size: 25px;
  font-weight: normal;
}

.container h2 {
  margin-top: 16px;
  font-size: 16px;
  font-weight: normal;
}

.container p {
  margin-top: 16px;
  font-weight: normal;
}
```

```javascript
// src/App.js

import React, { Component } from "react";
// Component를 import 함으로서 App extends React.Component 대신 App extends Component 이렇게 써도 된다.
import "./App.css";

class App extends Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <div className="container">
        <h1>React Example</h1>
        <p>HTML 적용하기</p>
      </div>
    );
  }
}

export default App;
```

## React 컴포넌트 이해하기

---

```javascript
// src/App.js

import React, { Component } from "react";
import ImportComponent from "./ImportComponent";
import "./App.css";

class App extends Component {
  render() {
    return (
      <div className="container">
        <h1>React Example</h1>
        <ImportComponent />
      </div>
    );
  }
}

export default App;
```

```javascript
// src/ImportComponent.js

import React, { Component } from "react";

class ImportComponent extends Component {
  render() {
    return <h2>This is Imported Component</h2>;
  }
}

export default ImportComponent;
```

## 생명주기 함수 이해하기

---

1단계:

```javascript
// src/App.js

import React, { Component } from "react";
import LifeCycle from "./LifeCycle";
import "./App.css";

class App extends Component {
  render() {
    return (
      <div className="container">
        <h1>React Example</h1>
        <LifeCycle />
      </div>
    );
  }
}

export default App;
```

```javascript
// src/LifeCycle.js

import React, { Component } from "react";

class LifeCycle extends Component {
  render() {
    console.log("3.render()");

    return <h2>This is Render Function</h2>;
  }
}

export default LifeCycle;
```

2단계:

```javascript
// src/LifeCycle.js

import React, { Component } from "react";

class LifeCycle extends Component {
  constructor(props) {
    super(props);
    console.log("1. constructor()");
  }

  render() {
    console.log("3. render()");

    return <h2>This is Render Function.</h2>;
  }
}

export default LifeCycle;
```

3단계:

```javascript
// src/App.js

import React, { Component } from "react";
import LifeCycle from "./LifeCycle";
import "./App.css";

class App extends Component {
  render() {
    return (
      <div className="container">
        <h1>React Example</h1>
        <LifeCycle propValue="fromApp" />
      </div>
    );
  }
}

export default App;
```

```javascript
// src/LifeCycle.js

import React, { Component } from 'react';

class LifeCycle extends Component {
  constructor(props){
    super(props);
    this.state = {};
    console.log("1. constructor()");
    console.log(props);
  }

  static getDerivedStateFromProps(props, state){
    console.log("2. getDerivedStateFromProps(), " + props.propValue);
    console.log(props);
    console.log(state);
    return ();
  }

  render(){
    console.log("3.render()");

    return(
      <h2>This is Render Function.</h2>
    );
  }
}

export default LifeCycle;
```

4단계:

```javascript
// src/LifeCycle.js

import React, { Component } from 'react';

class LifeCycle extends Component {
  constructor(props){
    super(props);
    this.state = {};
    console.log("1. constructor()");
    console.log(props);
  }

  static getDerivedStateFromProps(props, state){
    console.log("2. getDerivedStateFromProps(), " + props.propValue);
    return (
      {tempState: props.propValue};
    );
  }

  componentDidMount(){
    console.log("4. componentDidMount()");
    console.log("5. tempState : " + this.state.tempState);
    console.log(this.state);
  }

  render(){
    console.log("3. render()");

    return(
      <h2>This is Render Function.</h2>
    );
  }
}

export default LifeCycle;
```

5단계:

```javascript
// src/LifeCycle.js

import React, { Component } from "react";

class LifeCycle extends Component {
  constructor(props) {
    super(props);
    this.state = {};
    console.log("1. constructor()");
    console.log(props);
  }

  static getDerivedFromProps(props, state) {
    console.log("2. getDerivedStateFromProps(). " + props.propsValue);
    return { tempState1: props.propsValue };
  }

  componentDidMount() {
    console.log("4. componentDidMount()");
    console.log("5. tempState1 : " + this.state.tempState1);
    this.setState({ tempState2: true });
  }

  shouldComponentUpdate(props, state) {
    console.log("6. shouldComponentUpdate(), tempState : " + state.tempState2);
    return state.tempState2;
  }

  render() {
    console.log("3. render()");

    return <h2>This is Render Function</h2>;
  }
}

export default LifeCycle;
```

## React에서 jQuery 사용하기

---

jQuery는 JavaScript 라이브러리의 한 종류이다.

jQuery는 이벤트 처리, 애니메이션 등 JavaScript의 기능을 간단하고 빠르게 구현할 수 있도록 지원한다.

jQuery를 사용하기 위해선 cmd 창에서 프로젝트 경로로 이동한 후 [npm install jQuery]를 입력하면 설치된다!
