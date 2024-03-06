---
title: Create React App을 사용한 React 4
author: ggsong0328
date: 2024-03-01 15:30:00 +0800
categories: [리엑트 공부]
tags: [React]
pin: false
math: true
mermaid: true
---

## 업무 리스트 예제 제작하기

---

1단계:

```javascript
// js/App.js

import React, { Component } from "react";
import AddTask from "./AddTask";
import "./App.css";
class App extends Component {
  render() {
    return (
      <div className="container">
        <h1>React Example</h1>
        <AddTask />
      </div>
    );
  }
}
export default App;
```

```javascript
// src/AddTask.js

import React, { Component } from "react";

class AddTask extends Component {
  render() {
    let inputStyle = {
      marginTop: 20,
      padding: "0px, 10px",
      width: 125,
      lineHeight: "32px",
      fontSize: 14,
      border: "1px solid #ccc"
    };
    let buttonStyle = {
      margin: "20px 0px 0px 5px",
      padding: 10,
      fontSize: 14,
      backgroundColor: "#999",
      color: "#fff",
      border: "none",
      cursor: "pointer"
    };

    return (
      <div className="main">
        <div className="header">
          <form>
            <input
              type="text"
              placeholder="Add Task"
              style={inputStyle}
            ></input>
            <button type="submit" style={buttonStyle}>
              Added
            </button>
          </form>
        </div>
      </div>
    );
  }
}

export default AddTask;
```

2단계:

```javascript
// src/AddTask.js

import React, { Component } from "react";

class AddTask extends Component {
  addTask(e) {
    e.preventDefault();
    console.log(this_input.value);
  }

  render() {
    let inputStyle = {
      marginTop: 20,
      padding: "0px 10px",
      width: 125,
      lineHeight: "32px",
      fontSize: 14,
      border: "1px solid #ccc"
    };
    let buttonStyle = {
      margin: "20px 0px 0px 5px",
      padding: 10,
      fontSize: 14,
      backgroundColor: "#999",
      color: "#fff",
      border: "none",
      cursor: "pointer"
    };

    return (
      <div className="main">
        <div className="header">
          <form onSubmit={this.addTask.bind(this)}>
            <input
              type="text"
              placeholder="Add Task"
              style={inputStyle}
              ref={function (e) {
                this._input = e;
              }.bind(this)} // HTML 요소의 레퍼런스를 변수에 저장!
            ></input>
            <button type="submit" style={buttonStyle}>
              Added
            </button>
          </form>
        </div>
      </div>
    );
  }
}

export default AddTask;
```

3단계:

```javascript
// src/AddTask.js

import React, { Component } from "react";

class AddTask extends Component {
  constructor() {
    super();

    this.state = {
      tasks: []
    };
  }

  addTask = (e) => {
    e.preventDefault();

    let taskArray = this.state.tasks;

    if (this._input.value != "") {
      taskArray.push({
        key: Date.now(),
        msg: this._input.value
      });
    }
  };

  render() {
    let inputStyle = {
      marginTop: 20,
      padding: "0px 10px",
      width: 125,
      lineHeight: "32px",
      fontSize: 14,
      border: "1px solid #ccc"
    };
    let buttonStyle = {
      margin: "20px 0px 0px 5px",
      padding: 10,
      fontSize: 14,
      backgroundColor: "#999",
      color: "#fff"
    };

    return (
      <div className="main">
        <div className="header">
          <form onSubmit={this.addTask}>
            <input
              type="text"
              placeholder="Add Task"
              style={inputStyle}
              ref={(e) => (this._input = e)}
            ></input>
            <button type="submit" style={buttonStyle}>
              Added
            </button>
          </form>
        </div>
      </div>
    );
  }
}

export default AddTask;
```

4단계:

```javascript
// src/AddTask.js

import React, { Component } from react;

class AddTask extends Component {
  constructor(){
    super();

    this.state={
      tasks: []
    };
  }

  addTask = e => {
    e.preventDefault();

    let taskArray = this.state.tasks;

    if(this._input.value != ""){
      taskArray.push(
        {
          key: Date.now(),
          msg: this._input.value
        }
      );
    }

    this.setState({
      tasks: taskArray
    });
  };

  render(){
    let inputStyle={
      marginTop: 20,
      padding: "0px 10px",
      width: 125,
      lineHeight: "32px",
      fontSize: 14,
      border: "1px solid #ccc"
    };
    let buttonStyle={
      margin: "20px 0px 0px 5px",
      padding: 10,
      fontSize: 14,
      backgroundColor: "#999",
      color: "#fff",
      border: "none",
      cursor: "pointer"
    };
    let liStyle={
      marginTop: 10
    }

    let data = this.state.tasks;

    let liTasks = data.map(function(task){
      return <li key={task.key} style={liStyle}>{task.msg}</li>
    });

    return(
      <div className="main">
        <div className="header">
          <form onSubmit={this.addTask}>
            <input
              type="text"
              placeholder="Add Task"
              style={inputStyle}
              ref={e => this._input=e}
            >
            </input>
            <button type="submit" style={buttonStyle}>Added</button>
            <ul>
              {listTasks}
            </ul>
          </form>
        </div>
      </div>
    );
  }
}

export default AddTask;
```

5단계:

```javascript
// src/AddTask.js

import React, { Component } from "react";
import AddTaskList from "./AddTaskList";

class AddTask extends Component {
  constructor() {
    super();

    this.state = {
      tasks: []
    };
  }

  addTask = (e) => {
    e.preventDefault();

    let taskArray = this.state.tasks;

    if (this._input.value != "") {
      taskArray.push({
        key: Date.now(),
        msg: this._input.value
      });
    }

    this.setState({
      tasks: taskArray
    });
  };

  render() {
    let inputStyle = {
      marginTop: 20,
      padding: "0px 10px",
      width: 125,
      lineHeight: "32px",
      fontSize: 14,
      border: "1px solid #ccc"
    };
    let buttonStyle = {
      margin: "20px 0px 0px 5px",
      padding: 10,
      fontSize: 14,
      backgroundColor: "#999",
      color: "#fff",
      border: "none",
      cursor: "pointer"
    };

    return (
      <div className="main">
        <div className="header">
          <form onSubmit={this.addTask}>
            <input
              type="text"
              placeholder="Add Task"
              style={inputStyle}
              ref={(e) => (this._input = e)}
            ></input>
            <button type="submit" style={buttonStyle}>
              Added
            </button>
            <AddTaskList propsValue={this.state.tasks} />
          </form>
        </div>
      </div>
    );
  }
}

export default AddTask;
```

```javascript
// src/AddTaskList.js

import React, { Component } from "react";
class AddTaskList extends Component {
  render() {
    let liStyle = { marginTop: 10 };

    let data = this.props.propsValue;

    let listTasks = data.map((task) => (
      <li key={task.key} style={liStyle}>
        {task.msg}
      </li>
    ));
    return <ul>{listTasks} </ul>;
  }
}
export default AddTaskList;
```
