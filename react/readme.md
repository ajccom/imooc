大家好 欢迎来到慕课网，我是老白，今天让老白和大家一起了解一下 ReactJs。

1.课程介绍
  - Hello World 实例
  - React JSX 语法
  - React 的 props 和 state
  - React 的诞生 - 2013年3.30号发布 0.3.0 - 15.4.1
    没有适合 Facebook 的前端框架，而且 facebook 的工程师认为，前端开发工作中最主要的就是操作 View 层的内容，
    所以把 View 层处理好才是当务之急。
  前置知识
  JS HTML CSS 基础
  目标 
  了解和掌握使用 React 构建页面
  
  课程目标、学习内容、案例描述、场景、用途、重要性、实用性等
  
2.React 安装与使用
  - React 的安装
  
  <script src="https://unpkg.com/react@15/dist/react.js"></script>
  <script src="https://unpkg.com/react-dom@15/dist/react-dom.js"></script>
  
  - hello world 示例 
  http://codepen.io/gaearon/pen/ZpvBNJ?editors=1010
  
  官方工具：create-react-app
  
  延伸：NPM、Webpack、Babel、ES6
  
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
    · 事件绑定
  - 标签（JSX Type）的大小写区别
    · babel 验证  http://babeljs.io/repl/#?babili=false&evaluate=true&lineWrap=false&presets=es2015%2Creact%2Cstage-0&code=function%20hello()%20%7B%0A%20%20return%20%3CSiv%3EHello%20world!%3C%2FSiv%3E%3B%0A%7D
      1) babel 是一款插件式的语法转换工具，我们可以通过 babel 进行 JSX 语法到 ES 语法的转换
    · 属性的点
    · 标签的变量化，需要指定一个大写字母开头的名字
  
  延伸：AST 语法树
  
4.React Component - props & state 
  - props 的使用
     
      	const props = {firstName: 'Ben', lastName: 'Hector'};
      	return <Greeting {...props} />;
    
    · props.children 表示子组件
    · ref
  - state 的使用
    · setState
  - props 与 state 的区别
    · props 表述外部状态，只读
    · state 表示内部状态，可修改
    · 比如一个下拉列表，下拉列表的选项一般由外部状态决定，而被用户选中的项的值则可以用内部状态表示
    · stateless component 只负责渲染数据的无状态组件
      官方建议：
        1) Prefer using stateless functional components whenever possible.
        2) Components that don't use state are better to be written as simple pure functions.
    var Aaa = React.createClass({
    
    }) 
    
    class Aaa extend Component {
    
    }
    
    function Aaa (props) {
      return (
        <div>{props.name}</div>
      )
    }
    
  延伸：FP 函数式编程

5.React 生命周期函数
  Mounting：已插入真实 DOM
  Updating：正在被重新渲染
  Unmounting：已移出真实 DOM
  配合 will & did
  
  componentWillMount()
  componentDidMount()
  componentWillUpdate(object nextProps, object nextState)
  componentDidUpdate(object prevProps, object prevState)
  componentWillUnmount()
  
  componentWillReceiveProps(object nextProps)：已加载组件收到新的参数时调用
  shouldComponentUpdate(object nextProps, object nextState)：组件判断是否重新渲染时调用
  
  延伸：shouldComponentUpdate + Immutable.js
  
6.React 开发实践

key 帮助 React 确定哪些项改变、增加和删除
key 要求稳定、不重复
```
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
```
/****- React 起步应用
    · Hello World 示例
  ```
  npm install -g create-react-app
  create-react-app hello-world
  cd hello-world
  npm start
  ```
  ****/
  /****- React 的特点 
    · 给我们带来了组件化方式的开发体验
    · Virtual DOM 带来了服务器直出
      1) 跨平台的界面构建能力
  ****/
  /****
  var Counter = React.createClass({
        getInitialState: function () {
          return { count: 0 };
        },
        handleClick: function () {
          this.setState({
            count: this.state.count + 1,
          });
        },
        render: function () {
          return (
            <button onClick={this.handleClick}>
              Click me! Number of clicks: {this.state.count}
            </button>
          );
        }
      });
      ReactDOM.render(
        <Counter />,
        document.getElementById('container')
      );
  ****/
  
  
  
   react 课程提纲
 
 
 1.第一章设计统一为课程介绍（课程目标、学习内容、案例描述、场景、用途、重要性、实用性等）、效果展示、（把案例的重点功能进行展示，让用户清楚最后的实现效果）。功能技术分析（分析重点功能或模块使用的相关技术）、前置知识（让用户清楚学习该课程要具备的知识）、课程重难点（分析本案例重点和难点部分）、课程安排（描述整个课程安排，让用户知道接下来如何一步一步有计划的学习）、学习建议（针对本课程的章节、可以给用户一些学好对应章节的学习建议）
