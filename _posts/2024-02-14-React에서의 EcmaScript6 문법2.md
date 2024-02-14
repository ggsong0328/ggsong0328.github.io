---
title: React에서의 EcmaScript6 문법2
author: ggsong0328
date: 2024-02-14 16:00:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

# React에서의 EcmaScript6 문법 2

## 전개 연산자 (...) 사용하기

---

전개 연산자는 배열이나 객체를 좀 더 직관적이고 편리하게 합치거나 추출할 수 있게 도와주는 문법이다.

사용 방법으로는 변수 앞에 마침표 3개 (...)를 입력한다.

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class SpreadOperator extends React.Component {
  componentDidMount() {
    // JavaScript Array
    var varArray1 = ["num1", "num2"];
    var varArray2 = ["num3", "num4"]; // var sumVarArray=[varArray1[0], varArray1[1], varArray2[0], varArray2[1]];
    var sumVarArray = [];
    sumVarArray = sumVarArray.concat(varArray1, varArray2);
    console.log("1. sumVarArray : " + sumVarArray);
    // ES6 Array
    let sumLetArray = [varArray1, varArray2];
    console.log("2. sumLetArray : " + sumLetArray);
    let letArray = ["num1", "num2", "num3", "num4"];
    let [sum1, sum2, ...remain] = letArray;
    console.log(
      "3. sum1 : " + sum1 + ", sum2 : " + sum2 + ", remain : " + remain
    );
    // JavaScript Object
    var varObj1 = { key1: "var1", key2: "var2" };
    var varObj2 = { key2: "new2", key3: "var3" };
    var sumVarObj = {};
    sumVarObj = Object.assign(sumVarObj, varObj1, varObj2);
    // console.log("4. sumVarObj : "+sumVarObj);
    console.log("4. sumVarObj : " + JSON.stringify(sumVarObj));
    // ES6 Object
    let sumLetObj = { ...varObj1, ...varObj2 };
    console.log("5. sumLetObj : " + JSON.stringify(sumLetObj));
    let { key1, key3, ...others } = sumLetObj;
    console.log(
      "6. key1 : " +
        key1 +
        ", key3 : " +
        key3 +
        ", others : " +
        JSON.stringify(others)
    );
  }
  render() {
    let h2Style = { fontSize: 16, fontWeight: "normal" };
    return <h2 style={h2Style}>This is Spread Operator.</h2>;
  }
}
class App extends React.Component {
  render() {
    let h1Style = { fontWeight: "normal" };
    return (
      <div>
        <h1 style={h1Style}>React Example</h1>
        <SpreadOperator />
      </div>
    );
  }
}
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

```javascript
// var sumVarArray=[varArray1[0], varArray1[1], varArray2[0], varArray2[1]];
var sumVarArray = [];
sumVarArray = sumVarArray.concat(varArray1, varArray2);
```

기존 ES5에서 배열 2개를 합치기 위해서는 배열 각각의 인덱스로 접근해 값을 가져오거나 concat() 메소드를 사용했다.

varArray1, varArray2 배열에 각각 인덱스(0, 1)로 접근해 인자값(num1, num2, num3, num4)을 가져와 새로운 배열 sumVarArray에 하나씩 넣는다.

```javascript
let sumLetArray = [varArray1, varArray2];
```

반면에 ES6에서는 대괄호[] 를 사용해 여러 개의 배열을 합칠 수 있다.

```javascript
const [sum1, sum2, ...remain] = letArray;
```

letArray 배열의 값을 추출해 개별 변수에 넣는다. 순서대로 변수 sum1에 letArray[0] 값, 변수 sum2에 letArray[1] 값을 대입한다. 나머지 배열 값은 마지막 전개 연산자가 처리가 된 ...remain 변수에 배열 형식으로 넣는다.

```javascript
var sumVarObj = Object.assign({}, varObj1, varObj2);
```

기존 ES5에서는 객체 2개를 합치기 위해서는 Object.assign() 함수를 이용해야 한다.

