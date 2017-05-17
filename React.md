## React.js

http://www.runoob.com/react/react-tutorial.html

React 是一个用于构建用户界面的 JAVASCRIPT 库。

React主要用于构建UI，很多人认为 React 是 MVC 中的 V（视图）。

React 起源于 Facebook 的内部项目，用来架设 Instagram 的网站，并于 2013 年 5 月开源。
React 拥有较高的性能，代码逻辑非常简单，越来越多的人已开始关注和使用它。

---
##1、React 特点
1.**声明式设计** −React采用声明范式，可以轻松描述应用。

2.**高效** −React通过对DOM的模拟，最大限度地减少与DOM的交互。

3.**灵活** −React可以与已知的库或框架很好地配合。

4.**JSX** − JSX 是 JavaScript 语法的扩展。React 开发不一定使用 JSX ，但我们建议使用它。

5.**组件** − 通过 React 构建组件，使得代码更加容易得到复用，能够很好的应用在大项目的开发中。

6.**单向响应的数据流** − React 实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单。

#一、JSX
##1、JavaScript 表达式
我们可以在 JSX 中使用 JavaScript 表达式。表达式写在花括号 {} 中。实例如下：
React 实例

	ReactDOM.render(
	    <div>
	      <h1> {1+1} </h1>
	    </div>
    	,
   	    document.getElementById('example')
	);

##2、三元运算符

在 JSX 中不能使用 if else 语句，但可以使用 conditional (三元运算) 表达式来替代。以下实例中如果变量 i 等于 1 浏览器将输出 true, 如果修改 i 的值，则会输出 false.
React 实例

	ReactDOM.render(
		<div>
			<h1>{i == 1 ? 'True!' : 'False'}</h1>
		</div>
    	,
		document.getElementById('example')
	);

##3、注释
1、在标签内部的注释需要花括号

2、在标签外的的注释不能使用花括号

	ReactDOM.render(
    	/*注释 */
    	<h1>孙朝阳 {/*注释*/}</h1>,
    	document.getElementById('example')
	);
##4、数组
JSX 允许在模板中插入数组，数组会自动展开所有成员：React 实例
	
	var arr = [
 		 <h1>菜鸟教程</h1>,
 		 <h2>学的不仅是技术，更是梦想！</h2>,
	];
	ReactDOM.render(
 		 <div>{arr}</div>,
 	 	 document.getElementById('example')
	);

##5、HTML 标签 vs. React 组件
React 可以渲染 HTML 标签 (strings) 或 React 组件 (classes)。

1、要渲染 HTML 标签，只需在 JSX 里使用小写字母的标签名。
	
	var myDivElement = <div className="foo" />;
	ReactDOM.render(myDivElement, document.getElementById('example'));

2、要渲染 React 组件，只需创建一个大写字母开头的本地变量。

	var MyComponent = React.createClass({/*...*/});
	var myElement = <MyComponent someProperty={true} />;
	ReactDOM.render(myElement, document.getElementById('example'));

React 的 JSX 使用大、小写的约定来区分本地组件的类和 HTML 标签。

注意:***由于 JSX 就是 JavaScript，一些标识符像 class 和 for 不建议作为 XML 属性名。作为替代，React DOM 使用 className 和 htmlFor 来做对应的属性。***


##6、组件标签只能包含一个顶级标签
代码中嵌套多个 HTML 标签，需要使用一个标签元素包裹它
1.错误例子：

	ReactDOM.render(
 	 	<h1>这是错误的例子</h1>
  		<span>假设这里是标题下面的内容</span>,
 		document.getElementById("example")
	);

2.正确例子：

	ReactDOM.render(
  		<section>
   	 		<h1>这是正确的例子</h1>
   			<span>假设这里是标题下面的内容</span>
  		</section>,
  		document.getElementById("example")
	);

#二、React 组件

