## 第一节 技术框架

- CSS编译推荐采用 SCSS 语法。

## 第二节 书写规范

#### 2.0 属性顺序

```
{
    //显示属性
    display: block;
    overflow: hidden;
    opacity: .2;
    visibility: visible;
    //盒子属性
    width: 100px;
    height: 100px;
    background: #aba6a6;
    border: 10px solid red;
    padding: 10px;
    margin: 10px;
    box-sizing: border-box;
    box-shadow: 0 0 10px black;
    box-reflect: below;
    //文字属性
    color: #ffffff;
    font-size: 12px;
    line-height: 12px;
    font-weight: bolder;
    text-align: center;
    direction: ltr;
    writing-mode: vertical-lr;
    //定位属性
    position: relative;
    top: 0;
    left: 0;
    z-index: 6;
    float: right;
    //动画属性
    transform: translateX(.1);
    transition: height ease-in 2s;
    animation: slideUp 1s ease-in;
    //其他
    appearance: none;
    cursor: pointer;
    outline: none;
    ...etc
}
```

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

> [强制] 当构建选择器时应该使用清晰， 准确和有语义的class(类)名。不要使用标签选择器。

```
 /* good */
.content > .content-header > .title {
  font-size: 2em;
}

 /* bad */
div > header > h2 {
  font-size: 2em;
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

> [强制] url() 函数中的路径加引号

```
body {
    background: url("bg.png");
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

> [建议] 颜色值最好不要使用命名色值,在可能的情况下，使用6个字符的十六进制表示法。

```
/* good */
.success {
        background-color: #aaccaa;
}

/* bad */
.success {
    background-color: #aca;
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
opacity: 0.1;
```

## 第三节 命名规范

#### 3.0 文件命名

```
主要 main　　
基础 base　　
公共 common
布局 layouts　
页面 pages
组件 components
主题 themes　
打印 print
```

#### 3.1 命名组成

- 命名必须由单词，中划线组成。例如:.info,.news-list
- 不推荐使用拼音来作为样式名，尤其是缩写的拼音、拼音与英文的混合
- 所有命名都使用小写,使用中划线 “-” 作为连接字符，而不是下划线 “_“

#### 3.2 命名前缀

- [建议] 以VUE单页组件样式为例：
- 1.页面以NAME-page的方式命名
- 2.组件的命名统一用中横线，类名和组件名保持一致

```
//page: home.vue
<template>
    <div class="home-page">
        content
    </div>
</template>

//component: nav-bar.vue
<template>
    <div class="nav-bar">
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
副标题：sub-title　　
内容：content　
导航：nav　　
侧栏：sidebar　　
栏目：column　　
大包裹：container
小包裹：wrapper　　
左右中：left right center　　
登录条：login　　
标志：logo　　
广告：banner　　
页面主体：main　　
热点：hot　　
新闻：news　　
下载：download　　
子导航：sub-nav　　
菜单：menu　　
子菜单：sub-menu　　
搜索：search　　
友情链接：friend-link　　
页脚：footer　　
版权：copyright　　
滚动：scroll　　　
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
