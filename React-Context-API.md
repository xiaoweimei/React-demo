### 例子一，原生js
```
function f1(n1){
  console.log(1,n1)
  f2(n1)
}
function f2(n2){
  console.log(2,n2)
  f3(n2)
}
function f3(n3){
  console.log(3,n3)
  f4(n3)
}
function f4(n4){
  console.log(4,n4)
}
{
  let n=100
  f1(n)
  console.log('done')
}
```
### 例子二react方法改写
```
import React from "react";
import ReactDOM from "react-dom";
function F1(props){
  return (
    <div>1111,{props.n1}
      <F2 n2={props.n1}/>
    </div>
  )
}
function F2(props){
  return (
    <div>22222,{props.n2}
      <F3 n3={props.n2}/>
    </div>
  )
}
function F3(props){
  return (
    <div>33333,{props.n3}
      <F4 n4={props.n3}/>
    </div>
  )
}
function F4(props){
  return (
    <div>44444,{props.n4}</div>
  )
}
class App extends React.Component {
  constructor(){
    super()
    this.state={
      n:99
    }
  }
  render(){
    return (
      <div className="App">
        <F1 n1={this.state.n}></F1>
      </div>
    );
  }
}
const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```
### 例子三，原生js创建局部的全局变量
```
{
  let context={}
  window.setContext=function(key,value){
    context[key]=value
  }
  window.f1=function f1(){
    console.log(1)
    f2()
  }
  function f2(){
    console.log(2)
    f3()
  }
  function f3(){
    console.log(3)
    f4()
  }
  function f4(){
    console.log(4,context['n'])
  }
}
{
  window.setContext('n',100)
  f1()
  console.log('done')
}
```
### 例子四，使用react的Context Api
```
import React from "react";
import ReactDOM from "react-dom";
function F1(){
  return (
    <div className='border'>1111
      <F2/>
    </div>
  )
}
function F2(){
  return (
    <div className='border'>22222
      <F3/>
    </div>
  )
}
function F3(props){
  return (
    <div className='border'>33333,{props.n3}
      <nContext.Consumer>
        {(n)=><F4 n4={n}/>}  
      </nContext.Consumer>
    </div>
  )
}
function F4(props){
  return (
    <div className='border'>44444,{props.n4}</div>
  )
}
const nContext=React.createContext(100)
class App extends React.Component {
  render(){
    return (
      <div>
        <nContext.Provider value='999999'>
        <F1></F1>
        </nContext.Provider>
      </div>
    );
  }
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```
### 例子五，使用react的Context Api，添加更多方法
```
import React from "react";
import ReactDOM from "react-dom";
function F1(){
  return (
    <div className='border'>1111
      <F2/>
    </div>
  )
}
function F2(){
  return (
    <div className='border'>22222
      <F3/>
    </div>
  )
}
function F3(props){
  return (
    <div className='border'>33333,{props.n3}
      <nContext.Consumer>
        {(x)=><F4 n4={x.n} setN={x.setN}/>}  
      </nContext.Consumer>
    </div>
  )
}
function F4(props){
  return (
    <div className='border'>
    44444,{props.n4}
    <button onClick={props.setN}>Click me</button>
    </div>
  )
}
const nContext=React.createContext()
class App extends React.Component {
  constructor(){
    super()
    this.state={
      x:{
        n:67,
        setN:()=>{
          this.setState({
            x:{
              ...this.state.x,
              n:this.state.x.n+1
            }
          })
        }
      }
    }
  }
  render(){
    return (
      <div>
        <nContext.Provider value={this.state.x}>
        <F1></F1>
        </nContext.Provider>
      </div>
    );
  }
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```
