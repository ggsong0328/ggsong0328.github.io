---
title: Create React App을 사용한 React 3
author: ggsong0328
date: 2024-03-01 12:30:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

## map() 함수로 태그 반환하기

---

map() 함수를 사용하면 반복해서 출력해야 하는 태그들을 배열에 넣어두고 관리할 수 있다.

1단계:

```javascript
// js/App.js

import React, { Component } from "react";
import ReturnMap from "./ReturnMap";
import "./App.css";

class App extends Component {
  render() {
    return (
      <div className="container">
        <h1>React Example</h1>
        <ReturnMap />
      </div>
    );
  }
}

export default App;
```

```javascript
// src/ReturnMap.js

class ReturnMap extends Component {
  render(){
    let ulStyle={
      marginTop: 15
    };
    let liStyle={
      lineHeight: 1.8
    };
    let forArray=[
      <li key="1" style={liStyle}>React</li>
      <li key="2" style={liStyle}>React</li>
      <li key="3" style={liStyle}>React</li>
    ];

    return (
      <ul style={ulStyle}>
        {forArray}
      </ul>;
    )
  }
}

export default ReturnMap;
```

2단계:

```javascript
// src/ReturnMap.js

import React, { Component } from 'react';

class ReturnMap extends Component {
  render(){
    let ulStyle={
      marginTop: 15
    };

    let liStyle={
      lineHeight: 1.8
    };
    let forArray=[
      <li key="1" style={liStyle}>React</li>
      <li key="2" style={liStyle}>18.2.0</li>
      <li key="3" style={liStyle}>ArrayMap</li>
    ];
    let forNewArray = [];

    for(let i = 0; i < forArray.length; i++){
      forNewArray.push(forArray[i]);
    }

    return(
      <ul style={ulStyle}>
        {forNewArray}
      </ul>
    );
  }
}

export default ReturnMap;
```

3단계:

```javascript
// src/ReturnMap.js

import React, { Component } from 'react';

class ReturnMap extends Component {
  render(){
    let ulStyle={
      marginTop: 15
    };
    let liStyle={
      lineHeight: 1.8
    };
    let forEachArray=[
      <li key="1" style={liStyle}>React</li>
      <li key="2" style={liStyle}>18.2.0</li>
      <li key="3" style={liStyle}>Array Map</li>
    ];
    let forEachArray=[];

    forEachArray.forEach(result => {
      forEachNewArray.push(result);
    });

    return (
      <ul style={ulStyle}>
        {forEachNewArray}
      </ul>
    );
  }
}

export default ReturnMap;
```

4단계:

```javascript
// src/ReturnMap.js

import React, { Component } from 'react';

class ReturnMap extends Component {
  render(){
    let ulStyle={
      marginTop: 15
    };
    let liStyle={
      lineHeight: 1.8
    };
    let mapArray=[
      <li key="1" style={liStyle}>React</li>
      <li key="2" style={liStyle}>18.2.0</li>
      <li key="3" style={liStyle}>Array Map</li>
    ];
    let mapNewArray = mapArray.map(arrayVal => arrayVal);

    return (
      <ul style={ulStyle}>
        {mapNewArray}
      </ul>
    );
  }
}

export default ReturnMap;
```

5단계:

```javascript
// src/ReturnMap.js

import React, { Component } from 'react';

class ReturnMap extends Component {
  render(){
    let ulStyle={
      marginTop: 15
    };
    let liStyle={
      lineHeight: 1.8
    };
    let elementArray=[
      <li key="1" style={liStyle}>React</li>
      <li key="2" style={liStyle}>18.2.0</li>
      <li key="3" style={liStyle}>Array Map</li>
    ];

    return (
      <ul style={ulStyle}>
        {elementArray.map(arrayVal => arrayVal)}
      </ul>
    );
  }
}

export default ReturnMap;
```

## 컴포넌트 매핑 이해하기

---

1단계:

```javascript
// js/App.js

import React, { Component } from "react";
import DataComponent from "./DataComponent";
import "./App.css";

class App extends Component {
  render() {
    return (
      <div className="container">
        <h1>React Component</h1>
        <DataComponent />
      </div>
    );
  }
}

export default App;
```

```javascript
// src/DataComponent

import React, { Component } from "react";

class DataComponent extends Component {
  render() {
    let ulStyle = {
      marginTop: 15
    };
    let liStyle = {
      lineHeight: 1.8
    };

    return (
      <ul style={ulStyle}>
        <li style={liStyle}>member1</li>
        <li style={liStyle}>member2</li>
        <li style={liStyle}>member3</li>
      </ul>
    );
  }
}

export default DataComponent;
```

2단계:

```javascript
// js/App.js

import React, { Component } from "react";
import DataComponent from "./DataComponent";
import "./App.css";
class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      loginData: [
        { name: "member1", age: 21 },
        { name: "member2", age: 22 },
        { name: "member3", age: 23 }
      ]
    };
  }
  render() {
    return (
      <div className="container">
        <h1>React Example</h1>
        <DataComponent loginData={this.state.loginData} />
      </div>
    );
  }
}
export default App;
```

```javascript
// src/DataComponent.js

import React, { Component } from "react";

class DataComponent extends Component {
  constructor(props) {
    super(props);
    this.state = { loginData: props.loginData };
  }

  render() {
    let ulStyle = {
      marginTop: 15
    };
    let liStyle = {
      lineHeight: 1.8
    };

    let data = this.state.loginData;
    let dataList = data.map((d, i) => (
      <li key={i + 1} style={liStyle}>
        {d.name}, {d.age}
      </li>
    ));

    return <ul style={ulStyle}>{dataList}</ul>;
  }
}

export default DataComponent;
```
