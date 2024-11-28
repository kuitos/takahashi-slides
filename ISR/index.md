# ISR 简介

The style of this slide is inspired by
Takahashi Method
高橋流簡報法

![](./ISR/img.png)

开始之前
先补充几个基础概念

JAMStack
**J**avaScript、**A**PIs、**M**arkup

[jamstack.org](https://jamstack.org/)

页面
接口
交互
网站是如何构成的

一种**Web 建站架构**

如何实现？
举个🌰

SSG + Headless CMS

SSG
Static Site Generation

典型框架
* Hugo
* Gatsby
* Jekyll
* VuePress

产物就是一堆含内容和交互的
**静态 HTML**

如何**动**起来？
不必每次改代码

Headless CMS
一种管理动态数据的通用方案

典型框架

![](./isr/img_1.png)
[strapi](https://strapi.io/)

结合起来

```js
// This function runs at build time on the build server
export async function getStaticProps() {
  return {
    props: {
      products: await getProductsFromAPI()
    }
  }
}
// The page component receives products prop
// from getStaticProps at build time
export default function Products({ products }) {
  return (
    <>
      <h1>Products</h1> 
      <ul>
        {products.map((product) => (
          <li key={product.id}>{product.name}</li>
        ))}
      </ul>
    </>
  )
}
```

优势
与传统网站相比

无源码变更
修改内容变更 CMS 即可

无在线服务
纯静态，无数据库、服务器依赖，低成本且不用担心被攻击风险

快
内容全部托管 CDN

有没有问题？

数据变更需触发**全量**构建

引入 ISR

是什么？

递增式静态再生
[Incremental Static Regeneration]((https://nextjs.org/docs/basic-features/data-fetching/incremental-static-regeneration))

可以**不用重新构建**
来更新静态站点的方式

举个🌰

```js
// This function runs at build time on the build server
export async function getStaticProps() {
  return {
    props: {
      products: await getProductsFromAPI()
    },
    revalidate: 60
  }
}
// The page component receives products prop
// from getStaticProps at build time
export default function Products({ products }) {
  return (
    <>
      <h1>Products</h1> 
      <ul>
        {products.map((product) => (
          <li key={product.id}>{product.name}</li>
        ))}
      </ul>
    </>
  )
}
```

访问流程：
1. 请求有预渲染返回静态页面
2. 请求无预渲染返回 fallback 页面（骨架屏）
3. 10s 内的访问返回 cached 内容
4. Next.js 后台触发页面重新生成
5. 重新生成成功，缓存更新

stale-while-revalidate

有没有问题？

体验不一致
总有人会访问到过期的页面

改进？

[DPR](https://github.com/jamstack/jamstack.org/discussions/549DPR)
Distributed Persistent Rendering

方案
1. 没有预渲染的直接构建生成
2. 不响应过期内容直接 CDN 回源到构建渲染服务
3. 每次发布更新 CDN 缓存

存在的问题
1. 运行时构建生成的性能问题
2. 不够**静态**了，防不了 DDos

总结
很多场景其实 ISR 够了不需要 SSR

营销页
介绍页
官网

