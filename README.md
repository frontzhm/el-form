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

## el-form先搭个架子


