---
title: "Uniapp 开发篇"
date: 2024-10-02 00:00:00+0000
image: https://qiniu-web-assets.dcloud.net.cn/unidoc/zh/uni-app.png
tags: 
    - uniapp
    - multi-platform
categories:
    - Web
---

# Uniapp 开发篇

## 目录
1. 介绍
2. 环境搭建（Hello World）
3. 项目基本目录结构
4. 开发规范概述
5. 全局配置文件（`pages.json`）
6. 创建新页面和页面的配置
7. 配置 `tabBar`
8. 组件
9. 页面样式与布局
10. Vue 基本语法复习
11. Uniapp 的生命周期
12. 下拉刷新
13. 上拉加载
14. 网络请求

## 一、介绍

Uniapp 是一个基于 Vue.js 开发跨平台应用的框架，支持多个平台（如微信小程序、H5、Android、iOS 等）的开发。它提供了丰富的组件库和 API，开发者只需要编写一套代码，就可以跨平台运行。

### Uniapp 的优势
- **跨平台性**：一套代码多端运行
- **社区支持强大**，文档齐全
- **丰富的插件市场**

如果你刚入门小程序开发，可能会对 Uniapp 和原生微信小程序的区别感到困惑。我的建议是先观看以下视频，可以更好地理解两者的优缺点：

