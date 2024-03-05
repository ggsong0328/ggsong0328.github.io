---
title: Create React App을 사용한 React 2
author: ggsong0328
date: 2024-02-29 12:30:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

## React에서 jQuery 사용하기

---

jQuery는 JavaScript 라이브러리의 한 종류이다.

jQuery는 이벤트 처리, 애니메이션 등 JavaScript의 기능을 간단하고 빠르게 구현할 수 있도록 지원한다.

jQuery를 사용하기 위해선 cmd 창에서 프로젝트 경로로 이동한 후 [npm install jquery]를 입력하면 설치된다!

사용 예제:

```javascript
// src/App.js

import React, { Component } from "react";
import Jquery from "./Jquery";
import "./App.css";

class App extends Component {
  render() {
    return (
      <div className="container">
        <h1>React Example</h1>
        <Jquery />
      </div>
    );
  }
}

export default App;
```

```javascript
// src/Jquery.js

import React, { Component } from 'react';
import $ from 'jquery';

class Jquery extends Component {
  componentDidMount(){
    ${"#buttonId"}.on("click", () => {
      console.log($("#inputId").val());
    });
  }

  render(){
    let inputStyle={
      marginTop: 30,
      padding: "0px, 10px",
      lineHeight: "32px",
      border: "1px solid #ccc"
    }
    let buttonStyle={
      marginLeft: 6,
      marginTop: 30,
      fontSize: 14,
      backgroundColor: "#999",
      color: "#fff",
      border: "none",
      cursor: "pointer"
    };

    return(
      <div>
        <h2>This is jQuery.</h2>
        <input id="inputId" name="inputName", style={inputStyle} />
        <button id="buttonId" style={buttonStyle}>jQuery Button</button>
      </div>
    );
  }
}

export default Jquery;
```

## state 정의하기

---

```javascript
// src/App.js

import React, { Component } from "react";
import SetState from "./SetState";
import "./App.css";

class App extends Component {
  render() {
    return (
      <div className="container">
        <h1>React Example</h1>
        <SetState />
      </div>
    );
  }
}

export default App;
```

```javascript
// src/SetState.js

import React, { Component } from "react";

class SetState extends Component {
  constructor() {
    super();

    this.state = {
      comment: "Original State"
    };
  }

  modifyComment = () => {
    this.setState({
      comment: "Change State"
    });
  };

  render() {
    let buttonStyle = {
      marginTop: 20,
      padding: 10,
      fontSize: 14,
      backgroundColor: "#999",
      color: "#fff",
      border: "none",
      cursor: "pointer"
    };

    return (
      <div>
        <p>{this.state.comment}</p>
        <button onClick={this.modifyComment} style={buttonStyle}>
          Modify Comment
        </button>
      </div>
    );
  }
}

export default SetState;
```

## Fragment 이해하기

---

컴포넌트에서 여러 태그를 반환하려 할 때, 불필요한 HTML 태그로 전체를 둘러싸지 않으면 오류가 생긴다.

이럴 때에는 <Fragments> 태그를 사용하면, 불필요한 HTML 태그 없이도 작동 가능하다!

```javascript
// src/App.js

import React, { Component } from "react";
import Fragments from "./Fragments";
import "./App.css";
class App extends Component {
  render() {
    return (
      <div className="container">
        <h1>React Example</h1>
        <Fragments />
      </div>
    );
  }
}
export default App;
```

```javascript
import React, { Component, Fragment } from "react";
class Fragments extends Component {
  render() {
    return (
      <Fragment>
        <p>P Tag</p>
        <p>SPAN Tag</p>
      </Fragment>
    );
  }
}
export default Fragments;
```
