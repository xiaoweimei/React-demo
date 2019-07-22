- HTML
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
- CSS
```
.root{
  display:flex;
  justify-content:center;
  align-items:center
}
.papa{
  border:1px solid grey;
  padding:10px;
  margin:10px;
}
.son{
  border:1px solid red;
  padding:10px;
  margin:10px 0
}
```
- JavaScript
```
var money={
  amount:100000
}
var fnLists={}
var eventHub={
  trigger(eventName,data){
    let fnList=fnLists[eventName]
    if(!fnList){return}
    for(let i=0;i<fnList.length;i++){
      fnList[i](data)
    }
  },
  on(eventName,fn){
    if(!fnLists[eventName]){
      fnLists[eventName]=[]
    }
    fnLists[eventName].push(fn)
  }
}

var x={
  init(){
    eventHub.on('我想花钱',function(data){
      money.amount-=data
      render()
    })
  }
}
x.init()
class App extends React.Component{
  constructor(){
    super()
    this.state={
      money:money
    }
  }
  render(){
    return (
      <div className='root'>
        <BigPapa money={this.state.money}/>
        <YoungPapa money={this.state.money}/>
      </div>
    )
  }
}
class BigPapa extends React.Component{
  constructor(){
    super()
  }
  render(){
    return (
      <div className='papa'>大爸 {this.props.money.amount}
        <Son1 money={this.props.money}/>
        <Son2 money={this.props.money}/>
      </div>
    )
  }
}
class YoungPapa extends React.Component{
  constructor(){
    super()
  }
  render(){
    return ( 
      <div className='papa'>二爸 {this.props.money.amount}
        <Son3 money={this.props.money}/>
        <Son4 money={this.props.money}/>
      </div>
    )
  }
}
class Son1 extends React.Component{
  constructor(){
    super()
  }
  render(){
    return (
      <div className='son'>儿子1 {this.props.money.amount}</div>
    )
  }
}
class Son2 extends React.Component{
  constructor(){
    super()
  }
  x(){
    eventHub.trigger('我想花钱',100)
  }
  render(){
    return (
      <div className='son'>儿子2 {this.props.money.amount}
        <button onClick={()=>this.x()}>消费</button>
      </div>
    )
  }
}
class Son3 extends React.Component{
  constructor(){
    super()
  }
  render(){
    return (
      <div className='son'>儿子3 {this.props.money.amount}</div>
    )
  }
}
class Son4 extends React.Component{
  constructor(){
    super()
  }
  render(){
    return (
      <div className='son'>儿子4 {this.props.money.amount}</div>
    )
  }
}
function render(){
  ReactDOM.render(<App/>,document.querySelector('#root'))
}
render()
```
