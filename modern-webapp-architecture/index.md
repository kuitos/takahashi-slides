# 现代化
  web应用
	架构及实践

by Kuitos

## 公司介绍

数云
www.shuyun.com

电商CRM
年度最佳全渠道营销服务商
16年底上市筹备

Send your resume to
简历请投
kui.liu@shuyun.com

## 自我介绍

github: @kuitos
zhihu: kuitos
weibo: @kuitos

工作

前端打杂的

SPA应用架构
MVVM
前端工程化

代码洁癖
强迫症

The style of this slide is inspired by
Takahashi Method
高橋流簡報法

可能引起部分观众不适
Maybe made you disgusting and vertigo

请在家长陪同下观看
Pls look my handsome face hhhh

## 暖场完了

READY?

GO!

## 去年前端圈主旋律

### 框架&类库

Angular Vue MVVM
React Redux Immutable
cycle.js Reactive

### 语言&工具

ES2015
ESNEXT FP FRP
BABEL
webpack jspm rollup

AND SO ON...

## 今年前端圈主旋律

### 标准化

一个现代化webapp的标准

模块化,
组件化,
工程化

一个个的讲

#### 模块化

CommonJs vs AMD vs CMD vs UMD

CommonJs

![](modern-webapp-architecture/pasted-image-886.png)

AMD & CMD

![](modern-webapp-architecture/pasted-image-894.png)

UMD

{AMD, CommonJs}


辣么多模块化工具，我选哪个？

火车是用来等的，不是用来追的

ES2015 Module

![](modern-webapp-architecture/pasted-image-955.png)

特点就是

静态模块
语义简洁
标准

万事俱备，只缺 Module Loader

dynamic module loading

System.import

半路杀出的程咬金

![](modern-webapp-architecture/what-is-webpack-1057.png)

敢问路在何方

HTTP/2 + ES6 Module Loader

#### 组件化

命令式 vs 声明式

命令式
Jquery
![](modern-webapp-architecture/pasted-image-1160.png) 

声明式
Angular/React/Vue
![](modern-webapp-architecture/pasted-image-1224.png)

本质上是
命令式DOM 与 声明式UI
之间的差异

命令式DOM
面向对象
传统GUI编程

声明式UI
标记语言
对web开发者更友好

组合优于继承被再一次证明
![](modern-webapp-architecture/pasted-image-2188.png)

声明式组件是现代化组件框架的首要特点

数据绑定
data binding is awesome

![](modern-webapp-architecture/pasted-image-1433.png)

不是字符串替换！！

不是静态模板！！

基本配置

声明式UI + 数据绑定

总会碰到问题
理想很丰满，现实很骨感

单向 or 双向

单向 from 函数式

属性值是输入，组件DOM是输出
参数不可变
stateless

双向 from MVVM

实时关系映射

单向风头太劲

抛弃双向?

最佳实践

组件数据来自props
非表单操作型控件，单向
表单操作型控件，双向

![](modern-webapp-architecture/pasted-image-1590.png)
![](modern-webapp-architecture/pasted-image-1594.png)

组件间通信
communication between components

子组件的状态变更如何通知给父组件?

以angular为例

双向数据流

class/object getter/setter
![](modern-webapp-architecture/pasted-image-1628.png)

`$scope.$watch`
![](modern-webapp-architecture/pasted-image-1651.png)

单向数据流

单向绑定 + `inline-events`

![](modern-webapp-architecture/pasted-image-1693.png)
![](modern-webapp-architecture/pasted-image-1689.png)

无明显层级关系

配套服务中注册回调,
事件通知(下下策)

Why 下下策?

事件爆炸,
时序,
状态管理困难

勿论你怎么做
数据驱动
才是真正的核心理念

是否需要全组件化?

组件化的核心诉求

复用?

~~复用~~

分治(分而治之)

广义的全组件化

细粒度的基础控件,
粗粒度的业务模板/容器组件

还剩最复杂的一个

状态管理

redux or rxjs

#### 工程化

工程化 ≠ 工具自动化 

涉及 开发 => 发布上线

关注点

开发体验（构建自动化）,
性能（缓存等）,
持续集成（CI）,
发布（灰度发布）

两个重要原则

就近维护原则
![](modern-webapp-architecture/pasted-image-2258.png)

分治原则
![](modern-webapp-architecture/pasted-image-2278.png)

总结

现代化web应用应该是
以组件化架构为中心，
结合 ES Module 的模块化思路，
通过一套完整的自动化流程，
实现从开发到上线都具备较好体验的一个工程。

最后

以上涉及的技术领域，都在数云正在发生或即将发生！
简历请投
kui.liu@shuyun.com

Thank you!
https://github.com/kuitos
