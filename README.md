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

![el-form1](https://blog-huahua.oss-cn-beijing.aliyuncs.com/blog/code/el-form1.png)

## 显示输入框

观察`App.vue`

- `el-form`起码有属性`model`和`rules`，还有个方法`validate`
- 因为`el-form-item`写在其内部，所以也肯定有`slot`

- 同理，`el-form-item`起码有属性`label`和`prop`，和`slot`
- `el-input`可以`v-model`，而`v-model`是`value`和`input`的语法糖

![el-form2](https://blog-huahua.oss-cn-beijing.aliyuncs.com/blog/code/el-form2.png)

## 加入验证

输入的时候，应该要判断输入值是不是有效。

输入是在`el-input`那边，验证是在`el-input-item`那边，那么就需要在`el-input`调用`el-input-item`的验证方法，
但是呢，`el-input-item`必须知道**规则和值**才能验证，换言之，需要知道`el-form`。

先考虑`el-input-item`和`el-form`。

这两，这个demo里是父子组件的关系，但实际上，不一定，但起码是 前辈和后代的关系。

之前总结过，[vue组件通信方式](https://juejin.cn/post/6897143330271035399)。

组件内部嵌套层级不确定，后代组件想要祖先组件数据的话，可考虑`provide/inject`。

