### react hook APi
1. 例子一
```
import React from "react";
import ReactDOM from "react-dom";
import {useState} from 'react';

function App() {
  const [count/*值* */,setCount/*更新函数*/]=useState(0)
  const add=()=>{
    setCount(count+1)
  }
  const minus=()=>{
    setCount(count-1)
  }
  return (
    <div>
      <div>{count}</div>
      <button onClick={add}>+1</button>
      <button onClick={minus}>-1</button>
    </div>
  )
}
const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```
2. 例子二，用class改写
```
import React from "react";
import ReactDOM from "react-dom";
import {useState} from 'react';

class App extends React.Component{
  constructor(){
    super()
    this.state={
      count:0
    }
  }
  add=()=>{
    this.setState({
      count:this.state.count+1
    })
  }
  minus=()=>{
    this.setState({
      count:this.state.count-1
    })
  }
  render(){
    return (
      <div>
        <div>{this.state.count}</div>
        <button onClick={this.add}>+1</button>
        <button onClick={this.minus}>-1</button>
      </div>
    )
  }
}
const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```
3. 例子三
```
import React from "react";
import ReactDOM from "react-dom";
import {useState} from 'react';

function App() {
  const [count/*值* */,setCount/*更新函数*/]=useState(0)
  const [user,setUser] =useState({name:'frank',age:18})
  const add=()=>{
    setCount(count+1)
  }
  const minus=()=>{
    setCount(count-1)
  }
  const old=()=>{
    setUser({
      ...user,
      age:user.age+1
    })
  }
  return (
    <div>
      <div>{count}</div>
      <button onClick={add}>+1</button>
      <button onClick={minus}>-1</button>
      <div>{user.name},{user.age}</div>
      <button onClick={old}>加一岁</button>
    </div>
  )
}
const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```
4. 例子四
```
import React from "react";
import ReactDOM from "react-dom";
import {useState} from 'react';

function App() {
  const [count/*值* */,setCount/*更新函数*/]=useState(0)
  const [user,setUser] =useState({
    name:'frank',age:18,
    hobbies:['lol','dota','code']
  })
  const add=()=>{
    setCount(count+1)
  }
  const minus=()=>{
    setCount(count-1)
  }
  const old=()=>{
    setUser({
      ...user,
      age:user.age+1
    })
  }
  const addhob=()=>{
    let newhob=Math.random()
    setUser({
      ...user,
      hobbies:[...user.hobbies,newhob]
    })
  }
  const minushob=()=>{
    user.hobbies.splice(1,1)
    setUser({
      ...user,
      hobbies:user.hobbies
    })
  }
  return (
    <div>
      <div>{count}</div>
      <button onClick={add}>+1</button>
      <button onClick={minus}>-1</button>
      <div>{user.name},{user.age},<br />{user.hobbies.join('.')}</div>
      <button onClick={old}>加一岁</button>
      <button onClick={addhob}>增加爱好</button>
      <button onClick={minushob}>删除爱好</button>
    </div>
  )
}
const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```
5. 例子五
```
import React, { useEffect } from "react";
import ReactDOM from "react-dom";
import {useState} from 'react';

function App() {
  const [count/*值* */,setCount/*更新函数*/]=useState(0)
  const [user,setUser] =useState({
    name:'frank',age:18,
    hobbies:['lol','dota','code']
  })
  useEffect(()=>{
    document.querySelector('#output').innerText=count
  })
  const add=()=>{
    setCount(count+1)
  }
  const minus=()=>{
    setCount(count-1)
  }
  const old=()=>{
    setUser({
      ...user,
      age:user.age+1
    })
  }
  const addhob=()=>{
    let newhob=Math.random()
    setUser({
      ...user,
      hobbies:[...user.hobbies,newhob]
    })
  }
  const minushob=()=>{
    user.hobbies.splice(1,1)
    setUser({
      ...user,
      hobbies:user.hobbies
    })
  }
  return (
    <div>
      <div>{count}</div>
      <button onClick={add}>+1</button>
      <button onClick={minus}>-1</button>
      <div>{user.name},{user.age},<br />{user.hobbies.join('.')}</div>
      <button onClick={old}>加一岁</button>
      <button onClick={addhob}>增加爱好</button>
      <button onClick={minushob}>删除爱好</button>
    </div>
  )
}
const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```
