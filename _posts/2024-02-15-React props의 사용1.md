---
title: React props의 사용 1
author: ggsong0328
date: 2024-02-15 23:00:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

## props 사용하기

---

props는 부포 컴포넌트가 자식 컴포넌트에 데이터를 전달할 때 사용한다.

props를 전달받은 자식 컴포넌트에서는 데이터를 수정할 수 없다.

데이터를 변경하기 위해서는 컴포넌트 내부에서만 사용하는 변수에 값을 넣어 사용해야 한다.

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
    // console.log(this.props);
    // console.log(this.props.propsValue);
    let propsValue = this.props.propsValue;
    propsValue += " from App Component.";
    return <div>{propsValue}</div>;
  }
}
class App extends React.Component {
  render() {
    let h1Style = { fontWeight: "normal" };
    return (
      <div>
        <h1 style={h1Style}>React Example</h1>
        <Props propsValue="This is props" />
      </div>
    );
  }
}
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

```javascript
<Props propsValue="This is props" />
```

하위 컴포넌트에 전달할 props, propsValue에 문자열을 저장한다.

```javascript
let propsValue = this.props.propsValue;
```

this.props 뒤에 상위 컴포넌트에서 전달받은 props를 붙이면, 해당 데이터를 사용할 수 있다.

```javascript
propsValue += " from App Component";
```

데이터를 수정해야 할 경우, props 자체가 아닌 컴포넌트 내부 변수, propsValue에 옮겨 제공한다.

상위 컴포넌트에서 받은 문자열 뒤에 새로운 문자열, 'from App Component'를 붙인다.

```javascript
<div>{propsValue}</div>
```

가공된 문자열을 화면에 표시한다.

## props의 다양한 자료형 선언하기

---

자식 컴포넌트에서 props에 대한 자료형을 선언해 놓으면, 부모 컴포넌트에서 넘어오는 props 변수들의 자료형과 비교한다.

자료형:

1. 문자 - **<p>{string}</p>**
2. 숫자 - **<p>{number}</p>**
3. 불린 - **<p>{boolean.toString()}</p>**
4. 배열 - **<p>{array.toString()}</p>**
5. 오브젝트 - **<p>{JSON.stringfy(object)}</p>**
6. 함수 - **<p>{fn}</p>**

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
    // console.log(this.props);

    // for(let item in this.props){
    // console.log(item);
    // console.log(this.props[item]);
    // }

    let {
      stringData,
      numberData,
      booleanData,
      arrayData,
      objectData,
      functionData
    } = this.props;

    return (
      <div>
        <p>stringData : {stringData}</p>
        <p>numberData : {numberData}</p>
        <p>booleanData : {booleanData.toString()}</p>
        <p>arrayData : {arrayData.toString()}</p>
        <p>objectData : {JSON.stringify(objectData)}</p>
        <p>functionData : {functionData}</p>
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
        <h1 style={h1Style}>Hello React</h1>
        <Props
          stringData="React"
          numberData={10}
          // booleanData={true}
          booleanData={1 === 1}
          arrayData={[0, 1, 2]}
          objectData={{ UI: "HTML, CSS, JavaScript", program: "React" }}
          functionData={console.log("functionData")}
        />
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<App />);
```

## props를 Boolean으로 사용하기

---

props 값을 Boolean 형으로 하위 컴포넌트에 전달할 경우, true나 false 중 하나를 반환한다.

추가 문법으로 props를 선언한 후 값을 할당하지 않고 넘기면 true가 기본 값으로 할당된다.

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
    // let BooleanTrueFalse=this.props.BooleanTrueFalse;
    let { BooleanTrueFalse } = this.props;
    // console.log(BooleanTrueFalse);

    return (
      <div>
        <p>
          {BooleanTrueFalse ? "2. " : "1. "}
          {BooleanTrueFalse.toString()}
        </p>
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
        <Props BooleanTrueFalse={false} />
        <Props BooleanTrueFalse />
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<App />);
```

```javascript
let { BooleanTrueFalse } = this.props;
```

render() 함수 내에서 지역 변수를 선언해 props로 전달한 값을 대입한다. 하나의 props 값을 대입할 경우에도 중괄호를 사용한다. 중괄호를 사용하지 않을 경우에는 Object로 대입된다.

```javascript
{
  BooleanTrueFalse ? "2 ." : "1. ";
}
```

삼항연산자를 이용해 BooleanTrueFalse 변수가 true면 '2', false면 '1'을 화면에 출력한다.

```javascript
{
  BooleanTrueFalse.toString();
}
```

BooleanTrueFalse 변수가 false일 경우에는 false가 출력되고, 값이 없을 경우 기본 값으로 true가 화면에 출력된다. Boolean 변수는 직접 화면에 출력할 수 없으므로 출력을 하기 위해 toString() 메서드를 사용해 문자열로 변환한다!
