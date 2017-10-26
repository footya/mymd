title: 前端框架San学习
speaker: 杭永胜
transition: fade
theme: moon
highlightStyle: monokai_sublime
<script src="http://static.jsbin.com/js/embed.min.js?4.1.0"></script>
[slide class="title-slide"]
<div class="center"><img src="/logo-colorful.svg" width="80"/></div>
# 前端框架San学习
<small>杭永胜</small>

[slide]
## san是什么
-----------------------------------
- 由百度EFE 团队开发
- 一个传统的MVVM组件框架
- san不是单词就是三的拼音

[slide]
## san 有什么
-----------------------------------
- HTML模板
- 数据驱动
- 组件化
- 高性能视图
- 组件反解
- 体积小巧 <10k (gzip)
- 浏览器兼容到IE8

[slide]
## san 怎么用
1. cdn 引用
```
// 开发版本
<script src="https://unpkg.com/san@latest/dist/san.dev.js"></script>
// 生产版本
<script src="https://unpkg.com/san@latest"></script>
```

2. npm install
```
npm install san
```

[slide]
## Hello World
------------------------------------
```
var MyApp = san.defineComponent({
    template: '<p>Hello {{name}}!</p>',
    initData: function () {
        return {name: 'world'};
    }
});
var myApp = new MyApp();
myApp.attach(document.body);
```
<a class="jsbin-embed" href="http://jsbin.com/huyudatuwe/embed?html,output">JS Bin on jsbin.com</a>


[slide]
## 列表
```
var MyApp = san.defineComponent({
    template: '<ul><li s-for="item in list">{{item}}</li></ul>',
    attached: function () {
        this.data.set('list', [1, 2, 3, 4, 5]);
    }
});
var myApp = new MyApp();
myApp.attach(document.body);
```
<a class="jsbin-embed" href="http://jsbin.com/cijagok/embed?html,output">JS Bin on jsbin.com</a>


[slide]
## 双向绑定
```
var MyApp = san.defineComponent({
    template: ''
        + '<div>'
        +   '<input value="{= name =}" placeholder="please input">'
        +   'Hello {{name}}!'
        + '</div>'
});
var myApp = new MyApp();
myApp.attach(document.body);
```
<a class="jsbin-embed" href="http://jsbin.com/katahoc/embed?html,output">JS Bin on jsbin.com</a>


[slide]
## 数据操作

- 初始化
```
san.defineComponent({
    initData: function () {
        return {
            width: 200,
            top: 100,
            left: -1000
        };
    }
});
```

[slide]
- set get
```
san.defineComponent({
    attached: function () {
        requestUser().then(this.userReceived.bind(this));
    },
    userReceived: function (data) {
        this.data.set('user', data);
    },
    changeEmail: function (email) {
        this.data.set('user.email', email);
    },
    getUser: funciton (data) {
        return this.data.get('user');
    }
});
```


[slide]
- 数组操作
```
san.defineComponent({
    flag: function () {
        // 修改数组项直接用set
        this.data.set('users[0].flag', true);
    },
    addUser: function (name) {
        this.data.push('users', {name: name});
        // this.data.unshift('users', {name: name});
    },
    rmOne: function () {
        this.data.pop('users');
        // this.data.shift('users');
    },
    rm: function (user) {
        this.data.remove('users', user);
    },
    rmAt: function (index) {
        this.data.removeAt('users', index);
    },
    rmto: function (index, deleteCount) {
        this.data.splice('users', [index, deleteCount]);
    }
});
```

[slide]
## 过滤器

过滤器之间类似管道的方式前一个的输出做为后一个的输入向后传递
```
{{ expr [[| filter-call1] | filter-call2...] }}
```

内置过滤器：
- html HTML转义
- url URL转义
- raw 不进行转义


