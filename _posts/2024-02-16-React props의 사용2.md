---
title: React props의 사용 2
author: ggsong0328
date: 2024-02-16 10:30:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

## props를 객체형으로 사용하기

---

props 값을 객체로 하위 컴포넌트에 전달할 경우, 자료형을 object로 선언한다.

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class Props extends React.Component {
  render() {
    // console.log(this.props); // propsValue: {program: "React", version: "18.2.0"}

    // let propsValue=this.props.propsValue;
    let { propsValue } = this.props;
    // console.log(propsValue); // {program: "React", version: "18.2.0"}

    return (
      <div>
        <p>{JSON.stringify(propsValue)}</p>
        <p>{propsValue.program}</p>
        <p>{propsValue.version}</p>
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
        {/* <Props program="React" version="18.2.0" /> */}
        <Props propsValue={{ program: "React", version: "18.2.0" }} />
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<App />);
```

```javascript
let { propsValue } = this.props;
```

함수 내에서 변수를 선언해 props로 전달된 값을 할당한다.

```javascript
{
  JSON.stringify(propsValue);
}
```

object 객체의 key와 value 값들을 화면에 출력한다.

## props를 필수 값으로 사용하기

---

props의 자료형을 선언할 때 prop-types를 사용한다.

자료형 설정 대신 isRequired를 조건에 추가하면, props 값이 없는 경우 경고 메시지를 발생할 수 있다.

CDN 방식:

```javascript
<script
  src="https://cdnjs.cloudflare.com/ajax/libs/prop-types/15.8.1/prop-types.min.js"
  crossorigin
></script>
```

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class Props extends React.Component {
  render() {
    let { program, version } = this.props;
    // console.log(program, version); // undefined "18.2.0"

    return (
      <div>
        {program} {version}
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
        <Props version="18.2.0" />
      </div>
    );
  }
}

Props.propsTypes = {
  program: PropTypes.isRequired
};

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<App />);
```

```javascript
Props.propsTypes = {
  program: PropTypes.isRequired
};
```

program이라는 props 값을 필수 값으로 지정한다. 하지만 상위 컴포넌트에서 program이라는 props를 전달하지 않았기 때문에 경고 메시지가 발생한다.

## props를 기본 값으로 사용하기

---

props의 기본 값은 부모 컴포넌트에서 값이 넘어 오지 않았을 때 사용한다. defaultProps라는 문법을 사용한다.

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class Props extends React.Component {
  render() {
    let { program, version } = this.props;
    // console.log(program, version); // undefined "18.2.0"

    return (
      <div>
        {program} {version}
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
        <Props version="18.2.0" />
      </div>
    );
  }
}

Props.defaultProps = {
  program: "React",
  version: "1000"
};

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<App />);
```

```javascript
{
  program;
}
{
  version;
}
```

program props 값이 비어 있기 때문에 Props.defaultProps에서 지정한 기본 값이 화면에 표시된다.

version props 값은 상위 컴포넌트에서 전달되었기 때문에 지정한 기본 값은 무시된다.

```javascript
Props.defaultProps = {
```

상위 컴포넌트에서 값이 전달될 것이라 기대되는 program과 version props에 각각 기본 값을 할당했다.

## props를 사용해 자식 컴포넌트에 node 전달하기

---

상위 컴포넌트에서 하위 컴포넌트로 node를 전달할 수 있습니다.

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class Props extends React.Component {
  render() {
    let children = this.props.children;

    return <div>{children}</div>;
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
        <Props>
          <p>Node from App Component1.</p>
        </Props>
        <Props>
          <p>Node from App Component2.</p>
        </Props>
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<App />);
```

```javascript
{
  children;
}
```

상위 컴포넌트에서 전달한 node는 this.props.children이라는 구문으로 접근할 수 있다.
