大家好 欢迎来到慕课网，我是老白，今天让老白和大家一起了解一下 ReactJs。

1.课程介绍
  - Hello World 实例
  - React JSX 语法
  - React 的 props 和 state
  - React 的诞生 - 2013年3.30号发布 0.3.0 - 15.4.1
  前置知识
  
  课程目标、学习内容、案例描述、场景、用途、重要性、实用性等
  
2.React 安装与使用
  - React 的安装
  
  <script src="https://unpkg.com/react@15/dist/react.js"></script>
  <script src="https://unpkg.com/react-dom@15/dist/react-dom.js"></script>
  
  - hello world 示例 
  http://codepen.io/gaearon/pen/ZpvBNJ?editors=1010
  
3.JSX 介绍  
  - JSX 是什么
  - JSX 与原生 JS 语法编写相比所具备的优势
    · PPT 展示比较
    · 精简大段代码，隐藏内部逻辑
  - JSX 中的表达式
    · {} 号界定符
    · 样式设置的注意点
      1) 使用 JS 的样式名
      2) 使用一个对象包裹所有样式属性，如果不熟悉的话，老白教大家一个简单方法，去除连字符变成驼峰命名 “transition-timing-function”
  - 标签（JSX Type）的大小写区别
    · babel 验证  http://babeljs.io/repl/#?babili=false&evaluate=true&lineWrap=false&presets=es2015%2Creact%2Cstage-0&code=function%20hello()%20%7B%0A%20%20return%20%3CSiv%3EHello%20world!%3C%2FSiv%3E%3B%0A%7D
      1) babel 是一款插件式的语法转换工具，我们可以通过 babel 进行 JSX 语法到 ES 语法的转换
    · 属性的点
    · 标签的变量化，需要指定一个大写字母开头的名字
  
4.React Component - props & state 
  - props 的使用
	```
      	const props = {firstName: 'Ben', lastName: 'Hector'};
      	return <Greeting {...props} />;
    	```
  - state 的使用
  - props 与 state 的区别
    · props 表述外部状态
    · state 表示内部状态
    · 比如一个下拉列表，下拉列表的选项一般由外部状态决定，而被用户选中的项的值则可以用内部状态表示
    · stateless component 只负责渲染数据的无状态组件
      官方建议：
        1) Prefer using stateless functional components whenever possible.
        2) Components that don't use state are better to be written as simple pure functions.
 

5.React 生命周期函数
  

6.React 开发实践

key 帮助 React 确定哪些项改变、增加和删除
key 要求稳定、不重复

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Collage Town</title>
  </head>
  <body>
    <div class="town"></div>
    <script src="../../build/react.js"></script>
    <script src="../../build/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.24/browser.min.js"></script>
    <style>
      ul, li {padding: 0; margin: 0; list-style: none}
      .collage {margin: 20px; text-align: center; border: 1px solid #ddd}
      .faculty {width: 100px; height: 100px; display: inline-block; margin: 20px; text-align: center; line-height: 100px; border: 1px solid #ddd}
    </style>
    <script type="text/babel">
      var Faculty = React.createClass({
        render: function () {
          return (
            <div className="faculty" title={this.props.name}>{this.props.name}</div>
          )
        }
      })
    
      var Collage = React.createClass({
        render: function () {
          return (
            <li className="collage">
              <h3>{this.props.name}</h3>
              {
                (this.props.faculties || []).map(function (faculty, i) {
                  return <Faculty name={faculty} key={i}/>
                })
              }
            </li>
          )
        }
      })
      
      var CollageTown = React.createClass({
        render: function () {
          return (
            <div>
              <h2>{this.props.name}</h2>
              <ul>
                {
                  (this.props.collages || []).map(function (collage, i) {
                    return <Collage name={collage.name} faculties={collage.faculties} key={i} />
                  })
                }
              </ul>
            </div>
          )
        }
      })
      
      var collages = [
        {
          name: '上海海洋大学',
          faculties: ['信息学院', '金融学院', '海洋学院']
        },
        {
          name: '上海海事大学',
          faculties: ['国际贸易学院', '外国语学院', '食品安全学院']
        },
        {
          name: '上海应用技术大学',
          faculties: ['工程学院', '建筑学院', '计算机学院']
        },
      ]
      ReactDOM.render(<CollageTown name="上海南汇大学城" collages={collages} />, document.querySelector('.town'))
    </script>
  </body>
</html>