我们将讨论如何使用组件使得我们的应用更容易来管理。接下来我们封装一个输出 "Hello World！" 的组件，组件名为 HelloMessage：

	var HelloMessage = React.createClass({
  		render: function() {
   			return <h1>Hello World！</h1>;
 		}
	});
 
	ReactDOM.render(
 		<HelloMessage />,
  		document.getElementById('example')
	);
##1、实例解析：
+ **React.createClass**  方法用于生成一个组件类 HelloMessage。

+ **&lt;HelloMessage />**  实例组件类并输出信息。

**注1：原生 HTML 元素名以小写字母开头，而自定义的 React 类名以大写字母开头，比如 HelloMessage 不能写成 helloMessage。***

**注2：组件类只能包含一个顶层标签，否则也会报错。**

##2、向组件传递参数

如果我们需要向组件传递参数，可以使用 **this.props** 对象,实例如下：

	var HelloMessage = React.createClass({
  		render: function() {
    		return <h1>Hello {this.props.name}</h1>;
  		}
	});
 
	ReactDOM.render(
  		<HelloMessage name="Runoob" />,
  		document.getElementById('example')
	);

以上实例中 name 属性通过 this.props.name 来获取。

**注意：在添加属性时， class 属性需要写成 className ；for 属性需要写成 htmlFor ，这是因为 class 和 for 是 JavaScript 的保留字。**

##3、复合组件
我们可以通过创建多个组件来合成一个组件，即把组件的不同功能点进行分离。

以下实例我们实现了输出网站名字和网址的组件：

实例中 WebSite 组件使用了 Name 和 Link 组件来输出对应的信息，也就是说 WebSite 拥有 Name 和 Link 的实例。
	
	/* 复合组件 */
	var WebSite = React.createClass({
  		render: function() {
    		return (
      			<div>
        			<Name name={this.props.name} />
        			<Link site={this.props.site} />
      			</div>
    		);
  		}
	});
 
	/* 单功能组件1 */
	var Name = React.createClass({
  		render: function() {
    		return (
      			<h1>{this.props.name}</h1>
    		);
  		}
	});
 
	/* 单功能组件2 */
	var Link = React.createClass({
  		render: function() {
    		return (
      			<a href={this.props.site}>
	        		{this.props.site}
      			</a>
    		);
  		}
	});
 
	ReactDOM.render(
  		<WebSite name="菜鸟教程" site=" http://www.runoob.com" />,
  		document.getElementById('example')
	);

#三、React State（状态）
React 把组件看成是一个状态机（State Machines）。通过与用户的交互，实现不同状态，然后渲染 UI，让用户界面和数据保持一致。

React 里，只需更新组件的 state，然后根据新的 state 重新渲染用户界面（不要操作 DOM）。

以下实例中创建了 LikeButton 组件，**getInitialState** 方法用于定义初始状态，也就是一个对象，这个对象可以通过 **this.state** 属性读取。当用户点击组件，导致状态变化，**this.setState** 方法就修改状态值，每次修改以后，自动调用 this.render 方法，再次渲染组件。

	<script type="text/babel">
      	var LikeButton = React.createClass({
        	getInitialState: function() {
         		return {liked: false};
	        },

	        handleClick: function(event) {
		        this.setState({liked: !this.state.liked});
	        },

	        render: function() {
	            var text = this.state.liked ? '喜欢' : '不喜欢';
                return (
      		      <p onClick={this.handleClick}>
      		        你<b>{text}</b>我。点我切换状态。
      		      </p>
      		    );
      	  }
      });

      ReactDOM.render(
        	<LikeButton />,
        	document.getElementById('example')
      );
    </script>

#四、React Props
**state 和 props 主要的区别在于 props 是不可变的，而 state 可以根据与用户交互来改变。**

这就是为什么有些容器组件需要定义 state 来更新和修改数据。 而子组件只能通过 props 来传递数据。

##1、使用props
实例中 name 属性通过 this.props.name 来获取。

	var HelloMessage = React.createClass({
  		render: function() {
    		return <h1>Hello {this.props.name}</h1>;
  		}
	});
 
	ReactDOM.render(
  		<HelloMessage name="Runoob" />,
  		document.getElementById('example')
	);

