# DOM 事件的级别。

1. DOM0 级事件：将一个函数赋值给一个事件处理属性，例如：


```
<button id="btn"></button>
<script>
var btn = document.querySelector("#btn");
btn.onclick = function() {
console.log("click");
}

// 事件解绑
btn.onclick = null
</script>
```

DOM0 级事件处理程序的缺点在于，一个处理程序无法同时绑定多个处理函数。

2. DOM2 级事件：定义了 addEventListener 和 removeEventListener，分别用来绑定和解绑事件，该方法包含三个参数，分别为绑定的事件名，处理函数和是否在捕获时执行。例如：


```
<button id="btn"></button>
<script>
var btn = document.querySelector("#btn");

function show() {
console.log('click');
}

btn.addEventListener('click', show, false);

// 事件解绑
btn.removeEventListener('click', show, false);
</script>
```

DOM2 级事件在 DOM0 事件基础上弥补了一个处理程序无法同时绑定多个函数的问题。

> 注：IE8 及以下版本不支持 addEventListener 和 removeEventListener。

3. DOM3 级事件：DOM3 级事件在 DOM2 级事件的基础上增加了更多的事件类型，例如：blur、load、scroll、keydown 等。

> 注：由于 DOM1 级中并没有定义事件相关的内容，所以没有 DOM1 级事件。

# DOM 事件模型。

捕获和冒泡

# DOM 事件流。

1. 从 window 对象传导到目标节点上，称为"捕获阶段"。
2. 在目标节点上触发，称为"目标阶段"。
3. 从目标节点传导回 window 对象上，称为"冒泡阶段"。

# 描述 DOM 事件捕获的具体流程。

window -> document -> html 元素 -> body 元素 -> 父元素 -> 目标元素

tips: `Document.documentElement` 获取 html 元素

# Event 对象的常见应用。

event.preventDefault() 阻止默认事件

event.stopPropagation() 阻止事件冒泡

event.stopImmediatePropagation() 事件响应优先级

event.currentTarget 绑定事件的元素

event.target 点击的元素对象

# 自定义事件。

```javascript
var customEvent = new Event('custom');

el.addEventListener('custom', function() {
  console.log('custom');
});

// 触发事件
el.dispatchEvent(customEvent);
```

CustomEvent 也可自定义事件，而且可以传入参数对象。

# 页面事件的生命周期

* DOMContentLoaded：DOM树构建完毕触发，可以用JS去访问DOM节点
  * 图片等资源有可能没有加载完毕
  * defer和async加载的脚本可能没有执行
* load：页面所有资源加载完毕
* beforeunload：用户即将离开页面时触发的事件，它会返回一个字符串用来询问用户是否离开
* unload：用户已经离开时触发
* document.readyState：表示页面的加载状态，可以在readystatechange事件中监听页面变化状态
  * loading：页面加载中
  * interactive：页面解析完毕，时间上和DOMContentLoaded同时发生，但是先触发interactive状态
  * complete：页面所有资源加载完毕，与load同时发生，但是先触发complete状态

# 点击事件穿透

* 实现点击事件穿透（遮罩层蒙层点击）：
  * 借助pointer-events: none;实现点击穿透，pointer-events: auto恢复点击处理

* 阻止点击事件穿透：
  * 不要混用touch和click
  * 借助fastclick，貌似最新浏览器已经不需要了
  * 延长蒙层的消失时间

