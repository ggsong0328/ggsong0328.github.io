---
title: React에서의 EcmaScript6 문법1
author: ggsong0328
date: 2024-02-14 15:00:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

# React에서의 EcmaScript6 문법 1

---

EcmaScript는 표준화된 스크립트 언어이고 숫자는 버전을 의미한다.

2015년에 발행된 ES6는 많은 유용한 기능이 추가되었고, JavaScript는 이 기술 규격을 따른다.

React 역시 JavaScript 기반의 라이브러리이기 때문에 ES6의 모든 기능을 사용할 수 있다.

## 템플릿 문자열 사용하기

---

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class ES6 extends React.Component {
  componentDidMount() {
    var jsString1 = "JavaScript";
    var jsString2 = "입니다.\n다음 줄입니다.";
    // console.log(jsString1 + " 프로그래밍" + jsString2);

    let ES6String1 = "ES6";
    let ES6String2 = "입니다.";
    // console.log(ES6String1 + " 프로그래밍" + ES6String2);
    // console.log(`${ES6String1} 프로그래밍${ES6Strong2} // 다음 줄입니다.`);

    let LongString = "ES6에 추가된 String 함수들입니다.";
    // console.log("startsWith : " + LongString.startsWith("ES6에 추가"));
    // console.log("endsWith : " + LongString.endsWith("함수들입니다."));
    // console.log("includes : " + LongString.includes("추가된 String"));
  }

  render() {
    let h2Style = {
      fontSize: 16,
      fontWeight: "normal"
    };

    return <h2 style={h2Style}>This is ES6 String.</h2>;
  }
}
class App extends React.Component {
  render() {
    let h1Style = { fontWeight: "normal" };
    return (
      <div>
        <h1 style={h1Style}>React Example</h1>
        <ES6 />
      </div>
    );
  }
}
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

```javascript
var jsString1 = "JavaScript";
var jsString2 = "입니다\n다음 줄입니다.";
```

문자열과 변수를 합치기 위해서는 문자열을 작은 따옴표 또는 큰 따옴표로 감싸고 + 기호로 연결해야 한다.

```javascript
console.log(`${ES6String1} 프로그래밍${ES6String2}`);
```

따옴표가 아닌 ``(백틱)으로 전체 문자열과 변수를 묶어 사용한다. 변수는 ${변수명} 형태로 넣고 코드상에서 줄바꿈을 하면 개행 문자 없이도 사용 가능하다.

```javascript
console.log("startsWith : " + LongString.startsWith("ES6에 추가"));
console.log("endsWith : " + LongString.endsWith("함수들입니다."));
console.log("includes : " + LongString.includes("추가된 String"));
```

startsWith(), endsWith(), includes()는 ES6에 추가된 String 함수들이다.

startsWith() 함수는 변수 앞에서부터, endsWith() 함수는 뒤에서부터 일치하는 문자열이 있는지 찾는다.

includes() 함수는 위치에 상관없이 변수에 특정 문자열이 포함되어 있는지를 판단한다. 함수 조건에 부합하면 true, 부합하지 않으면 false를 반환한다.

## var, let const 사용하기

---

예전 ES5에서 사용하는 var은 변수를 재선언, 재할당할 수 있다.

이런 특징으로 인해 변수의 사용 범위가 불확실해지거나 의도하지 않은 변수의 값 변경이 발생할 수 있다.

이러한 단점을 보완하기 위해 ES6에서 let과 const가 추가되었다!

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class Variables extends React.Component {
  constructor(props) {
    super(props);
    this.state = {};
  }
  componentDidMount() {
    var varName = "React";
    // console.log("varName : "+varName);
    var varName = "React 18.2.0"; // 'varName' is already defined no-redeclare
    // console.log("varName : "+varName);
    let letName = "React"; // console.log("letName : "+letName);
    // let letName="React 18.2.0"; // Parsing error : Identifier 'letName' has already been declared
    letName = "React 18.2.0"; // console.log("letName : "+letName);
    // const constName="React"; // console.log("constName : "+constName);
    // const constName="React 18.2.0"; // Parsing error : Identifier 'constName' has already been declared
    // constName="React 18.2.0"; // Uncaught TypeError : Assignment to constant variable
  }
  render() {
    let h2Style = { fontSize: 16, fontWeight: "normal" };
    return <h2 style={h2Style}>This is ES6 Variables.</h2>;
  }
}
class App extends React.Component {
  render() {
    let h1Style = { fontWeight: "normal" };
    return (
      <div>
        <h1 style={h1Style}>React Example</h1>
        <Variables />
      </div>
    );
  }
}
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

```javascript
var varName = "React 18.2.0"; // 'varName' is already defined no-redeclare
```

이미 선언한 var 변수를 다시 선언했을 때 **~ is already defined no-redeclare** 라는 경고 메시지가 로그에 출력된다.

하지만 var 변수는 재선언, 재할당을 허용하기 때문에 경고 메시지가 출려되어도 페이지가 정상적으로 표시된다.

```javascript
let letName = "React 18.2.0";
```

이미 선언한 let 변수를 다시 선언했을 때 **Parsing error: Identifier '~' has already been declared** 라는 에러 메시지가 로그에 출력된다.

let 변수는 재선언을 허용하지 않기 때문에 에러 메시지가 표시된다.

```javascript
letName = "React 18.2.1";
```

let 변수는 재할당을 허용한다. 이미 선언한 let 변수 letName에 새로운 값을 할당했을 때 페이지가 정상적으로 렌더링 된다.

```javascript
const constName = "React 18.2.0";
```

이미 선언한 const 변수를 다시 선언했을 때 **Parsing error: Identifier '~' has already been declared** 라는 에러 메시지가 로그에 출력된다.

const 변수는 재선언을 허용하지 않기 때문에 에러 메시지가 표시된다.

```javascript
constName = "React 18.2.1";
```

이미 선언한 const 변수에 새로운 값은 할당했을 때 **Uncaught TypeError : Assignment to constant variable.** 이라는 에러 메시지가 로그에 출력된다.

const 변수는 재할당을 허용하지 않기 때문에 에러 메시지가 표시된다.
