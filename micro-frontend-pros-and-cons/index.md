# 微前端架构
失与得

by Kuitos

我们探索微前端架构实践的
诉求

- 技术栈无关 
- 独立开发、独立部署 
- 独立运行时
- 如 SPA 般的丝滑体验

## 技术选型

npm package?

- 技术栈无关 ❓
- 独立开发、独立部署 ✅
- 独立运行时 ❓
- 如 SPA 般的丝滑体验 ✅

Iframe?

- 技术栈无关 ✅
- 独立开发、独立部署 ✅
- 独立运行时 ✅
- 如 SPA 般的丝滑体验 🚫

要不就 Iframe 吧 🐶

Iframe 7 宗罪

慢

- 每次进入上下文重建
- 每次进入资源重载

硬隔离带来的
上下文不共享的问题

无解

- url 不同步
- UI 不同步
- 内存变量不共享
- DOM 结构不共享
- 等等

Iframe 又不让用

搞得那么**累**
真的有价值吗

敏捷性
独立开发和更快的部署周期

相互依赖下降
降低错误和回归问题的风险

自由组合
更高的产品商业灵活性

更快的交付
持续集成、持续部署、持续交付

维护和 bugfix 简单
只需要熟悉自己的区域

世界上哪有完美的解决方案

![](./micro-frontend-pros-and-cons/wanna-all.png)

微前端架构的
<del>缺点</del>成本

开发与部署环境分离
本地需要一个更复杂的开发环境

复杂的集成
Isolated CSS、JS Sandbox、Dynamic Load

第三方模块重叠

社区有哪些
**优秀**的选择？

![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1558037745720&di=dfe1e1a242ef1846a842dfcbb9c7aec8&imgtype=0&src=http%3A%2F%2Fimg.mp.itc.cn%2Fupload%2F20170420%2F0e022a607d8647eaa8c78ac89ccdd922.gif)

[乾坤](https://github.com/kuitos/qiankun)

**现场开源！**








