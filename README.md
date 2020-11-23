---
title: 手写实现el-for系列组件的核心逻辑 - 练习组件通信
tags: js
categories: js
---

先运行下面命令

```shell
npm install
npm run serve
```

以前觉得[element-ui](https://element.eleme.cn/#/zh-CN/component/quickstart)肯定特别难写，最近在看组件通信，就试试写下[el-form](https://element.eleme.cn/#/zh-CN/component/form)，当做练习了，这样以后自己也能试着开发高阶组件。

本文，一步步来，读者如果有耐心的话，最好也自己手敲一遍。

## 搭个架子

为了快捷方便，用`vue create`创建个项目，因为喜欢pug,，装个`npm i pug pug-plain-loader -D`

先看看官网，关于`el-form`使用的`demo`，然后将重点复制到`App.vue`，再新建相应的组件文件。



