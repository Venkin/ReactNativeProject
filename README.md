## React Native是什么, 能解决什么问题 
* 官网介绍: Build Native Mobile Apps using JavaScript and React.
React Native lets you build mobile apps using only JavaScript. It uses the same design as React, letting you compose a rich mobile UI from declarative components.
> 翻译: React Native通过JavaScript语言 和 React风格 构建原生移动应用, 通过声明各种组件创建出一个丰富多彩的移动UI界面.

* React Native着力于提高多平台开发的开发效率 —— 仅需学习一次，编写任何平台。(Learn once, write anywhere)
* 创建的应用内皆是原生的自定义组件. 生成运行的代码仍然是Java或Objective-C
* 不用在编译应用上浪费时间, 代码修改完可以立即看到效果  
![所见即所得](img/giphy.gif)
* 解决开发人员不足 IOS/Android/WinPhone (RN, 3W)
* 代码动态更新.
https://www.baidu.com/img/bd_logo1.png
* React & ReactNative 原生
* js 实现虚拟DOM驱动界面View渲染  MVC

* 文档地址
> - React官方`https://facebook.github.io/react/docs/getting-started.html`
> - ReactNative官方`https://facebook.github.io/react-native/docs/getting-started.html`
> - 中文`http://reactnative.cn/docs/0.28/getting-started.html`

> 原生 -> RN(跨平台) ->> 基于WebView(跨平台)

## 对比其他技术理解为什么使用React Native
* 跨平台开发框架
> （例如 PhoneGap，RubyMotion，Bootstrap)基于一个WebView, 使用 HTML，CSS 和 JavaScript 来将 web 的内容和体验搬到本地. 渲染速度比原生缓慢, 动画效率低.这种方式开发的 app 一般被称为 Hybrid app

* Xamarin框架, C#语言跨平台开发.优点是界面渲染高效. 缺点是API是由 Xamarin 所决定的,一旦 iOS 或Android平台推出了新的SDK, 必须等Xamarin 升级才能使用新的sdk.

* NativeScript框架, 通过反射得到所有平台 API，进行预编译，将这些 API 注入JavaScript运行环境，最后在Javascript 调用后拦截这个调用，并运行 native 代码。

## React Native的环境搭建
### 配置开发环境
* 安装JDK, 配置JDK环境变量
	> `http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html`
* 安装SDK, 配置SDK环境变量
	> * `http://www.androiddevtools.cn/`  
	> * 配置环境变量`ANDROID_HOME`指向sdk根目录  
	> * sdk需要包含android-23  
	> * sdk包含appcompat-v7/recyclerview-v7依赖库, 需要通过SDK Manager将Android Support Repository和Google Repository更新到最新.(23.0.1及以上)  
	> * 必须将sdk的tools和platform-tools配置到path中.如`%ANDROID_HOME%\tools;%ANDROID_HOME%\platform-tools;`
	> 
	> ![JAVA_HOME](img/JAVA_HOME.png)
	> ![ANDROID_HOME](img/ANDROID_HOME.png)


* 安装Node.js (JavaScript运行环境, 包含npm 包管理器)
* 安装Git (MINGW及C++环境)
* 配置npm镜像 (或可直接翻墙上网)
	> * npm config set registry https://registry.npm.taobao.org
	> * npm config set disturl https://npm.taobao.org/dist
* 安装React Native命令行工具
	> npm install -g react-native-cli

## 第一个React Native程序
1. 创建项目
	> react-native init ItheimaDemo
2. 运行packager
	* 进入ItheimaDemo工程目录
	* 执行`react-native start`
	* 测试查看打包脚本: `http://127.0.0.1:8081/index.android.bundle?platform=android`

3. 运行Android/IOS项目
	> react-native run-android

	- 注意:项目运行到手机后, 界面没有内容或显示为红色, 说明手机或模拟器没有和电脑在同一个网段, 无法访问到JS的服务。
		>  解决方法:在手机端按菜单键 -> Dev Settings -> Debug server host&port for device -> 在弹出的框中输入pc的ip和端口号, 如10.0.3.2:8081  确认后回到界面, 点击 菜单 -> Reload 重新加载

