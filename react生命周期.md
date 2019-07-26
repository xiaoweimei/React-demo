### 原生js
```
let app=document.getElementById("app")
//create创建div
let div=document.createElement('div')

let state=0

div.innerHTML=`
  <p>${state}</p>
  <button>+1</button>
  <button>die</button>
`
//componentWillMount
//mount，挂载div
app.appendChild(div)

//update div
div.querySelector('button').onclick=()=>{
  state+=1
  div.querySelector('p').innerText=state
}

//die destroy div
div.querySelectorAll("button")[1].onclick=()=>{
  div.querySelector("button").onclick=null
  div.querySelectorAll("button")[1].onclick=null
  div.remove()
  div=null
}
```
### React生命周期
```
import React from "react";
import ReactDOM from "react-dom";
import "./styles.css";

let div=document.createElement('div')
document.body.appendChild(div)
console.log=function(content){
  div.innerHTML+=`${content}<br>`
  
}

class Baba extends React.Component{
  onClick(){
    this.setState({
      hasChild:false
    })
  }
  callSon(){
    this.setState({
      word:'你还好吧'
    })
  }
  constructor(){
    super()
    this.state={
      hasChild:true,
    }
  }
  render(){
    return (
      <div>我是你爸爸
        {this.state.hasChild?<App word={this.state.word}/>:null}
        <button onClick={()=>this.onClick()}>kill son</button>
        <button onClick={()=>this.callSon()}>call son</button>
      </div>
    )
  }
}

class App extends React.Component{
  onClick(){
    console.log('用户点击了')
    this.setState({
      n:this.state.n+1
    })
  }
  constructor(){
    console.log('创建app')
    super()
    this.state={
      n:0
    }
  }
  componentWillMount(){
    console.log('将要mount App')
  }
  render(){
    console.log('填充/更新 App的内容')
    return (
      <div className="App">
        {this.state.n}
        <br/>我爸说{this.props.word}<br/>
        <button onClick={()=>this.onClick()}>+1</button>
        <button>go die</button>
      </div>
    );
  }
  componentDidMount(){
    console.log('mount App完毕')
  }
  componentWillUpdate(){
    console.log('update App之前')
  }
  componentDidUpdate(){
    console.log('update App之后')
  }
  componentWillUnmount(){
    console.log('App 快要死了，记得有事儿烧纸')
  }
  componentWillReceiveProps(){
    console.log('我爸说话了')
  }
}

const rootElement = document.getElementById("root");
ReactDOM.render(<Baba />, rootElement);

```