첫 번째 인자 {}는 함수의 return 값이고 뒤의 인자의 객체들은 콤마로 연결해 나열하면 여러 개의 객체를 합칠 수 있다.

```javascript
let sumLetObj = { ...varObj1, ...varObj2 };
```

ES6에서는 ...을 객체명 앞에 붙여 여러 개의 객체를 합칠 수 있다.

```javascript
const { key1, key3, ...others } = sumLetObj;
```

sumLetObj 객체의 키와 값을 추출해 키와 동일한 명칭의 개별 변수에 넣는다. 나머지는 전개 연산자 처리된 ...others 변수에 객체 형식으로 넣는다.

## 화살표 함수 사용하기

---

ES6에서 등장한 화살표 함수는 function 대신 **=>** 문자열을 사용하여 return 문자열을 생략할 수도 있다.

따라서 기존 ES5 함수보다 간략하게 선언할 수 있다. 또한 화살표 함수에서는 콜백함수에서 this를 bind를 해야하는 문제도 발생하지 않는다!

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class ArrowFunction extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      arrowLabel: "React 18.2.0",
      num: 4
    };
  }

  componentDidMount() {
    function myFn1(num1) {
      console.log(num1 + ". ES5 Function");
    }

    let myFn2 = (num1) => {
      console.log(num1 + ". Arrow Function");
    };

    myFn1(1);
    myFn2(2);
    this.myFn3(1, 2);
    this.myFn4();
    this.myFn5();
    this.myFn6(1, 2, 3);
  }

  myFn3 = (num1, num2) => {
    let num3 = num1 + num2;
    console.log(num3 + ". Arrow Function : " + this.state.arrowLabel);
  };

  myFn4() {
    var this_bind = this;

    setTimeout(function () {
      console.log(this_bind.state.num + ". ES5 Callback Function No Bind");
      // console.log(this.state.arrowLabel);
    }, 100);
  }

  myFn5() {
    setTimeout(
      function () {
        console.log("5. ES5 Callback Function Bind : " + this.state.arrowLabel);
      }.bind(this),
      100
    );
  }

  myFn6 = (num1, num2, num3) => {
    let num4 = num1 + num2 + num3;

    setTimeout(() => {
      console.log(
        num4 + ". Arrow Callback Function : " + this.state.arrowLabel
      );
    }, 100);
  };

  render() {
    let h2Style = {
      fontSize: 16,
      fontWeight: "normal"
    };

    return <h2 style={h2Style}>This is Arrow Function.</h2>;
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
        <ArrowFunction />
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<App />);
```

```javascript
myFn1(1);
myFn2(2);
this.myFn3(1, 2);
this.myFn4();
this.myFn5();
this.myFn6(1, 2, 3);
```

myFn1 ~ myFn6까지의 함수를 순서대로 호출한다.

```javascript
function myFn1(num1) {
```

함수를 호출할 때 전달받은 num1이라는 변수를 함수 내부에서 사용할 수 있다.

```javascript
myFn3 = (num1, num2) => {
```

함수를 function 키워드 대신 => 로 선언했다.

함수 내에서 사용하는 this 컴포넌트인데, this로 컴포넌트의 state에 접근해 사용할 수 있다.

```javascript
myFn4() {
  var this_bind = this;

```

콜백 함수 내부에서는 컴포넌트에 this로 접근할 수 없기 때문에 접근할 수 있는 변수에 this를 백업한다.

백업된 변수는 this_bind를 이용해 컴포넌트의 state 변수에 접근할 수 있다.

```javascript
console.log(this.state.arrowLabel);
```

콜백 함수 내부에서 this는 window 객체이기 때문에 this로 state 변수에 접근하면 undefined 에러가 발생!

```javascript
}.bind(this), 100);
```

bind() 함수로 this를 지정해주면, this를 컴포넌트로 사용할 수 있다.

```javascript
myFn6 = (num1, num2, num3) => {
```

화살표 함수에서는 this를 bind() 함수로 this를 지정해주지 않아도, this 컴포넌트로 사용해 state에 접근할 수 있다(!)
