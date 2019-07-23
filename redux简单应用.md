```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <script src="https://cdn.bootcss.com/redux/4.0.4/redux.min.js"></script>
  <title>JS Bin</title>
</head>
<body>
  <div id='app'>
    
  </div>
  <script>
    function add1(){
      store.dispatch({type:'add',payload:1}) //1 首先派发一个事件
    }
    function add2(){
      store.dispatch({type:'add',payload:2})
    }
    function addIf(){
      var oldState=store.getState()
      if(oldState%2===1){
        store.dispatch({type:'add',payload:1})
      }
    }
    function addAsync(){
      setTimeout(()=>{
        store.dispatch({type:'add',payload:1})
      },2000)
    }
    function render(store){
      var app=document.querySelector('#app')
      app.innerHTML=`
        <div>
          你点击了<span id="value">${store.getState()}</span>次
          <div>
          <button id='add1' onclick='add1()'>+1</button>
          <button id='add2' onclick='add2()'>+2</button>
          <button id='add1IfOdd' onclick='addIf()'>如果是单数就+1</button>
          <button id='add1After2Sec' onclick='addAsync()'>两秒钟后+1</button>
        </div>
      </div>
    `
    }
    
    function stateChanger(state,action){
      if(state===undefined){
        return 0
      }else{
        if(action.type==='add'){
          var newState=state+action.payload
          return newState
        }else{
          return state //2 根据操作生成新的state，触发一个事件
        }
      }
    }
    var store=Redux.createStore(stateChanger)
    render(store)
    
    store.subscribe(()=>{
      render(store)//3 接收到事件，重新render
    })
  </script>
</body>
</html>
```