##2、默认 Props
你可以通过 getDefaultProps() 方法为 props 设置默认值，实例如下：
	
	var HelloMessage = React.createClass({
  		getDefaultProps: function() {
    		return {
      			name: 'Runoob'
    		};
  		},
  
		render: function() {
    		return <h1>Hello {this.props.name}</h1>;
  		}
	});
 
	ReactDOM.render(
  		<HelloMessage />,
  		document.getElementById('example')
	);

##3、State 和 Props
以下实例演示了如何在应用中组合使用 state 和 props 。我们可以在父组件中设置 state， 并通过在子组件上使用 props 将其传递到子组件上。在 render 函数中, 我们设置 name 和 site 来获取父组件传递过来的数据。

	var WebSite = React.createClass({
  		getInitialState: function() {
    		return {
      			name: "菜鸟教程",
      			site: "http://www.runoob.com"
    		};
  		},
 
  		render: function() {
    		return (
      			<div>
        			<Name name={this.state.name} />
        			<Link site={this.state.site} />
      			</div>
    		);
  		}
	});
 
	var Name = React.createClass({
  		render: function() {
    		return (
      			<h1>{this.props.name}</h1>
    		);
  		}
	});
 
	var Link = React.createClass({
  		render: function() {
    		return (
      			<a href={this.props.site}>
        			{this.props.site}
      			</a>
    		);
  		}
	});
 
	ReactDOM.render(
  		<WebSite />,
  		document.getElementById('example')
	);

##4、Props 验证
Props 验证使用 propTypes，它可以保证我们的应用组件被正确使用，React.PropTypes 提供很多验证器 (validator) 来验证传入数据是否有效。当向 props 传入无效数据时，JavaScript 控制台会抛出警告。

以下实例创建一个 Mytitle 组件，属性 title 是必须的且是字符串，非字符串类型会自动转换为字符串 ：

	var title = "菜鸟教程";
	// var title = 123;
	var MyTitle = React.createClass({
  		propTypes: {
    		title: React.PropTypes.string.isRequired,
	  	},
 
	  	render: function() {
    	 	return <h1> {this.props.title} </h1>;
   		}
	});
	ReactDOM.render(
    	<MyTitle title={title} />,
    	document.getElementById('example')
	);


更多验证说明：

	React.createClass({
  		propTypes: {
    // 可以声明 prop 为指定的 JS 基本数据类型，默认情况，这些数据是可选的
   		optionalArray: React.PropTypes.array,
    	optionalBool: React.PropTypes.bool,
    	optionalFunc: React.PropTypes.func,
    	optionalNumber: React.PropTypes.number,
    	optionalObject: React.PropTypes.object,
    	optionalString: React.PropTypes.string,
 
    // 可以被渲染的对象 numbers, strings, elements 或 array
    	optionalNode: React.PropTypes.node,
 
    //  React 元素
   		optionalElement: React.PropTypes.element,
 	
    // 用 JS 的 instanceof 操作符声明 prop 为类的实例。
   		optionalMessage: React.PropTypes.instanceOf(Message),
 
    // 用 enum 来限制 prop 只接受指定的值。
    	optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),
 
    // 可以是多个对象类型中的一个
   		optionalUnion: React.PropTypes.oneOfType([
      		React.PropTypes.string,
      		React.PropTypes.number,
      		React.PropTypes.instanceOf(Message)
    	]),
 
    // 指定类型组成的数组
    	optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),
 
    // 指定类型的属性构成的对象
    optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),
 
    // 特定 shape 参数的对象
    optionalObjectWithShape: React.PropTypes.shape({
      color: React.PropTypes.string,
      fontSize: React.PropTypes.number
    }),
 
    // 任意类型加上 `isRequired` 来使 prop 不可空。
    requiredFunc: React.PropTypes.func.isRequired,
 
    // 不可空的任意类型
    requiredAny: React.PropTypes.any.isRequired,
 
    // 自定义验证器。如果验证失败需要返回一个 Error 对象。不要直接使用 `console.warn` 或抛异常，因为这样 `oneOfType` 会失效。
    customProp: function(props, propName, componentName) {
      if (!/matchme/.test(props[propName])) {
        return new Error('Validation failed!');
      }
    }
  },
  /* ... */
});

