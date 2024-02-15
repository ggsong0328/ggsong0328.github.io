---
title: React에서의 EcmaScript6 문법3
author: ggsong0328
date: 2024-02-15 22:00:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

# React에서의 EcmaScript6 문법 3

## forEach() 함수 사용하기

---

배열 함수 forEach()는 for 구문에서 사용하던 순번과 배열의 크기 변수를 사용하지 않는다.

배열의 처음부터 마지막 순번까지 모두 작업하는 경우 forEach() 함수를 사용하는 것이 편하다!

하지만 특정 순번에서만 배열 값을 사용하거나 변경해야 하는 상황이라면 for 구문을 사용해야한다.

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class ForEach extends React.Component {
  componentDidMount() {
    let forArray = [3, 2, 8, 8];
    let forNewArray = [];

    for (let i = 0; i < forArray.length; i++) {
      forNewArray.push(forArray[i]);
    }

    console.log("1. forNewArray : [" + forNewArray + "]");

    let forEachArray = [3, 2, 8, 8];
    let forEachNewArray = [];
    forEachArray.forEach((result) => {
      // console.log(result);
      forEachNewArray.push(result);
    });

    console.log("2. forEachNewArray : [" + forEachNewArray + "]");
  }
  render() {
    let h2Style = { fontSize: 16, fontWeight: "normal" };
    return <h2 style={h2Style}>This is ForEach Function.</h2>;
  }
}
class App extends React.Component {
  render() {
    let h1Style = { fontWeight: "normal" };
    return (
      <div>
        <h1 style={h1Style}>React Example</h1>
        <ForEach />
      </div>
    );
  }
}
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

```javascript
for (let i = 0; i < forArray.length; i++) {
  forNewArray.push(forArray[i]);
}
```

for 구문에서는 순번 변수(i)와 배열의 크기(forArray.length)가 필요하다. 순번을 0부터 1씩 증가시킨다.

배열의 크기보다 작은 값이 될 때까지 새로운 배열 forNewArray에 기존 변수 값을 push() 메서드를 이용해서 넣는다.

```javascript
forEachArray.forEach((result) => {
  forEachNewArray.push(result);
});
```

forEach() 함수에서는 순번과 배열의 크기 정보를 사용하지 않는다. 0부터 배열의 크기만큼 반복하면서 순서대로 배열 값을 반환한다.

반복문이 실행될 때마다 화살표 함수로 결과값(result)을 받아 새로 배열 forEachNewArray에 넣는다.

## map() 함수 사용하기

---

배열 함수 map()은 forEach() 함수와 마찬가지로 for 구문에서 사용했던 순번과 배열의 크기 변수를 사용하지 않는다.

차이점은 map() 함수는 forEach() 함수와 달리 return 구문을 사용해 반환 값을 받을 수 있다.

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class Map extends React.Component {
  componentDidMount() {
    let mapArray = [3, 2, 8, 8];
    let mapNewArray = mapArray.map((x) => x);
    console.log("1. mapNewArray : [" + mapNewArray + "]");
    let mapMultiArray = mapArray.map((x) => x * 2);
    console.log("2. mapMultiArray : [" + mapMultiArray + "]");
    let objArray = [
      { key: "React", value: "18.2.0" },
      { key: "UI", value: "Interaction" }
    ];
    let mapObjArray = objArray.map((obj, index) => {
      console.log(index + 3 + ". obj : " + JSON.stringify(obj));
      let mapReturnObj = {};
      mapReturnObj[obj.key] = obj.value;
      return mapReturnObj;
    });
    console.log("5. mapObjArray : " + JSON.stringify(mapObjArray));
  }
  render() {
    let h2Style = { fontSize: 16, fontWeight: "normal" };
    return <h2 style={h2Style}>This is Map Function.</h2>;
  }
}
class App extends React.Component {
  render() {
    let h1Style = { fontWeight: "normal" };
    return (
      <div>
        <h1 style={h1Style}>React Example</h1>
        <Map />
      </div>
    );
  }
}
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

```javascript
let mapNewArray = mapArray.map((x) => x);
```

기존 배열(mapArray)에서 map() 함수를 사용해서 순서대로 하나씩 순서대로 하나씩 요소에 접근해 가져온다.

이때마다 콜백 함수가 실행된다. 가져온 값을 변수 x에 넣은 후 그대로 반환해 (x => x) 순서대로 쌓아 놓는다.

마지막 요소까지 반복했다면, 한 번에 새로운 배열은 mapNewArray에 저장한다.

```javascript
let mapMultiArray = mapArray.map((x) => x * 2);
```

기존 배열(mapArray)에서 요소에 순서대로 접근한 다음, 각각 2를 곱해 새로운 배열(mapMultiArray)에 저장한다.

```javascript
let objArray = [
  { key: "React", value: "18.2.0" },
  { key: "UI", value: "Interaction" }
];
```

배열 안에 객체를 생성한다.

```javascript
let mapObjArray = objArray.map((obj, index) => {
```

배열 안에 객체를 순서대로 가져와 콜백 함수를 실행하는데, 가져온 값을 obj라는 변수에 저장한다. 콜백 함수의 두 번째 인자인 index는 기존 배열의 index와 동일!

```javascript
console.log(index + 3 + ". obj : " + JSON.stringify(obj));
```

기존 배열에서 가져온 객체 값을 순서대로 출력한다.

```javascript
let mapReturnObj = {};
mapReturnObj[obj.key] = obj.value;
return mapReturnObj;
```

새로운 객체(mapReturnObj)를 선언한다. 기존 배열(objArray)의 key, value 값을 새로운 객체인 mapReturnObj에 key, value 값으로 저장한다. 모든 반복이 끝나면 새롭게 선언된 객체인 mapReturnObj를 반환한다.