[开发微信小程序使用原生开发还是uniapp开发](https://www.bilibili.com)

## 二、环境搭建（Hello World）

### 2.1 下载 HBuilderX
[HBuilderX 下载地址](https://www.dcloud.io/hbuilderx.html)

HBuilderX 是官方推荐的 IDE，天然整合了 uniapp，方便高效。

### 2.2 下载微信开发者工具
[微信开发者工具下载地址](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)

最终我们需要通过微信开发者工具来打包和预览微信小程序。

### 2.3 创建 Uniapp 项目
1. 打开 HBuilderX，点击 `新建` -> `项目` -> `选择 Uniapp 模板`。
2. 设置项目名称和路径。
3. 生成项目基本结构后，点击运行即可看到 hello world 项目在浏览器中运行。

### 2.4 在微信开发者工具中运行
1. 在 HBuilderX 中点击运行，选择 `运行到小程序模拟器`。
2. 如果遇到报错，可以进入微信开发者工具 -> 设置 -> 安全，开启服务端口。

### 2.5 在手机上运行
1. 连接安卓或 iOS 设备，通过 HBuilderX 将应用运行到真机上。
2. iOS 设备需要额外的配置，暂不支持直接运行。

## 三、项目基本目录结构

一个标准的 Uniapp 项目目录结构如下：
```
- pages/         # 存放页面文件，Vue 单文件组件
- static/        # 静态资源（图片、字体等）
- components/    # 自定义组件
- unpackage/     # 打包后的文件
- App.vue        # 根组件
- main.js        # 项目入口文件
- manifest.json  # 应用配置（名称、版本等）
- pages.json     # 页面路由、导航栏、TabBar 配置
- uni.scss       # 全局样式文件
```

## 四、开发规范概述

### 4.1 命名规范
- 组件命名：使用驼峰或短横线连接方式，如 `myComponent` 或 `my-component`。
- CSS 类名：使用短横线连接，如 `.my-container`。

### 4.2 文件组织规范
- 页面文件放在 `pages/` 目录下，按功能划分子目录。
- 组件文件放在 `components/` 目录下，按功能划分子目录。

### 4.3 编码规范
- 遵循 Vue.js 的编码规范。
- 使用 Flex 布局确保各平台的一致性。

## 五、全局配置文件（`pages.json`）

### 5.1 `globalStyle`（全局样式）
用于配置导航栏、标题、窗口背景色等。常见属性如下：

| 属性                         | 类型        | 默认值  | 说明                                                      |
|------------------------------|-------------|---------|-----------------------------------------------------------|
| navigationBarBackgroundColor  | HexColor    | #F8F8F8 | 导航栏背景颜色                                             |
| navigationBarTextStyle        | String      | black   | 导航栏标题颜色，支持 `black` 或 `white`                   |
| navigationBarTitleText        | String      |         | 导航栏标题文字内容                                         |

> 注意：页面配置中的样式优先级高于全局配置。

### 5.2 `pages`（页面路由）
`pages.json` 中的 `pages` 节点定义应用中的页面。配置示例：
```json
{
  "pages": [
    {
      "path": "pages/index/index",
      "style": {
        "navigationBarTitleText": "首页"
      }
    }
  ]
}
```

### 5.3 `tabBar`（多 Tab 应用）
可以通过 `tabBar` 配置一级导航栏，示例：
```json
{
  "tabBar": {
    "color": "#999999",
    "selectedColor": "#3cc51f",
    "backgroundColor": "#ffffff",
    "list": [
      {
        "pagePath": "pages/home/home",
        "text": "首页",
        "iconPath": "static/icon_home.png",
        "selectedIconPath": "static/icon_home_selected.png"
      }
    ]
  }
}
```

## 六、创建新页面和页面的配置

### 6.1 创建新页面
在 HBuilderX 中右键 `pages/` 目录，选择 “新建 -> 页面”，为新页面命名。

### 6.2 配置 `pages.json`
手动添加新页面的路径配置：
```json
{
  "path": "pages/newPage/newPage",
  "style": {
    "navigationBarTitleText": "新页面"
  }
}
```

### 6.3 运行新页面
通过浏览器或真机测试，确保新页面正常显示。

## 七、配置 `tabBar`

配置 `tabBar` 时，可以设置图标、文字以及中间凸起的按钮。以下为基本配置示例：
```json
{
  "tabBar": {
    "color": "#999",
    "selectedColor": "#3cc51f",
    "backgroundColor": "#fff",
    "list": [
      {
        "pagePath": "pages/index/index",
        "text": "首页",
        "iconPath": "static/icon_home.png",
        "selectedIconPath": "static/icon_home_selected.png"
      }
    ],
    "midButton": {
      "iconPath": "static/icon_add.png",
      "iconWidth": "50px",
      "backgroundImage": "static/button_bg.png"
    }
  }
}
```

## 八、组件

### 8.1 `Text` 组件
用于包裹文本内容，常用属性：
- `selectable`: 是否可选中内容，默认为 `false`。
- `decode`: 是否解码 HTML 字符实体，默认为 `false`。

示例：
```html
<text selectable="true">可选中的文本</text>
```

### 8.2 `Icon` 组件
用于显示图标，常用属性：
- `type`: 图标类型，如 `success`、`warn`、`loading`。
- `size`: 图标大小。
- `color`: 图标颜色。

示例：
```html
<icon type="success" size="30" color="#4caf50"></icon>
```
待更新···

## 九、页面样式与布局

### 9.1 尺寸单位
- **px**: 固定像素单位。
- **rpx**: 响应式像素单位，会根据屏幕宽度自动调整。

### 9.2 样式导入
使用 `@import` 导入外部样式：
```css
@import "./common.css";
```

## 十、Vue 基本语法复习

Uniapp 是基于 Vue.js 的框架，如果你熟悉 Vue，可以跳过此部分。如果不熟悉，可以复习 Vue 的基本语法。

## 十一、Uniapp 的生命周期

### 应用的生命周期
- `onLaunch`: 应用初始化时触发。
- `onShow`: 应用显示时触发。
- `onHide`: 应用隐藏时触发。

### 页面生命周期
- `onLoad`: 页面加载时触发。
- `onShow`: 页面显示时触发。
- `onReady`: 页面初次渲染完成时触发。
- `onHide`: 页面隐藏时触发。
- `onUnload`: 页面卸载时触发。

## 十二、下拉刷新

在 `pages.json` 中设置 `enablePullDownRefresh`

 为 `true` 即可启用下拉刷新：
```json
{
  "path": "pages/index/index",
  "style": {
    "enablePullDownRefresh": true
  }
}
```

## 十三、上拉加载

在页面的 `onReachBottom` 函数中处理上拉加载逻辑：
```javascript
onReachBottom() {
  // 加载更多数据
}
```

## 十四、网络请求

使用 `uni.request` 发送网络请求，支持 GET 和 POST 请求。示例：
```javascript
uni.request({
  url: 'https://example.com/api',
  method: 'GET',
  success: (res) => {
    console.log(res.data);
  }
});
```

可以考虑封装网络请求函数，避免重复代码：
```javascript
function request(url, data = {}, method = 'GET') {
  return new Promise((resolve, reject) => {
    uni.request({
      url,
      data,
      method,
      success: (res) => resolve(res.data),
      fail: (err) => reject(err)
    });
  });
}
```

## 十五、UI组件库的引入

待更新···

## 十六、跨平台编译

待更新···

····内容持续更新

---

以上内容是 Uniapp 开发的基础知识。随着项目的复杂度增加，可以深入研究组件通信、状态管理、多端兼容性优化等进阶内容。希望这篇文章对你有帮助！
-by daixun
```