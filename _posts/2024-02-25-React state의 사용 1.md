---
title: React state의 사용 1
author: ggsong0328
date: 2024-02-25 10:30:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

## state 사용하기

---

props를 상위 컴포넌트에서 하위 컴포넌트로 데이터를 전달할 때 사용했다면, state는 하나의 컴포넌트 안에서 전역 변수처럼 사용한다.

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class State extends React.Component {
  constructor(props) {
    super(props);

    // console.log(this.props.program); // React
    // console.log(props.program); // React

    this.state = {
      stateString: props.program,
      stateVersion: "18.2.0"
    };
  }

  render() {
    // console.log(this.props.program); // React

    return (
      <div>
        {this.state.stateString} {this.state.stateVersion}
      </div>
    );
  }
}

class App extends React.Component {
  render() {
    let h1Style = {
      fontWeight: "normal"
    };

    return (
      <div>
        <h1 style={h1Style}>React Example</h1>
        <State program="React" />
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<App />);
```

```javascript
this.state = {
  stateString: props.program,
  stateVersion: "18.2.0"
};
```

가장 먼저 실행되는 생성자 함수 constructor 안에서 state의 초깃값을 정의해야 한다. stateString state에는 props 값을 저장하고 stateVersion state에는 문자 '18.2.0'을 저장한다.

```javascript
{
  this.state.stateString;
}
{
  this.state.stateVersion;
}
```

this.state.변수명 문법으로 state에 접근합니다. state 값을 화면에 그대로 표시합니다.

## setState() 함수 사용하기

---

this.state.변수명 = 값 방식으로 state를 직접 변경하면 render() 함수를 호출하기 않으므로 화면에 보이는 state 값은 바뀌기 전 상태로 남게 됩니다.

setState() 함수로 state를 변경해야 render() 함수를 호출해 변경된 값을 화면에 보여줄 수 있습니다.

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class State extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      stateString: "React"
    };
  }

  // stateChange(flag){
  stateChange = (flag) => {
    if (flag === "direct") this.state.stateString = "React 18.2.0";
    if (flag === "setstate") this.setState({ stateString: "React 18.2.0" });
  };

  render() {
    let buttonStyle = {
      marginRight: 5,
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
        <button onClick={() => this.stateChange("direct")} style={buttonStyle}>
          state 직접 변경
        </button>
        <button
          onClick={() => this.stateChange("setstate")}
          style={buttonStyle}
        >
          set State() 함수로 변경
        </button>
        <p>stateString : {this.state.stateString}</p>
      </div>
    );
  }
}

class App extends React.Component {
  render() {
    let h1Style = {
      fontWeight: "normal"
    };

    return (
      <div>
        <h1 style={h1Style}>React Example</h1>
        <State />
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<App />);
```

```javascript
if (flag === "direct") this.state.stateString = "React 17.0.2";
```

[state 직접 변경] 버튼을 눌렀을 때 this.state.변수명 = 값 문법으로 state를 직접 변경하려고 한다.

이때 stateString 값은 "React 18.2.0"으로 변경되지만 render() 함수를 호출하지 않으므로 화면에는 이전 값인 "React"로 표시된다.

```javascript
if(flag === "setState") this.setState(stateString: "React 17.0.2");
```

[setState() 함수로 변경] 버튼을 눌렀을 때 setState() 함수로 state를 변경한다. 이때 stateString 값은 "React 18.2.0"으로 변경되고 render() 함수를 다시 호출해 화면에는 변경된 값으로 표시된다.

## state를 직접 변경한 후 forceUpdate() 함수 사용하기

---

this.state.변수명 = 값과 같이 직접 state를 변경하면 render() 함수를 호출하지 않으므로 화면에 보이는 state 값은 바뀌기 전 상태로 남게 된다.

이때 forceUpdate() 함수로 화면을 새로 고침하면, render() 함수를 호출해 변경된 값을 화면에 보여줄 수 있다.

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class State extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      stateString: "React"
    };
  }

  // stateChange(){
  stateChange = () => {
    this.state.stateString = "React 18.2.0";
    this.forceUpdate();
  };

  render() {
    let buttonStyle = {
      marginRight: 5,
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
        <button onClick={() => this.stateChange()} style={buttonStyle}>
          state 직접 변경
        </button>
        <p>stateString : {this.state.stateString}</p>
      </div>
    );
  }
}

class App extends React.Component {
  render() {
    let h1Style = {
      fontWeight: "normal"
    };

    return (
      <div>
        <h1 style={h1Style}>React Example</h1>
        <State />
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<App />);
```

```javascript
stateString: {
  this.state.stateString;
}
```

state인 stateString의 초깃값으로 "React" 문자열을 저장했다. constructor() 함수가 실행되고 render() 함수에서 화면을 그리기 때문에 {this.state.stateString}은 "React"로 표시된다.

```javascript
this.state.stateString = "React 17.0.2";
```

[state 직접 변경] 버튼을 눌렀을 때 this.state.변수명 = 값 문법으로 state를 직접 변경한다. 이때 stateString 값은 "React 18.2.0"으로 변경된다.

```javascript
this.forceUpdate();
```

forceUpdate() 함수는 화면을 강제로 새로 고침하기 때문에 render() 함수를 다시 실행시켜 화면에 변경된 state 값을 표시할 수 있다.