[slide]
## 自定义过滤器
```
var MyApp = san.defineComponent({
    template: ''
        + '<div>'
        +   '<input value="{=name=}" placeholder="please input">'
        +   'Hello {{name | upper | replaceToOther("A", "-")}}!'
        + '</div>',
    filters: {
        upper: function (value) {
            return value && value.toLocaleUpperCase();
        },
        replaceToOther: function (value, from, to) {
            var reg = new RegExp(from, 'g');
            return value && value.replace(reg, to);
        }
    }
});
var myApp = new MyApp();
myApp.attach(document.body);
```

[slide]
<a class="jsbin-embed" href="http://jsbin.com/zesuso/embed?html,output">JS Bin on jsbin.com</a>


[slide]
## 组件反解
> 组件初始化时传入 el，其将作为组件根元素，并以此反解析出视图结构。

- html模板直接输出，轻松缩短首屏时间
- 无需依赖node，任何后端语言都可以
- 静态页面也可以实现首屏渲染

[slide]
## 见证奇迹的时刻！
<a class="jsbin-embed" href="http://jsbin.com/puriwuv/embed?html,output">JS Bin on jsbin.com</a>


[slide]
## 怎么做到的？

- 组件模板直接输出到dom树，通过注释添加标记
```
<div id="test-el">
  <input prop-value="{=name=}" value=""/>
  <button on-click="changeName">change name</button>
  Hello <span><!--s-text:{{name}}-->errorrik<!--/s-text--></span>
</div>
```

- 组件通过传入dom节点，完成行为管理和视图刷新
```
var MyApp = san.defineComponent({
  changeName: function () {
    this.data.set('name', 'world');
  }
});
var myApp = new MyApp({el: document.getElementById('test-el')});
myApp.attach(document.body);
```


