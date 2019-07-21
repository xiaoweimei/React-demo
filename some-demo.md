- 实现一个加减的小例子
```
let result=document.querySelector("#result")
let add=document.querySelector("#add")
let minus=document.querySelector("#minus")
add.onclick=function(){
  result.innerText=number=parseInt(result.innerText,10)+1
}
minus.addEventListener("click",function(){
  result.innerText=parseInt(result.innerText,10)-1
})
```
- react函数实现
```
let number1=0
let number2=0
function App(){
  return (
    <div>
      <Box1 />
      <Box2 />
     </div>
  )
}
function Box1(obj){
  let add1=()=>{
    number1+=1
    render()
  }
  let minus1=()=>{
    number1-=1
    render()
  }
  return  <div class="parent">
      <span class="red">{number1}</span>
      <button onClick={add1}>+</button>
      <button onClick={minus1}>-</button>
     </div>
}
function Box2(){
  let add2=()=>{
    number2+=2
    render()
  }
  let minus2=()=>{
    number2-=2
    render()
  }
  return  <div class="parent">
      <span class="red">{number2}</span>
      <button onClick={add2}>+</button>
      <button onClick={minus2}>-</button>
     </div>

}
render()
function render(){
    ReactDOM.render(
    <App />,//React.createElement(App)
    document.querySelector('#root'))
}
```
- react的class实现
```
function App(props){
  return (
    <div>
      <Box1 name="frank"/>
      <Box2 name="jack"/>
     </div>
  )
}

class Box1 extends React.Component{
  constructor(props){
    super(props)
    this.state={
      number:0
    }
  }
  add(){
    this.setState({
      number:this.state.number+=1
    }
    )
  }
  minus(){
    this.setState({
      number:this.state.number-=1
    })
  }
  render(){ //局部render
    return (
      <div className="red">
        <span>{this.state.number}</span>
        <button onClick={this.add.bind(this)}>+</button>
        <button onClick={this.minus.bind(this)}>-</button>
        <span>{this.props.name}</span>
      </div>
      )
  }
}
class Box2 extends React.Component{
  constructor(props){
    super(props)
    this.state={
      number:0
    }
  }
  add(){
    this.setState({
      number:this.state.number+=1
    }
    )
  }
  minus(){
    this.setState({
      number:this.state.number-=1
    })
  }
  render(){ //局部render
    return (
      <div className="red">
        <span>{this.state.number}</span>
        <button onClick={this.add.bind(this)}>+</button>
        <button onClick={this.minus.bind(this)}>-</button>
        <span>{this.props.name}</span>
      </div>
      )
  }
}

render()
function render(){
  ReactDOM.render(
    <App />,
    document.querySelector("#root")
   )
}
```
