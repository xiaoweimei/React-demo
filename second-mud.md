1. 父子通信
html
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <script src="https://cdn.bootcss.com/react/16.8.6/umd/react.production.min.js"></script>
  <script src="https://cdn.bootcss.com/react-dom/16.8.6/umd/react-dom.production.min.js"></script>
  <title>JS Bin</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
```
css
```
.header{
  display:flex;
  justify-content:center;
}
.track{
  border-bottom:1px solid black;
}
*{margin:0;padding:0;box-sizing:border-box}
/* .player{
  transition: 2s all linear;
} */

body{
  padding:40px;
}
```
jsx
```
class App extends React.Component{
  constructor(){
    super()
    this.state={
      result1:0,
      result2:0
    }
    this.t0=new Date()
  }
  success1(){
    console.log('兔子跑完了，用时')
    let r1 = new Date()-this.t0
    this.setState({
      result1: r1
    })
  }
  success2(){
    console.log('乌龟跑完了，用时')
    let r2 = new Date()-this.t0
    this.setState({
      result2: r2
    })
  }
  render(){
    return (
      <div>
        <div class='header'>
          <Time1 result={this.state.result1}/>
          <Judge />
          <Time2 result={this.state.result2}/>
        </div>
        <Track1 success={this.success1.bind(this)}/>
        <Track2 success={this.success2.bind(this)}/>
      </div>
    )
  }
}
function Time1(props){
  return (
    <div>
      <h2>兔子用时</h2>
      <div>{props.result}</div>
    </div>
  )
}
function Time2(props){
  return (
    <div>
      <h2>乌龟用时</h2>
      <div>{props.result}</div>
    </div>
  )
}
function Judge(){
  return (
    <div>裁判</div>
  )
}

class Track1 extends React.Component{
  constructor(){
    super()
    let n=0
    this.state={
      style:{
        transform:`translateX(${n}%)`
      }
    }
    let timeId=setInterval(()=>{
      n+=10
      this.setState({
        style:{
          transform:`translateX(${n}%)`
        }
      })
      if(n>=100){
        window.clearInterval(timeId)
        this.props.success()
      }
    },1000)
  }
  render(){
    return (
      <div>
        <div class='player' style={this.state.style}>兔子</div>
        <div class="track"></div>
      </div>
    )
  }
}
class Track2 extends React.Component{
  constructor(){
    super()
    let n=0
    this.state={
      style:{
        transform:`translateX(${n}%)`
      }
    }
    let timerId=setInterval(()=>{
      n+=5
      this.setState({
        style:{
          transform:`translateX(${n}%)`
        }
      })
      if(n>=100){
        window.clearInterval(timerId)
        this.props.success()
      }
    },1000)
  }
  render(){
    return (
      <div>
        <div class='player' style={this.state.style}>乌龟</div>
        <div class="track"></div>
      </div>
    )
  }
}
ReactDOM.render(<App />,document.querySelector('#root'))
```
2. 祖孙通信
html
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <script src="https://cdn.bootcss.com/react/16.8.6/umd/react.production.min.js"></script>
  <script src="https://cdn.bootcss.com/react-dom/16.8.6/umd/react-dom.production.min.js"></script>
  <title>JS Bin</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
```
css
```
.header{
  display:flex;
  justify-content:center;
}
.track{
  border-bottom:1px solid black;
}
*{margin:0;padding:0;box-sizing:border-box}
/* .player{
  transition: 2s all linear;
} */

body{
  padding:40px;
}
.playground{
  border: 1px solid black;
  background:green;
}
```
jsx
```
class App extends React.Component{
  constructor(){
    super()
    this.state={
      result1:0,
      result2:0
    }
    this.t0=new Date()
  }
  success1(){
    console.log('兔子跑完了，用时')
    let r1 = new Date()-this.t0
    this.setState({
      result1: r1
    })
  }
  success2(){
    console.log('乌龟跑完了，用时')
    let r2 = new Date()-this.t0
    this.setState({
      result2: r2
    })
  }
  render(){
    return (
      <div>
        <div class='header'>
          <Time1 result={this.state.result1}/>
          <Judge />
          <Time2 result={this.state.result2}/>
        </div>
        <Playground success1={this.success1.bind(this)}
                    success2={this.success1.bind(this)}/>
      </div>
    )
  }
}
function Time1(props){
  return (
    <div>
      <h2>兔子用时</h2>
      <div>{props.result}</div>
    </div>
  )
}
function Time2(props){
  return (
    <div>
      <h2>乌龟用时</h2>
      <div>{props.result}</div>
    </div>
  )
}
function Judge(){
  return (
    <div>裁判</div>
  )
}
function Playground(props){
  let success1=props.success1
  let success2=props.success2
   return(
     <div class="playground">
       <Track1 success={success1}/>
       <Track2 success={success2}/>
     </div>
   )
}
class Track1 extends React.Component{
  constructor(){
    super()
    let n=0
    this.state={
      style:{
        transform:`translateX(${n}%)`
      }
    }
    let timeId=setInterval(()=>{
      n+=10
      this.setState({
        style:{
          transform:`translateX(${n}%)`
        }
      })
      if(n>=100){
        window.clearInterval(timeId)
        this.props.success()
      }
    },1000)
  }
  render(){
    return (
      <div>
        <div class='player' style={this.state.style}>兔子</div>
        <div class="track"></div>
      </div>
    )
  }
}
class Track2 extends React.Component{
  constructor(){
    super()
    let n=0
    this.state={
      style:{
        transform:`translateX(${n}%)`
      }
    }
    let timerId=setInterval(()=>{
      n+=5
      this.setState({
        style:{
          transform:`translateX(${n}%)`
        }
      })
      if(n>=100){
        window.clearInterval(timerId)
        this.props.success()
      }
    },1000)
  }
  render(){
    return (
      <div>
        <div class='player' style={this.state.style}>乌龟</div>
        <div class="track"></div>
      </div>
    )
  }
}
ReactDOM.render(<App />,document.querySelector('#root'))
```
