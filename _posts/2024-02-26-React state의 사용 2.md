---
title: React state의 사용 2
author: ggsong0328
date: 2024-02-26 10:30:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

## state 사용하기

---

1초에 하나씩 수가 증가되는 프로그램을 제작하자.

1단계:

```html
<div id="root"></div>
```

```css
#root {
  padding: 10px;
}
```

```javascript
class AutoCounter extends React.Component {
  render() {
    let titleStyle = {
      margin: 0,
      padding: 0,
      fontWeight: "bold",
      color: "#333"
    };

    return <p style={titleStyle}>React Example</p>;
  }
}

class AutoCounterBox extends React.Component {
  render() {
    let boxStyle = {
      display: "inline-block",
      padding: 20,
      backgroundColor: "#eaeaea",
      borderRadius: 6
    };

    return (
      <div style={boxStyle}>
        <AutoCounter />
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<AutoCounterBox />);
```

2단계:

constructor() 함수는 화면이 그려지기 전, 실행되는 함수로서 초기의 데이터를 설정할 수 있다.

componentDidMount() 함수는 화면이 그려진 후, 실행되는 함수이다.

setState() 함수는 state 값을 갱신할 때 사용되는 함수이다.

```javascript
class AutoCounter extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      count: 0
    };
  }

  /*
  timer(){
    //console.log(this.state.count);

    this.setState({
      count: this.state.count + 10
    });
  }

  componentDidMount(){
    // this.timer();
    setTimeout(this.timer, 1000);
  }
  */

  /*
  timer(){
    this.setState({
      count: this.state.count + 10
    });
  }

  componentDidMount(){
    setTimeout(this.timer.bind(this), 1000);
  }
  */

  timer = () => {
    this.setState({
      count: this.state.count + 10
    });
  };

  componentDidMount() {
    // setTimeout(this.timer, 1000);
    setInterval(this.timer, 1000);
  }

  timer() {
    this.setState({
      count: this.state.count + 10
    });
  }

  componentDidMount() {
    setInterval(this.timer, 1000);
  }

  render() {
    let titleStyle = {
      margin: 0,
      padding: 0,
      fontWeight: "bold",
      color: "#333"
    };

    return <p style={titleStyle}>{this.state.count}</p>;
  }
}

class AutoCounterBox extends React.Component {
  render() {
    let boxStyle = {
      display: "inline-block",
      padding: 20,
      backgroundColor: "#eaeaea",
      borderRadius: 6
    };

    return (
      <div style={boxStyle}>
        <AutoCounter />
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(<AutoCounterBox />);
```
