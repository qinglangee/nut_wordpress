# reactjs 教程项目

## 目标
创建一个 tic-tac-toe 游戏，类似占茅坑的游戏，两方在九宫格中落子，先连成三个的赢．
最终结果在 ~/temp/react/my-app中，　或者网上的在　https://codepen.io/gaearon/pen/gWWZgR?editors=0010

## 项目准备
用reactjs的工具安装，需要nodejs,还需要先安装它的工具．这个过程有可能需要翻墙，也可能不需要，看node源能不能访问到了．(装完目录就162M，这也太TM肥了)
```
npm install -g create-react-app
create-react-app my-app
```
完成后进入目录，默认的目录结构中,下面这两个文件是不能改名或移动的，其它的可以修改．
```
public/index.html is the page template;
src/index.js is the JavaScript entry point.
```
初始化游戏内容：把src/目录下内容全删掉，添加`index.css`和`index.js`, 稍后启动时命令是`npm start`,现在先不谈．
`index.css`就先不管了，来看下`index.js`的内容
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {/* TODO */}
      </button>
    );
  }
}

class Board extends React.Component {
  renderSquare(i) {
    return <Square />;
  }

  render() {
    const status = 'Next player: X';

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}

class Game extends React.Component {
  render() {
    return (
      <div className="game">
        <div className="game-board">
          <Board />
        </div>
        <div className="game-info">
          <div>{/* status */}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
}

// ========================================

ReactDOM.render(
  <Game />,
  document.getElementById('root')
);

```

`npm start`　运行就是可以查看初始界面了．

## 打包发布
完成后打包发布 `npm run build`, 生成的`build`目录就是可发布的静态目录．

## 组件 React.Component
react 主要用来构建界面，界面由各级 React.Component　组成．  
Component 接收 props 参数，在render()方法在渲染页面结构．render()方法中主要使用JSX，它是js生成html代码的一种简化语言．  
通常render()返回的就是一个`React element`．类似于
```
return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
```
也可以用`JSX`形式的`React element`, *所有方法都可以返回React element, 都可以用在render()方法中*
```
inEle(){
    return(
        <span>abc</span>
    );
}
```
组件可以写成多行，但需要放到括号中．（js会在return后插入分号，造成错误）
```
return (
  <Square
    value={this.state.squares[i]}
    onClick={() => this.handleClick(i)}
  />
);
```
## 向组件中传数据和使用数据
向Square组件中传入值 `return <Square value={i} />;`

在Square组件中使用值
```
<button className="square">
  {this.props.value}
</button>
```
## 设置onclick函数
传入值应该是一个函数定义而不是一个函数调用
```
<button className="square" onClick={() => this.setState({value: 'X'})}>
  {this.props.value}
</button>
```
## 构造函数
在javascript class中，子类的构造函数必须使用`super()`显式地调用父类的构造函数．  
state应该被当作组件的私有数据
```
class Square extends React.Component {
  constructor() {
    super();
    this.state = {
      value: null,
    };
  }
  render(){
      // ....
  }
}
```
## 更新state
`this.setState(state)` 会合并更新　`Component`　的state, 参数中有的会更新，参数中没有的，会保留原来的值．  
*组件的状态的属性应该都是不可变的值，修改时应该整个替换而不是直接修改*，基于以下几点：
1. 便于实现 undo/redo
2. 便于追踪修改，对于可变量，需要比较整个对象树，而对于不可变量，只要比较是不是同一个引用就可以了
3. 决定何时重新渲染．不可变量更容易判断是否有改变，是否需要重新渲染

## 状态集中
在 react 应用中，所有的状态都应该存储在最上层的组件中，它分发给自己的子组件，这样便于状态管理，所有子组件之间及与父组件之间状态都是同步的．  
当状态存储在父组件中以后，子组件就不能修改状态，因为状态是父组件的私有数据．这就需要父组件提供一个修改状态的方法传给子组件，子组件在对应的事件中调用父组件提供的方法．这些子组件叫做 `controlled components`．   
所谓`controlled components`只不过是带有`onXXX`事件处理方法的组件．在`controlled components`中每个状态的改变都有相应的处理函数，便于修改内容或验证数据之类的．

传入值和方法：  `return <Square value={this.state.squares[i]}　onClick={() => this.handleClick(i)}　/>;`

调用：
```
return (
  <button className="square" onClick={() => this.props.onClick()}>
    {this.props.value}
  </button>
);
```

## 功能组件
除了render()方法和props不需要其它方法的组件可以简化为一个方法
```
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```
## 列表元素的 keys
当　React 渲染一个数组/列表中的元素时，会根据它的key判断元素有没有被修改，所以最好在元素中为它们指定key.
`<li key={user.id}>{user.name}: {user.taskCount} tasks left</li>`
如果不指定的话，默认使用index作为key. *不建议使用index作为key,因为如果改变元素顺序或在列表中间增减元素会渲染错误*，直接设置　`key={i}` 跟默认设置是一样的．  
key 只需要在同一个列表中不重复就可以了，不需要全局唯一．











