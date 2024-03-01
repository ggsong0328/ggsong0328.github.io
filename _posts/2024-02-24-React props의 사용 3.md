---
title: React props의 사용 3
author: ggsong0328
date: 2024-02-24 10:30:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

## props 사용하기 - 컬러 팔레트 만들기

---

1단계 - ColorPalette 컴포넌트를 화면에 배치:

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class ColorPalette extends React.Component {
  render() {
    let paletteStyle = {
      display: "inline-block",
      marginRight: 10,
      width: 100,
      height: 100,
      backgroundColor: "#fff",
      boxShadow: "1px 1px 2px rgba(0, 0, 0, .2)"
    };

    return <div style={paletteStyle}></div>;
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<ColorPalette />);
```

2단계 - ColorPalette 컴포넌트에 ColorChip 컴포넌트를 추가

```javascript
class ColorChip extends React.Component {
  render() {
    let chipStyle = {
      width: 100,
      height: 100,
      backgroundColor: "#09f"
    };

    return <div style={chipStyle}></div>;
  }
}

class ColorPalette extends React.Component {
  render() {
    let paletteStyle = {
      display: "inline-block",
      marginRight: 16,
      backgroundColor: "#fff",
      boxShadow: "1px 1px 2px rgba(0, 0, 0, .2)"
    };

    return (
      <div style={paletteStyle}>
        <ColorChip />
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<ColorPalette />);
```

3단계 - ColorPalette 컴포넌트에 ColorName 컴포넌트 추가

```javascript
class ColorChip extends React.Component {
  render() {
    let chipStyle = {
      width: 100,
      height: 100,
      backgroundColor: "#09f"
    };

    return <div style={chipStyle}></div>;
  }
}

class ColorName extends React.Component {
  render() {
    let nameStyle = {
      margin: 0,
      padding: 10,
      textAlign: "center",
      fontSize: 14,
      fontWeight: "bold"
    };

    return <p style={nameStyle}>#09f</p>;
  }
}

class ColorPalette extends React.Component {
  render() {
    let paletteStyle = {
      display: "inline-block",
      marginRight: 16,
      backgroundColor: "#fff",
      boxShadow: "1px 1px 2px rgba(0, 0, 0, .2)"
    };

    return (
      <div style={paletteStyle}>
        <ColorChip />
        <ColorName />
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<ColorPalette />);
```

4단계 - props를 사용해서 다양한 색상의 팔레트 구현

```javascript
class ColorChip extends React.Component {
  render() {
    let chipStyle = {
      width: 100,
      height: 100,
      backgroundColor: this.props.color
    };

    return <div style={chipStyle}></div>;
  }
}

class ColorName extends React.Component {
  render() {
    let nameStyle = {
      margin: 0,
      padding: 10,
      textAlign: "center",
      fontSize: 14,
      fontWeight: "bold"
    };

    return <p style={nameStyle}>{this.props.color}</p>;
  }
}

class ColorPalette extends React.Component {
  render() {
    let paletteStyle = {
      display: "inline-block",
      marginRight: 16,
      backgroundColor: "#fff",
      boxShadow: "1px 1px 2px rgba(0,0,0,.2)"
    };

    return (
      <div style={paletteStyle}>
        <ColorChip color={this.props.color} />
        <ColorName color={this.props.color} />
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <div>
    <ColorPalette color="#f90" />
    <ColorPalette color="#09f" />
    <ColorPalette color="#eaeaea" />
  </div>
);
```

## 컴포넌트 속성 전달하기

---

Component1 -> Component2 -> Component3 컴포넌트 내용을 전달하고 있는 예제

React에서는 Component1에서 Component3으로 바로 내용을 전달하는 방법이 없다.

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class Component3 extends React.Component {
  render() {
    return (
      <div>
        <p>{this.props.color}</p>
        <p>{this.props.color}</p>
        <p>{this.props.color}</p>
      </div>
    );
  }
}

class Component2 extends React.Component {
  render() {
    return (
      <Component3
        color={this.props.color}
        name={this.props.name}
        size={this.props.size}
      />
    );
  }
}

class Component1 extends React.Component {
  render() {
    return (
      <Component2
        color={this.props.color}
        name={this.props.name}
        size={this.props.size}
      />
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<Component1 color="#f90" name="orange" size="small" />);
```

전개 연산자(spread operator, ...)를 사용하면 이러한 전달 코드를 조금 더 간단하게 작성할 수 있다.

전개 연산자를 사용하면 배열이나 객체의 정보를 모두 참조할 수 있다.

```javascript
const obj1 = {shape: "triangle", x: 42};
const obj2 = {shape: "rectangle" y: 12};

const cloneObj = {...obj1};
// console.log(cloneObj); // {shape: "triangle", x: 42}

const mergeObj = {...obj1, ...obj2};
// console.log(mergeObj) // {shape: "rectangle", x:42, y:12}
```

```javascript
class Component3 extends React.Component {
  render() {
    return (
      <div>
        <p>{this.props.color}</p>
        <p>{this.props.name}</p>
        <p>{this.props.size}</p>
      </div>
    );
  }
}

class Component2 extends React.Component {
  render() {
    return <Component3 {...this.props} />;
  }
}

class Component1 extends React.Component {
  render() {
    return <Component2 {...this.props} />;
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<Component1 color="#f90" name="orange" size="small" />);
```
