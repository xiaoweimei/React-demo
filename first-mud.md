### 写一个 React 函数组件，要求如下：
1. 接受 name 和 age 
2. 作为 props在 div 里展示 name 和 age
- function写法
```
function Box(obj){
  return (
    <div>
      {obj.name}{obj.age}
    </div>
    )
}
```
- class写法
```
class Box extends React.Component{
  constructor(props){
    super(props)
  }
  render(){ //局部render
    return (
      <div>
        <span>{this.props.name}</span>
        <span>{this.props.age}</span>
      </div>
      )
  }
}
```