[slide]
## 事件处理 - DOM事件
- DOM事件 [demo](http://jsbin.com/jokomag/edit?html,output)
```
san.defineComponent({
    initData: function () {
        return {title: 'test'}
    },
    template: '<button type="button" on-click="submit">submit</button>',
    submit: function () {
        var title = this.data.get('title');
        alert(title);
    }
});
```

[slide]
## 事件处理 - 自定义事件
[demo](http://jsbin.com/buxubiy/edit?html,output)
```
var Label = san.defineComponent({
    template: '<div class="ui-label" title="{{text}}">{{text}}</div>',
    initData: function(){
        return {text: 'demo'}
    },
    attached: function () {
        this.fire('done', this.data.get('text') + ' done');
    }
});
var MyComponent = san.defineComponent({
    template: '<div><ui-label bind-text="name" on-done="labelDone($event)"></ui-label></div>',
    components: {
        'ui-label': Label
    },
    labelDone: function (doneMsg) {
        alert(doneMsg);
    }
});
var myApp = new MyComponent();
myApp.attach(document.body);
```

[slide]
## 组件
> san 框架的基本单位，功能集合的最小单元


[slide]
### 组件定义 — 原型链继承

```
// 原型链继承 [demo](http://jsbin.com/xaxinod/edit?html,output)
function MyApp(options) {
    san.Component.call(this, options);
}
san.inherits(MyApp, san.Component);
MyApp.prototype.template = '<div>{{name}}</div>';
MyApp.prototype.attached = function () {
    this.data.set('name', 'hello');
};
new MyApp().attach(document.body);
```

[slide]
### 组件定义 - ESNext

```
// ESNext 写法
import {Component} from 'san';
class MyApp extends Component {
    constructor(options) {
        super(options);
    }
    static template = '<div>{{name}}</div>';
    attached () {
        this.data.set('name', 'hello');
    }
}
new MyApp().attach(document.body);
```

[slide]
### 组件定义 - 简单写法

```
// 不用ESNext
var MyApp = san.defineComponent({
    template: '<div>{{name}}</div>',
    attached: function () {
        this.data.set('name', 'hello');
    }
});
new MyApp().attach(document.body);
```

[slide]
## 组件生命周期
<img src="/life-cycle.png" height="520">


[slide]
## 组件生命周期
- compiled - 组件视图模板编译完成
- inited - 组件实例初始化完成
- created - 组件元素创建完成
- attached - 组件已被附加到页面中
- detached - 组件从页面中移除
- disposed - 组件卸载完成

[slide]
## 视图模板
```
san.defineComponent({
    template: '<div>{{name}}</div>',
    // template: require('./template.html'),
    initData: function () {
        return {
            name: 'san'
        };
    }
});
```

[slide]
## 视图模板-slot
```
var Panel = san.defineComponent({
    template: '<div>'
        + '  <div class="head" on-click="toggle">title</div>'
        + '  <div style="{{fold | yesToBe(\'display:none\')}}"><slot></slot></div>'
        + '</div>',
    ....
});
var MyComponent = san.defineComponent({
    components: {
        'ui-panel': Panel
    },
    template: '<div><ui-panel><h1>Hello San</h1></ui-panel></div>'
});
new MyComponent().attach(document.body);
/* MyComponent渲染结果
<div>
  <div class="head">title</div>
  <div style="display:none"><h1>Hello San</h1></div>
</div>
*/
```

[slide]
## 视图模板-slot demo
<a class="jsbin-embed" href="http://jsbin.com/dajinib/embed?html,output">JS Bin on jsbin.com</a>

[slide]
## 组件嵌套
```
<!-- Template -->
<div class="form">
    <div>预期完成时间：
        <ui-calendar value="{= endTimeDate =}" s-ref="endDate"></ui-calendar>
        <ui-timepicker value="{= endTimeHour =}" s-ref="endHour"></ui-timepicker>
    </div>
    <div class="form-op">
        <button type="button" on-click="submit">ok</button>
    </div>
</div>
```
```
var AddForm = san.defineComponent({
    // template
    components: {
        'ui-timepicker': require('../ui/TimePicker'),
        'ui-calendar': require('../ui/Calendar')
    },
    submit: function () {
        //可以调用组件的方法
        this.ref('endDate').xxx
        this.ref('endHour').xxx
    }
});
```

[slide]
## 组件调用
<div class="columns-2">
<pre>
<h3>父组件调用子组件</h3>
<code>this.ref('xxx').xxxfun</code>
</pre>
<pre>
<h3>子组件调用父组件</h3>
<code>this.owner.xxx</code>
</pre>
</div>
<a class="jsbin-embed" href="http://jsbin.com/vaqisis/embed?html,output">JS Bin on jsbin.com</a>

[slide]
## messages
> 组件可以向组件树的上层派发消息。

```
san.defineComponent({
    components: {
        'ui-select': Select,
        'ui-selectitem': SelectItem
    },
    template: ''
        + '<div>'
        + '  <ui-select value="{=value=}">'
        + '    <ui-selectitem value="1">one</ui-selectitem>'
        + '    <ui-selectitem value="2">two</ui-selectitem>'
        + '    <ui-selectitem value="3">three</ui-selectitem>'
        + '  </ui-select>'
        + '</div>'
});
```

[slide]
### message 派发

```
var SelectItem = san.defineComponent({
    template: '<li on-click="select"><slot></slot></li>',
    select: function () {
        var value = this.data.get('value');
        // 向组件树的上层派发消息
        this.dispatch('UI:select-item-selected', value);
    }
});
```

[slide]
### message 接收
```
var Select = san.defineComponent({
    template: '<ul><slot></slot></ul>',
    // 声明组件要处理的消息
    messages: {
        'UI:select-item-selected': function (arg) {
            var value = arg.value;
            this.data.set('value', value);
            // arg.target 可以拿到派发消息的组件
        }
    }
});
```

[slide]
### messages demo
<a class="jsbin-embed" href="http://jsbin.com/yexopig/embed?html,output">JS Bin on jsbin.com</a>
