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

## 组件相互获取属性和事件

输入的时候，应该要判断输入值是不是有效。

输入是在`el-input`那边，验证是在`el-input-item`那边，那么就需要在`el-input`调用`el-input-item`的验证方法，
但是呢，`el-input-item`必须知道**规则和值**才能验证，换言之，需要知道`el-form`的信息。

### 先考虑`el-input-item`怎么拿到`el-form`的属性

这两，这个demo里是父子组件的关系，但实际上，不一定，但起码是 前辈和后代的关系。

之前总结过，[vue组件通信方式](https://juejin.cn/post/6897143330271035399)。

组件内部嵌套层级不确定，后代组件想要祖先组件数据的话，可考虑`provide/inject`。

![el-form3](https://blog-huahua.oss-cn-beijing.aliyuncs.com/blog/code/el-form3.png)

### 再考虑`el-input`怎么调用`el-input-item`的方法

同理，这两，这个demo里是父子组件的关系，但实际上，不一定，但起码是 前辈和后代的关系。

这里虽然也可用`provide`，但是可以试试`$parent`，毕竟一个`el-input-item`通常只有一个`el-input`。

`$parent`很多时候需要用到递归，这里抛砖引玉下。

![el-form4](https://blog-huahua.oss-cn-beijing.aliyuncs.com/blog/code/el-form4.png)

## 验证单个表单元素

这里引入[async-validator](https://github.com/yiminghe/async-validator)，之前写过一个大概[怎么使用](https://juejin.cn/post/6897173952213942280)

在`el-form-item`里已经知道`prop`/`rule`，所以引入之后，就很简单了，这边加了一个显示错误信息的属性。

![el-form5](https://blog-huahua.oss-cn-beijing.aliyuncs.com/blog/code/el-form5.png)

这样输入的时候，能实时验证。

当用户在`App.vue`那边`elForm.validate()`的时候，`el-form`里的`validate`是对所有表单元素的`validate`进行了遍历，如果都是true，那就返回`true`，否则就是`false`。

所有表单元素，其实就是`el-form-item`，综合组件通信方式，果断还是用下`$children`，这里也一样要递归拿到`el-form-item`。

