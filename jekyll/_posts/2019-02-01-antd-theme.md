---
layout: post
title:  "学习antd-theme"
date:   2019-02-01 13:31:01 +0800
categories: css
tag: antd
---

* content
{:toc}


antd-theme				{#zhugeliang}
------------------------

#### antd的样式采用less语言，并向开发者提供了两个功能：
1. 按需加载组件样式
2. 自定义主题

按需加载组件样式，通过webpack中配置对应的插件即可。而自定义主题的应用，则需要了解更多的细节。
  
首先，要知道antd中一共有多少可定义的参数。  
引用自官网：[antd定制主题](https://ant.design/docs/react/customize-theme-cn)  
@primary-color: #1890ff;                         // 全局主色  
@link-color: #1890ff;                            // 链接色  
@success-color: #52c41a;                         // 成功色  
@warning-color: #faad14;                         // 警告色  
@error-color: #f5222d;                           // 错误色  
@font-size-base: 14px;                           // 主字号  
@heading-color: rgba(0, 0, 0, .85);              // 标题色  
@text-color: rgba(0, 0, 0, .65);                 // 主文本色  
@text-color-secondary : rgba(0, 0, 0, .45);      // 次文本色  
@disabled-color : rgba(0, 0, 0, .25);            // 失效色  
@border-radius-base: 4px;                        // 组件/浮层圆角  
@border-color-base: #d9d9d9;                     // 边框色  
@box-shadow-base: 0 2px 8px rgba(0, 0, 0, .15);  // 浮层阴影  

接着，就是如果定制。  
一，通过webpack配置：
  
```
// webpack.config.js
module.exports = {
  rules: [{
    test: /\.less$/,
    use: [{
      loader: 'style-loader',
    }, {
      loader: 'css-loader', // translates CSS into CommonJS
    }, {
      loader: 'less-loader', // compiles Less to CSS
+     options: {
+       modifyVars: {
+         'primary-color': '#1DA57A',
+         'link-color': '#1DA57A',
+         'border-radius-base': '2px',
+       },
+       javascriptEnabled: true,
+     },
    }],
    // ...other rules
  }],
  // ...other config
}
```


二，通过less文件覆盖：

```
@import "~antd/dist/antd.less";   // 引入官方提供的 less 样式入口文件
@import "your-theme-file.less";   // 用于覆盖上面定义的变量
```

但这两种，都是在打包阶段完成的主题自定义。我们还会面对主题切换的需求。
可以通过以下方式完成：
1. 在项目中引入less.js
2. 在html文件中放置一个color.less文件位于其他css文件下
3. 点击主题切换时，调用 less.modifyVars()修改color.less中包含的变量。



