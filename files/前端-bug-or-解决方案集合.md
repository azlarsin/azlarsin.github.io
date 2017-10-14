title: 前端 bug or 解决方案集合
author: azlar
date: '2017-10-14 10:16:24'
tags: []

---

流水账式记录前端遇到的各种问题，包括不限于框架、node、浏览器问题等。
<!-- desc -->

### firefox can't drag issue
这个问题是一个同事在用我写的一个 [小库](https://github.com/azlarsin/draggable-tree) 时发现的，在火狐内不能正常拖拽。（拽不起来）

#### 解决
火狐的拖拽机制需要用户设置 setData 才会生效。

另： 设置　`text/html`　可以防止火狐拖拽结束后打开新窗口。
另2：若需在 IE 下使用，只能设置 `setData('text', something)`。

```js
dom.addEventListener("dragstart", function (e){
	e.dataTransfer.setData('text/html', null);
});
```