- HTML
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <script src="https://cdn.bootcss.com/react/16.8.6/umd/react.production.min.js"></script>
  <script src="https://cdn.bootcss.com/react-dom/16.8.6/umd/react-dom.production.min.js"></script>
  <script src="https://cdn.bootcss.com/redux/4.0.4/redux.min.js"></script>
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
let createStore=Redux.createStore
let reducers=(state,action)=>{
  state=state||{
    money:{amount:100000}
  }
  switch(action.type){
    case '我想花钱':
      return {
        money:{
          amount:state.money.amount-action.payload
        }
      }
    case 'DECREMENT':
      return state-1
    default:
      return state
  }
}
const store=createStore(reducers)

class App extends React.Component{
  constructor(){
    super()
  }
  render(){
    return (
      <div className='root'>
        <BigPapa money={this.props.store.money}/>
        <YoungPapa money={this.props.store.money}/>
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
    //action
    store.dispatch({type:'我想花钱',payload:100})
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
  ReactDOM.render(<App store={store.getState()}/>,document.querySelector('#root'))
}
render()
store.subscribe(render)
```
