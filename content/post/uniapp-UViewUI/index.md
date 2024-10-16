---
title: "uniapp 引入 UViewUI"
date: 2024-10-16
categories: ["uniapp"]
---

### 引入UView
写在前面: 写这篇文章是因为，个人开发时为了能够兼容多端的UI所以选择了UViewUI，但是在引入项目时出现了很多问题，最后解决，所以写下这篇文章

#### 1、第一步安装SCSS

```bash
// 安装sass
npm i sass -D

// 安装sass-loader，注意需要版本10，否则可能会导致vue与sass的兼容问题而报错
npm i sass-loader@10 -D

```

#### 2、引入uView主JS库
在项目src目录中的main.js中，引入并使用uView的JS库，注意这两行要放在import Vue之后。
```js
// main.js
import uView from "uview-ui";
Vue.use(uView);

```

#### 3、在引入uView的全局SCSS主题文件
在项目src目录的uni.scss中引入此文件。
```scss

/* uni.scss */
@import 'uview-ui/theme.scss';

```

#### 4、引入uView基础样式
在App.vue中首行的位置引入，注意给style标签加入lang="scss"属性
```scss

<style lang="scss">
	/* 注意要写在第一行，同时给style标签加入lang="scss"属性 */
	@import "uview-ui/index.scss";
</style>

```

#### 5、配置easycom组件模式
此配置需要在项目src目录的pages.json中进行。
```json

// pages.json
{
	"easycom": {
		"^u-(.*)": "uview-ui/components/u-$1/u-$1.vue"
	},
	
	// 此为本身已有的内容
	"pages": [
		// ......
	]
}
```

#### 6、对uView进行了npm安装
此配置需要在项目src目录的pages.json中进行。
```bash

// 如果您的项目是HX创建的，根目录又没有package.json文件的话，请先执行如下命令：
// npm init -y

// 安装
npm install uview-ui@2.0.36

```
### 总结
根据上面的步骤使用HbuilderX编辑器，应该就可以编译完成，但是可能你会遇到一些问题
在我的成功引入的环境中:

<p> nodejs version:17 </p>
<p> vue version:vue2 </p>
<p> 如果你使用vue3的话请引入 UView-plus</p>



你需要注意的是假如编译报错时可能会显示找不到对应的模块此时就需要在page.json,和引入的scss文件路径进行修改，
注意尽量不要自己敲路径，尽量复制路径，因为你永远不知道自己会不会打错路径，另外根据UView官网你可能会看到如果使用HbuilderX编辑器的话不需要安装scss-loader，这是一个坑，不安装的话会报错,另外如果你使用HbuilderX官网的插件导入的话要注意使用vue2版本，但是我并没有使用成功，可能是我的配置还是有问题。