#五、React 组件API
我们将讲解以下7个方法:

+ 设置状态：setState
+ 替换状态：replaceState
+ 设置属性：setProps
+ 替换属性：replaceProps
+ 强制更新：forceUpdate
+ 获取DOM节点：findDOMNode
+ 判断组件挂载状态：isMounted

#六、组件的生命周期

1、组件的生命周期可分成三个状态：

+ Mounting：已插入真实 DOM
+ Updating：正在被重新渲染
+ Unmounting：已移出真实 DOM

2、生命周期的方法有：

+ componentWillMount 在渲染前调用,在客户端也在服务端。
+ componentDidMount : 在第一次渲染后调用，只在客户端。之后组件已经生成了对应的DOM结构，可以通过this.getDOMNode()来进行访问。 如果你想和其他JavaScript框架一起使用，可以在这个方法中调用setTimeout, setInterval或者发送AJAX请求等操作(防止异部操作阻塞UI)。
+ componentWillReceiveProps 在组件接收到一个新的prop时被调用。这个方法在初始化render时不会被调用。
+ shouldComponentUpdate 返回一个布尔值。在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。 
可以在你确认不需要更新组件时使用。
+ componentWillUpdate 在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用。
+ componentDidUpdate 在组件完成更新后立即调用。在初始化时不会被调用。
+ componentWillUnmount 在组件从 DOM 中移除的时候立刻被调用。

#七、React AJAX

React 组件的数据可以通过 **componentDidMount** 方法中的 Ajax 来获取，当从服务端获取数据库可以将数据存储在 state 中，再用 **this.setState** 方法重新渲染 UI。

当使用异步加载数据时，在组件卸载前使用 **componentWillUnmount** 来取消未完成的请求。
以下实例演示了获取 Github 用户最新 gist 共享描述:

#八、React 表单与事件

1、实例一

设置了输入框 input 值 **value = {this.state.data}**。在输入框值发生变化时我们可以更新 state。我们可以使用 **onChange 事件**来监听 input 的变化，并修改 state。

如下代码将渲染出一个值为 Hello Runoob! 的 input 元素，并通过 onChange 事件响应更新用户输入的值。

	var HelloMessage = React.createClass({
	    getInitialState: function() {
	    	return {value: 'Hello Runoob!'};
  		},
  		handleChange: function(event) {
    		this.setState({value: event.target.value});
  		},
  		render: function() {
		    var value = this.state.value;
		    return <div>
    		        <input type="text" value={value} onChange={this.handleChange} /> 
    		        <h4>{value}</h4>
    	       </div>;
  		}	
	});
	
	ReactDOM.render(
  		<HelloMessage />,
  		document.getElementById('example')
	);

2、实例二

在以下实例中我们将为大家演示如何在子组件上使用表单。 onChange 方法将触发 state 的更新并将更新的值传递到子组件的输入框的 value 上来重新渲染界面。

你需要在父组件通过创建事件句柄 (handleChange) ，并作为 prop (updateStateProp) 传递到你的子组件上。

	var Content = React.createClass({
		render: function() {
    		return  <div>
        	    		<input type="text" value={this.props.myDataProp} onChange={this.props.updateStateProp} /> 
        	    		<h4>{this.props.myDataProp}</h4>
		            </div>;
  		}
	});
	
	var HelloMessage = React.createClass({
		getInitialState: function() {
		    return {value: 'Hello Runoob!'};
		},
  		handleChange: function(event) {
    		this.setState({value: event.target.value});
  		},
  		render: function() {
    		var value = this.state.value;
    		return <div>
            		<Content myDataProp = {value} updateStateProp = {this.handleChange}></Content>
           			</div>;
 		 }/*在父级创建事件句柄 (handleChange) ，并作为 prop (updateStateProp) 传递到子组件上*/
	});
	
	ReactDOM.render(
  		<HelloMessage />,
  		document.getElementById('example')
	);