![run-android_success.jpg](img/run-android_success.jpg)

## 了解代码结构
1. import模块
	> 类似于java的import和c++的#include,用于引入其他模块

		import React, { Component } from 'react';
		// 从react-native中批量导入组件
		import {
		  AppRegistry,
		  StyleSheet,
		  Text,
		  View
		} from 'react-native';

2. 视图组件声明模块
	> 界面的入口, render函数用于渲染视图, return返回的即为界面显示的内容.其语法规范是JSX

		class ItcastDemo extends Component {
		  render() {
		    return (
		      <View >...</View>
		    );
		  }
		}

3. 样式配置模块.
	> 此模块配置了视图显示的样式效果.在视图组件模板中的使用方式
	> 给视图添加类似属性`style={styles.container}`即可

		const styles = StyleSheet.create({
		  container: {
		    ...
		  },
		  welcome: {
		    ...
		  },
		  instructions: {
		    ...
		  },
		});

4. 注册应用的入口.
	> 第一个'ItcastDemo'是项目名称, 第二个ItcastDemo是视图组件名称. 两个名称可以不同。此入口必须要配置。

		AppRegistry.registerComponent('ItcastDemo', () => ItcastDemo);

### React Native的特点及需要掌握的知识
* 特点:
	1. 界面展示(Just the UI), 作为MVC的View层
	2. 虚拟DOM (Virtual DOM), 特性,在内存中高效更新视图,实现差异化更新
	3. 数据流 (Data Flow), 单向数据流. 渲染顺序从父节点传递到子节点，如果顶层组件的某个prop改变了，React会递归的向下便利整棵组件树，重新渲染所有使用这个属性的组件。
* 需要的知识
	1. JSX语法(全程JavaScript XML) ,每一个XML标签都会被JSX转换工具转换成纯Javascript代码
	2. ES6语法知识.React Native从0.18之后，新建项目默认已经采用了ES6语法
	3. css, div, js基础  

* ![一次学习,编写各个平台](img/Learnonce,writeanywhere.jpg)


## React Native 的组件，样式及平台接口
* 核心组件:`http://reactnative.cn/docs/0.28/tutorial-core-components.html#content`

### 修改文字内容/点击事件
* onPress 属性

### 添加图片
1. 在import中添加Image组件导入
2. 在render中Image标签.

        <Image style={styles.pic}
               source={{uri: `http://www.itheima.com/uploads/2015/08/198x57.png`}}>
        </Image>

3. 在styles中添加pic的样式配置:

		pic: {
		  width:200,
		  height:50,
		}

### 组件的嵌套
* 组件嵌套是控件复用的基础

		// 自定义的组件内容
		class SubMsg extends Component{
		  render() {
		    return(
		        <View>
		          <Text>黑马程序员</Text>
		          <NextMsg />
		        </View>
		    );
		  }
		}

### 组件的状态state
* 在组件的构造函数中声明state

		  constructor(props){
		    super(props);
		    this.state = {
		      isRed: true,
		      headerMessage: 'Hello itheima! 来自state'
		    };
		  }

* 在控件中使用state

        <Text style={styleObj}>
          {this.state.headerMessage}
        </Text>

### 组件的参数props
* 在组件中声明默认属性:

		//ES6
		class Video extends React.Component {

		    static defaultProps = {
			        autoPlay: false,
			        maxLoops: 10,
		    };  // 注意这里有分号
		    static propTypes = {
		        autoPlay: React.PropTypes.bool.isRequired,
		        maxLoops: React.PropTypes.number.isRequired,
		        posterFrameSrc: React.PropTypes.string.isRequired,
		        videoSrc: React.PropTypes.string.isRequired,
		    };  // 注意这里有分号
		    render() {
		        return (
		            <View />
		        );
		    } // 注意这里既没有分号也没有逗号
		}
* 数据类型校验

	类型propTypes: `https://facebook.github.io/react/docs/component-specs.html#proptypes`

### 事件events

* https://facebook.github.io/react/docs/events.html

* 点击事件声明方式(ES6下)

        onPress={this.handleOptionsButtonClick.bind(this)}
        onPress={e=>this.handleOptionsButtonClick(e)}

### TextInput输入组件及style样式
