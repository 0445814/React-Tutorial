# postcss
[PostCSS](https://github.com/postcss/postcss/blob/master/README-cn.md) 是一个允许使用 JS 插件转换css样式的工具集。 这些插件可以检查（lint）你的 CSS，支持 CSS Variables 和 Mixins， 编译尚未被浏览器广泛支持的先进的 CSS 语法，内联图片，以及其它很多优秀的功能。

截止到目前，PostCSS 有 [200 多个插件](https://github.com/postcss/postcss/blob/master/docs/plugins.md)。下面是一些主流的、常用的插件:  

### 一，Autoprefixer 
[Autoprefixer](https://github.com/postcss/autoprefixer)是最流行的 CSS 处理工具之一，也是`postcss`最为流行的插件。它主要用于给css自动添加浏览器兼容性前缀。它使用 [Can I Use](https://www.caniuse.com) 上面的数据。

[cra(create-react-app)](https://facebook.github.io/create-react-app/docs/getting-started)默认支持[Autoprefixer](https://github.com/postcss/autoprefixer)，开箱即用。

```css 
/* css代码 */
.App {
  transform:rotate(180deg);
}

/* 编译后 */  
.App {
  -webkit-transform: rotate(180deg);
  transform: rotate(180deg);
}
```

### 二，postcss-cssnext  
[postcss-cssnext](https://github.com/MoOx/postcss-cssnext)是一款可以让你使用未来css语法(css4)的`postcss`插件。

```css
/* 自定义`--mianColor` */
:root{
    --mianColor:#ffc001;
}

/* 使用var调用`--mianColor`属性 */
.test{
    background: var(--mianColor);
}

/*编译后*/
.test{
    background: #ffc001;
}
```

### 三，cssnano 
[cssnano](https://cssnano.co/)是一款用于压缩css的`postcss`插件。通常压缩率可达50%。

### 四，postcss-sprites
[postcss-sprites](https://github.com/2createStudio/postcss-sprites)是一款用于自动生成雪碧图的`postcss`插件。
```css
/* 原代码 */
.comment { background: url(images/sprite/ico-comment.png) no-repeat 0 0; }
.bubble { background: url(images/sprite/ico-bubble.png) no-repeat 0 0; }

/* 编译后 */
.comment { background-image: url(images/sprite.png); background-position: 0 0; }
.bubble { background-image: url(images/sprite.png); background-position: 0 -50px; }
```
.....

更多postcss插件请查看[postcss插件列表](https://github.com/postcss/postcss/blob/master/docs/plugins.md)