#九、React Refs

React 支持一种非常特殊的属性 Ref ，你可以用来绑定到 render() 输出的任何组件上。

这个特殊的属性允许你引用 render() 返回的相应的支撑实例（ backing instance ）。这样就可以确保在任何时间总是拿到正确的实例。

1、使用方法

绑定一个 ref 属性到 render 的返回值上：

	<input ref="myInput" />
在其它代码中，通过 this.refs 获取支撑实例:
	var input = this.refs.myInput;
	var inputValue = input.value;
	var inputRect = input.getBoundingClientRect();

2、完整实例

你可以通过使用 this 来获取当前 React 组件，或使用 ref 来获取组件的引用，实例如下：

	var MyComponent = React.createClass({
		handleClick: function() {
    	// 使用原生的 DOM API 获取焦点
    		this.refs.myInput.focus();
  		},

  		render: function() {
    //  当组件插入到 DOM 后，ref 属性添加一个组件的引用于到 this.refs
    		return (
      			<div>
        			<input type="text" ref="myInput" />
        			<input type="button" value="点我输入框获取焦点" 	
						onClick=this.handleClick} />
      			</div>
    		);
  		}
	});
 
	ReactDOM.render(
  		<MyComponent />,
  		document.getElementById('example')
	);

实例中，我们获取了输入框的支撑实例的引用，子点击按钮后输入框获取焦点。我们也可以使用 getDOMNode()方法获取DOM元素

## 一、HTML 模板

使用 React 的网页源码，结构大致如下。

    <!DOCTYPE html>
    <html>
      <head>
          <script src="../build/react.js"></script>
          <script src="../build/react-dom.js"></script>
          <script src="../build/browser.min.js"></script>
      </head>
      <body>
          <div id="example"></div>
          <script type="text/babel">
            // ** Our code goes here! **
          </script>
      </body>
    </html>

+ 最后一个 &lt;script&gt;标签的 type 属性为 text/babel。这是因为 React 独有的 JSX 语法，跟 JavaScript 不兼容。凡是使用 JSX 的地方，都要加上 type="text/babel" 。
+ 三个库： 它们必须首先加载。
+ ——  react.js , React 的核心库
+ ——  react-dom.js ,是提供与 DOM 相关的功能
+ ——  Browser.js ，用是将 JSX 语法转为 JavaScript 语法，这一步很消耗时间，实际上线的时候，应该将它放到服务器完成。
	
	$ babel src --out-dir build

上面命令可以将 src 子目录的 js 文件进行语法转换，转码后的文件全部放在 build 子目录。

## 二、ReactDOM.render()

ReactDOM.render 是 React 的最基本方法，用于将模板转为 HTML 语言，并插入指定的 DOM 节点。

    ReactDOM.render(
      <h1>Hello, world!</h1>,
      document.getElementById('example')
    );

上面代码将一个 h1 标题，插入 example 节点。

## 三、JSX 语法

上一节的代码， HTML 语言直接写在 JavaScript 语言之中，不加任何引号，这就是 JSX 的语法，它允许 HTML 与 JavaScript 的混写。

    var names = ['Alice', 'Emily', 'Kate'];

    ReactDOM.render(
      <div>
        {
          names.map(function (name) {
            return <div>Hello, {name}!</div>
          })
        }
      </div>,
      document.getElementById('example')
    );

上面代码体现了 JSX 的基本语法规则：遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析。

JSX 允许直接在模板插入 JavaScript 变量。如果这个变量是一个数组，则会展开这个数组的所有成员。

    var arr = [
      <h1>Hello world!</h1>,
      <h2>React is awesome</h2>,
    ];
    ReactDOM.render(
      <div>{arr}</div>,
      document.getElementById('example')
    );

上面代码的arr变量是一个数组，结果 JSX 会把它的所有成员，添加到模板。