2.对于案例课程，在小节里面要详细体现案例每一步的实现思路。（实现思路最好写到PPT中，时不时的给用户展示以让用户在每个时间点都知道老师要做什么）
3.章节说明，要写清楚本章或节讲解的内容是什么，掌握的知识点是什么，达到一个什么样的学习效果（每次敲完代码要给用户看到这段代码实现了的效果）。
4、最后一章设计统一为课程回顾与总结（带着用户把整个课程回顾一遍，尤其是重难点，技术点，最后总结经验、心得以及扩展建议等）
===================

====================
====================
```
===================
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Collage Town</title>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
  </head>
  <body>
    <div class="town"></div>
    <script src="../../build/react.js"></script>
    <script src="../../build/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.24/browser.min.js"></script>
    <style>
      ul, li {padding: 0; margin: 0; list-style: none}
      .collage {margin: 20px; text-align: center; border: 1px solid #ddd}
      .faculty {width: 100px; height: 100px; display: inline-block; margin: 20px; text-align: center; line-height: 100px; border: 1px solid #ddd; overflow: hidden; transition: all .3s ease-in}
      .off .faculty {height: 0px; border: 1px solid #fff; margin: 0px}
    </style>
    <script type="text/babel">
      function Faculty (props) {
        return (
          <div className="faculty" title={props.name}>{props.name}</div>
        )
      }
      
      var Collage = React.createClass({
        getInitialState: function () {
          return {
            status: 'off'
          }
        },
        toggle: function () {
          this.setState({
            status: 'off' === this.state.status ? 'on' : 'off'
          })
        },
        render: function () {
          return (
            <li className={'collage ' + this.state.status} ref="collage">
              <h3 onClick={this.toggle}>{this.props.name}</h3>
              {
                (this.props.faculties || []).map(function (faculty, i) {
                  return <Faculty name={faculty} key={i}/>
                })
              }
            </li>
          )
        }
      })
      
      function CollageTown (props) {
        return (
          <div>
            <h2>{props.name}</h2>
            <ul>
              {
                (props.collages || []).map(function (collage, i) {
                  return <Collage name={collage.name} faculties={collage.faculties} key={i} />
                })
              }
            </ul>
          </div>
        )
      }
      
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

===============
==============

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>React Lifecycle Function</title>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
  </head>
  <body>
    <div class="town"></div>
    <script src="../../build/react.js"></script>
    <script src="../../build/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.24/browser.min.js"></script>
    <style>
      ul, li {padding: 0; margin: 0; list-style: none}
    </style>
    <div class="div"></div>
    <script type="text/babel">
      var List = React.createClass({
        getInitialState: function () {
          return {
            length: 3
          }
        },
        componentWillMount: function () {
          console.log('will mount')
        },
        componentDidMount: function () {
          console.log('did mount')
          setInterval(() => {
            var l = this.state.length + 3
            this.setState({
              length: l
            })
          }, 3000)
        },
        shouldComponentUpdate: function (nextProps, nextState, obj) {
          console.log(this.state, nextState)
          return true
        },
        render: function () {
          return (
            <ul>
              {
                new Array(this.state.length).fill(0).map(function (v, i) {
                  return (<li key={i}>item {i}</li>)
                })
              }
            </ul>
          )
        },
        componentWillUpdate: function () {
          console.log('will update')
        },
        componentDidUpdate: function () {
          console.log('did update')
        }
      })
     
      ReactDOM.render(<List />, document.querySelector('.div'))
    </script>
  </body>
</html>
===========

===========props


<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Props.children</title>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
  </head>
  <body>
    <div class="town"></div>
    <script src="../../build/react.js"></script>
    <script src="../../build/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.24/browser.min.js"></script>
    <style>
      ul, li {padding: 0; margin: 0; list-style: none}
      .tv {width: 100px; height: 50px; background: red}
      .table {width: 300px; height: 300px; background: gray}
      .chair {width: 100px; height: 100px; background: blue}
    </style>
    <div class="room"></div>
    <script type="text/babel">
      
      var Room = React.createClass({
        componentDidMount: function () {
          console.log(this.refs)
          window.door = this.refs.door
        },
        render: function () {
          return (
            <ul>
              {
                this.props.children.map(function (child) {
                  return child
                })
              }
              <Door ref="door" />
            </ul>
          )
        }
      })
      
      var Door = React.createClass({
        render: function () {
          return (<div ref="dom" className="door">DOOR</div>)
        }
      })
      
      function TV () {
        return <div className="tv" />
      }
      
      function Table () {
        return <div className="table" />
      }
      
      function Chair () {
        return <div className="chair" />
      }
      
      ReactDOM.render((<Room>
        <TV />
        <Table />
        <Chair />
      </Room>), document.querySelector('.room'))
    </script>
  </body>
</html>

==========================

==========================
hello world

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Hello World</title>
  </head>
  <body>
    <div id="div"></div>
    <script src="../../build/react.js"></script>
    <script src="../../build/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.24/browser.min.js"></script>
    <script type="text/babel">
      function HelloWorld () {
        return (<h1>Hello World</h1>)
      }
      
      ReactDOM.render(<HelloWorld />, document.getElementById('div'))
    </script>
  </body>
</html>


=====================
```
