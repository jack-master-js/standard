## Table of Contents

  1. [第一节 技术框架](#)
  1. [第二节 书写规范](#)
  1. [第三节 命名规范](#)
  
## 第一节 技术框架

- CSS编译推荐采用 SCSS 语法。

## 第二节 书写规范

#### 2.0 属性顺序

- 显示属性(display)
- 大小间距(width, height, border, padding, margin等)
- 内容文字(color, font-size, line-height, letter-spacing, text-align等)
- 背景(background)
- 定位(position, top, right, float, z-index等)
- 其他(animation, transition等)

#### 2.1 选择器

> [强制] 如无必要，不得为 id、class 选择器添加类型选择器进行限定

```
 /* good */
 #error,
 .danger-message {
     font-color: #c00;
 }

 /* bad */
 dialog#error,
 p.danger-message {
     font-color: #c00;
 }
```

> [强制] 当构建选择器时应该使用清晰， 准确和有语义的class(类)名。不要使用标签选择器。 如果你只关心你的class(类)名

```
 /* good */
div.content > header.content-header > h2.title {
  font-size: 2em;
}

 /* bad */
.content > .content-header > .title {
  font-size: 2em;
}
```

> [建议] 每个选择器和属性声明总是使用新的一行

```
 /* good */
h1,
h2,
h3 {
  font-weight: normal;
  line-height: 1.2;
}

 /* bad */
a:focus, a:active {
  position: relative; top: 1px;
}
```

#### 2.2 属性缩写

> [建议] 在可以使用缩写的情况下，尽量使用属性缩写

```
/* good */
.post {
    font: 12px/1.5 arial, sans-serif;
}

/* bad */
.post {
    font-family: arial, sans-serif;
    font-size: 12px;
    line-height: 1.5;
}
```

> [建议] 使用 border / margin / padding 等缩写时，应注意隐含值对实际数值的影响，确实需要设置多个方向的值时才使用缩写

```
/* good */
.page {
    margin-right: auto;
    margin-left: auto;
}

.featured {
    border-color: #69c;
}

/* bad */
.page {
    margin: 5px auto; /* introducing redundancy */
}

.featured {
    border: 1px solid #69c; /* introducing redundancy */
}
```

#### 2.3 值与单位

> [强制] 文本内容必须用双引号包围

```
/* good */
html[lang|="zh"] q:before {
    font-family: "Microsoft YaHei", sans-serif;
    content: "“";
}

html[lang|="zh"] q:after {
    font-family: "Microsoft YaHei", sans-serif;
    content: "”";
}

/* bad */
html[lang|=zh] q:before {
    font-family: 'Microsoft YaHei', sans-serif;
    content: '“';
}

html[lang|=zh] q:after {
    font-family: "Microsoft YaHei", sans-serif;
    content: "”";
}
```

#### 2.4 数值

> [强制] 当数值为 0 - 1 之间的小数时，省略整数部分的 0

```
/* good */
panel {
    opacity: .8
}

/* bad */
panel {
    opacity: 0.8
}
```

#### 2.5 url()

> [强制] url() 函数中的路径不加引号

```
body {
    background: url(bg.png);
}
```

#### 2.6 长度

> [强制] 长度为 0 时须省略单位。 (也只有长度单位可省)

```
/* good */
body {
    padding: 0 5px;
}

/* bad */
body {
    padding: 0px 5px;
}
```

#### 2.7 颜色

> [建议] 颜色值最好不要使用命名色值,在可能的情况下，使用3个字符的十六进制表示法。

```
/* good */
.success {
    background-color: #aca;
}

/* bad */
.success {
    background-color: #aaccaa;
}
```

> [建议] 颜色值中的英文字符采用小写。如不用小写也需要保证同一项目内保持大小写一致

```
/* good */
.success {
    background-color: #aca;
    color: #90ee90;
}

/* good */
.success {
    background-color: #ACA;
    color: #90EE90;
}

/* bad */
.success {
    background-color: #ACA;
    color: #90ee90;
}
```

#### 2.8 2D 位置

> [强制] 必须同时给出水平和垂直方向的位置

> [解释] 2D 位置初始值为 0% 0%，但在只有一个方向的值时，另一个方向的值会被解析为 center。为避免理解上的困扰，应同时给出两个方向的值。

```
/* good */
body {
    background-position: center top; /* 50% 0% */
}

/* bad */
body {
    background-position: top; /* 50% 0% */
}
```

#### 2.9 字体族

> [强制] font-family 属性中的字体族名称应使用字体的英文 Family Name，其中如有空格，须放置在引号中

```
h1 {
    font-family: "Microsoft YaHei"; //微软雅黑
}
```

#### 2.10 字号

> [强制] 需要在 Windows 平台显示的中文内容，其字号应不小于 12px

> [解释] 由于 Windows 的字体渲染机制，小于 12px 的文字显示效果极差、难以辨认

#### 2.11 字体风格

> [建议] 需要在 Windows 平台显示的中文内容，不要使用除 normal 外的 font-style。其他平台也应慎用

> [解释] 由于中文字体没有 italic 风格的实现，所有浏览器下都会 fallback 到 obilique 实现 (自动拟合为斜体)，小字号下 (特别是 Windows 下会在小字号下使用点阵字体的情况下) 显示效果差，造成阅读困难

#### 2.12 变换与动画

> [强制] 使用 transition 时应指定 transition-property

```
/* good */
.box {
    transition: color 1s, border-color 1s;
}

/* bad */
.box {
    transition: all 1s;
}
```

> [建议] 尽可能在浏览器能高效实现的属性上添加过渡和动画

```
transform: translate(npx, npx);
transform: scale(n);
transform: rotate(ndeg);
opacity: 0..1;
```

## 第三节 命名规范

#### 3.0 文件命名

```
主要的 main　　
基础框架 base　　
公共 common
布局 layout　
主题 themes　
打印 print
```

#### 3.1 命名组成

- 命名必须由单词，中划线组成。例如:.info,.news-list
- 不推荐使用拼音来作为样式名，尤其是缩写的拼音、拼音与英文的混合
- 所有命名都使用小写,使用中划线 “-” 作为连接字符，而不是下划线 “_“

#### 3.2 命名前缀

- [建议] 以VUE单页组件样式为例,可在组件第一层div上定义一个命名空间,开启scoped
- [强制] 通用样式命名为common
- [强制] sass所要用的变量及函数,命名为main

```
//home.vue
<template>
    <div class="home-wrapper">
        content
    </div>
</template>
```

#### 3.3 命名单词

- 不以表现来命名，而是根据内容来命名。
- 推荐使用功能和内容相关词汇的命名

```
头：header　　
尾：footer　　
栏目标题：title　　
内容：content/container　　
导航：nav　　
侧栏：sidebar　　
栏目：column　　
页面外围控制整体佈局宽度：wrapper　　
左右中：left right center　　
登录条：loginbar　　
标志：logo　　
广告：banner　　
页面主体：main　　
热点：hot　　
新闻：news　　
下载：download　　
子导航：subnav　　
菜单：menu　　
子菜单：submenu　　
搜索：search　　
友情链接：friend-link　　
页脚：footer　　
版权：copyright　　
滚动：scroll　　
内容：content　　
标签：tags　　
文章列表：list　　
提示信息：msg　　
小技巧：tips　　
加入：join-us　　
指南：guide　　
服务：service　　
注册：regsiter　　
状态：status　　
投票：vote　　
合作伙伴：partner
```
