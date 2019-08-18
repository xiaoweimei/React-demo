1. 一个关于父子通信的例子
- html
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
- jsx
```
class App extends React.Component{
  constructor(){
    super()
    this.state={
      message:'你好'
    }
  }
  changeMessage(){
    this.setState({
      message:'真好'
    })
  }
  render(){
    return (
      <div>hi
        <Foo message={this.state.message} fn={this.changeMessage.bind(this)}/>
      </div>
    )
  }
}
function Foo(props){
  return (
    <p>我的messenge是{props.message}
      <button onClick={props.fn}>click</button>
    </p>
  )
}
ReactDOM.render(<App/>,document.querySelector('#root'))
```
