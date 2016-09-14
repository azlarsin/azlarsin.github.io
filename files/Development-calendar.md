title: Development calendar
author: azlar
date: 2016-09-08 21:20:20
tags: [develop calendar, another test tag, third test tag, a very long tag test let's test and console it, another a very long tag test let's test and console it, test]
ignore: false

---



记录开发 blog 的过程。
<!-- desc -->
## todo
### 功能
- 根据 `Widget` 宽度与 `Tags`、`Articles` 的字体大小计算其最大显示字符数
- `List` 样式
- `Article` 样式
- `Pagination`
- `build.js` 移动文件问题（现在需要 sudo 权限，由于有一个 `.DS_STORE` 文件存在）
- `build.js` => `new post`（命令生成 `yaml` 配置文件）
- `List` 评论数量、样式
- 归档
- SEO
- !!! github pages **static html map**

### bugs
 - [tootip of tags](#toc_18)
 - 迁移项目目录，重构目录结构
 - `css` => `scss` 与样式重新整理、规范


## 开发

### 16.9.9
折腾了一天，把代码高亮从 [`prism.js`](http://prismjs.com/) 换到了 [`highlight.js`](https://highlightjs.org/)。其实使用上感觉并不明显，主要是后者高亮主题多（然并卵，还是自己边抄边调了一套高亮）。

后台编译（伪）程序 `build.js`，添加了一些处理细节，之后要开始写 `tag-map` 的生成。

自己在设计方面还是太差，设计出来的东西简直非人能看。

### 16.9.11
- 左部挂件： `tag-list`
- 挂件中的 `tag-list` 与 `list` 中的 `tag` 的选中状态联动。

### 16.9.12
#### 文章预览
本来使用的方式是从 `head 信息` 后截取 140 字符，再向后寻找到第一个 “。”；使用之后发现效果并不好。

于是使用了在 `md 文件` 中添加一个 `<!-- desc -->` 这种方式来实现（参考 `hexo` 的预览文本方式）。这种方式可定制性更强。

P.S. 再次感慨很多时候不能纯凭机器，有时一个标识就可以解决的问题，用语言却可以派生出很多问题。

#### 长=long tag
在 `tag-list` 中，会截取一部分（:hover 的时候提示显示），在文档列表页，不会截取：
![long tag hover hint](//blog.azlar.cn/build/images/long tag hover effect.gif)

#### 文件移动
调用 `build.js` 的时候，会同时移动图片了，但是不能使用相对路径（由于 `index.html` 在 `build/` 的外面）。

正在考虑要不要将 index.html 移动到 `build` 内部。

#### 建立关联文章 `map`
通过分析每篇文章的 `tags`，获取拥有相同 `tag` 的文章。本来是在前端分析的，前端比较麻烦，而目前我是充分相信后端数据的，故使用后端直接分析得出 `index` 比较方便简单。

```javascript
//code in build.js
realListMap.map((article, index) => {
    let articleTags = article.tags;
    let articleRelated = [];
    for(let i = 0;i < articleTags.length;i++) {
        articleRelated = articleRelated.concat(tags[articleTags[i]].filter((item) => {
           return articleRelated.indexOf(item) < 0;
        }));
    }
    
    article.related = articleRelated;
});
```

### 16.9.13
#### `tag-list` 排序
按文章多少排序：

```javascript
var sortedKeys = Object.keys(tags).sort(function(a,b){return tags[b].length - tags[a].length});

//sortedKeys.map((tag) => {...});
```

#### auto scroll `tag.selected` into viewpoint
自动将当前页面，`tag-list` 中被选中的 `tag` 滑动显示。一般在选中 tag 后，刷新页面，或者点击 `:site/tag/xxx` 直接进入页面时会用到。

```javascript
//componentWillReceiveProps -> setState() -> callback()
let selectedTag = $(".tag-block.selected");
selectedTag[0].scrollIntoView({ behavior: "smooth" });
```

使用后发现，每次点击都会触发，体验很差，故需要判断其是否在视图 `viewport` 内；这个问题刚好之前研究过（两个 `rect` 是否相交）。之前有收藏一篇 [how-to-tell-if-a-dom-element-is-visible-in-the-current-viewport](http://stackoverflow.com/questions/123999/how-to-tell-if-a-dom-element-is-visible-in-the-current-viewport)，从里面选取了一个方法（有点懒得看之前写的判断两矩形相交）：

```javascript
function isElementInViewport (el) {
    //special bonus for those using jQuery
    if (typeof jQuery === "function" && el instanceof jQuery) {
        el = el[0];
    }

    var rect = el.getBoundingClientRect();

    return (
        rect.top >= 0 &&
        rect.left >= 0 &&
        rect.bottom <= (window.innerHeight || document.documentElement.clientHeight) && /*or $(window).height() */
        rect.right <= (window.innerWidth || document.documentElement.clientWidth) /*or $(window).width() */
    );
}
```
于是在视图内的 `tag` 被选中就不会自动滚动至顶部了，因为不会触发 `scrollIntoView()`：

```javascript
var selectedTag = $(".tag-block.selected");

if(selectedTag.length > 0 && !isElementInViewport(selectedTag)) {
    selectedTag[0].scrollIntoView({ behavior: "smooth" });
}
```

### 16.9.13
#### 部署倒 `github pages`
今天把项目部署到了线上后才发现一个 2b 的事情：`github pages` 并不支持 **`rewrite`**。

想了很多办法，甚至一度跑去开通了 `amazon` 的 `aws`，可是在这个过程中，心里一直念叨着：我写这个不就是为了弄一个纯静态的么，上 `vps` 不是坑自己么。。。

github 说对 jekyll 有一个插件支持，但我没调试那个。

于是想通过 `hack` 办法来实现，发现 gp 所有找不到的页面都会定向到 `404.html`，所以直接将该页面写为类似 `index.html` 的入口文件。问题解决。。

但是这样做应该有明显的问题：

- seo 问题
- 资源引用路径必须都使用绝对路径

故这只是一个临时的办法，若想实现静态化，除了虚拟出所有的 html 文件，貌似没有其他办法。（这个会在 `build.js` 生成文件的时候，将所有的 `html map` 生成）

P.S. `404.html` 真是好 `low` 的办法~

#### 移动端样式
部署后顺手写了点样式，由于之前的一部分是在 `PB` 项目开始之前写的，发现之前的样式写的好 low，又提不起精神改，头痛。。。

将样式整理与 `scss` 重写放进 `todo` 吧 -。-


## 维护

### 16.9.8
由于顶部有 `navigation-bar` 的存在，导致页面自动定位 `anchor` 的时候，会被遮蔽，故需要

- 方法1， css

	```css
	.blog .wrapper .content *[id]:before {
	    display: block;
	    content: "";
	    margin-top: -82px;
	    height: 82px;
	    visibility: hidden;
    }
	```
	
- 方法二，js listen window.hasChange && locatin.href，then auto scroll the navigation-bar.height。
- 这种方法会有一个问题：**`点击同一个 hash 的时候，浏览器会认为当前位置并不是该 hash 所在的位置，然后重新定位，而此次定位，不会触发刚才写的 auto scoll 方法。`** 解决：为目录中的 `<a>` 添加一个 listener：该 hash 与当前 location.hash 相同的时候，prenentDefault();
	


### 16.9.11
发现 切换 `tag` 时样式变化错误的 [bug](http://stackoverflow.com/questions/39443139/chrome-compute-style-error-with-transition)，尝试各种方式修复不能。

### 16.9.12
缩小了列表页，文章标题下 `tag` 的字体大小，由于有时候 `tag` 过多、过长，选中增大以后会比较难看。

在 `Widget` 组件中对 `shouldComponentUpdate` 做了一个单独处理：

```javascript
shouldComponentUpdate(nextProps, nextState) {
    return nextState.nowTag != this.state.nowTag;
}
```
由于 `shouldComponentUpdate ` 默认返回 `true`，故会造成一些不必要的更新（`Widget` 的 `props` 由 `App(Root Component)` 传入，又由 `App` 的某个子组建来更新，故 `Widget` 会被多次触发相同 `tag` 的 更新）。


### 16.9.13
瞎忙一天，就为了解决这个问题：[css-absolute-element-hid-by-overflow-auto](http://stackoverflow.com/questions/39463285/css-absolute-element-hid-by-overflow-auto)。

目前发现的是 `chrome` 解析没有父级约束 `.parent{ position: relative; }` 的元素的时候，在 `.grandpa {overflow: auto}` 存在并且 **触发滚动** 的时候，判断独立的 `absolute` 元素会基于其原有位置。

这个问题留待解决啊。

P.S. 感冒了，脑子不是很清醒。

### 16.9.14
#### [css-absolute-element-hid-by-overflow-auto](http://stackoverflow.com/questions/39463285/css-absolute-element-hid-by-overflow-auto)
感谢 `stackoverflow` 的小哥给出的解决方案：[jsfiddle](https://jsfiddle.net/TheBigDMo1/k2ahruyb/4/)，他的坚持不懈真是让我倍感羞愧。这个问题我还是准备先留一下，看看（不久的）将来有没有更好的解决方案。

####





    
    