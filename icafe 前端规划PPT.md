title: icafe项目前端规划
speaker: 杭永胜
transition: fade
highlightStyle: monokai_sublime

[slide class="title-slide"]
# icafe项目前端规划
<small>杭永胜</small>

[slide]
## 起点
-----------------------------------
>以提升页面性能和规范开发为基础，前端采用fis-java-jsp解决方案为基础

[slide]
## 目前存在的问题
-----------------------------------
>目前js方面的问题比较突出，主要集中在如下几个方面：

- 代码结构不清晰
- 代码编写没有统一的约定和规范
- 很多代码存在重复加载
- 网站性能低下已经影响到用户体验

[slide]
## 解决思路
------------------------------------
- 约定命名规范、目录规范、中英文对照表等为项目持续开发提供参考。
- 以组件化思路开发,引入fis来实现前端资源的管理和代码的合并压缩等优化操作。
- 转换开发思路，切分页面功能为多个组件(widget)，提高组件的通用性，最后达到**页面=(组件+组件)**的模式。
- 杜绝组件之间的相关引用，使用全局事件机制来实现组件间解耦。
- 提供统一的组件封装模板，规范前端代码。


[slide]
##开发规范参考
------------------------------------
- 公司[《CSS编码规范》](http://styleguide.baidu.com/style/css/index.html)
- 公司[《HTML编码规范》](http://styleguide.baidu.com/style/html/index.html)
- 公司[《JavaScript编码规范》](http://styleguide.baidu.com/style/js/index.html)
- 推荐[《淘宝alice css规范和最佳实践》](http://aliceui.org/docs/rule.html)


[slide]
##[fis-java-jsp](https://github.com/fouber/fis-java-jsp)构建方案
--------------------------------------
+ FIS是专为解决前端开发中自动化工具、性能优化、模块化框架、开发规范、代码部署、开发流程等问题的工具框架，.FIS针对不同后端语言定制了不同的解决方案，如fis-plus，jello等

[slide]
###  源代码目录示例
--------------------------------------
>前端文件全部存放在mario-web\src\main\webapp下，包括js、css、img、jsp等等其他静态资源

```
+---pages
    +---common //通用模块，第三方库以及公共组件
    |   +---lib
    |   |   +---jquery
    |   |   +---mod
    |   +---widget
    |   |   +---topbar
    +---demo  //业务模块 demo
    |   +---widget //组件目录
    |   |   +---header
    |   |   |   +---img
    |   |   |   \---header.js
    |   |   |   \---header.css
    |   |   |   \---header.jsp
    |   |   +---body
    |   |   +---footer
    |   |   +---list
    |   |   +---nav
    |   +---static //page static目录
    |   |   +---index //目录名与jsp页面一一对应
    |   |   |   \---index.js
    |   |   |   \---index.css
    |   |---index.jsp
    |   |---***.jsp
    +---issue  //卡片模块
    +---space  //空间模块
    +---***业务模块与后端模块一一对应
```
[slide]
###  编译后目录示例
>fis编译后前端代码放到mario-fis，后端用来做指向的jsp,【此目录不上传到svn】

```
+---mario-fis
    +---pages
    |   +---common //通用模块，第三方库以及公共组件
    |   |   +---widget
    |   +---demo  //业务模块 demo
    |   |   +---widget //组件目录
    |   |   |   +---header
    |   |   |   |   |---header.jsp
    |   |   |   +---body
    |   |   |   +---footer
    |   |   |   +---list
    |   |   |   +---nav
    |   |   |---index.jsp
    |   |   |---***.jsp
    |   +---issue  //卡片模块
    |   +---space  //空间模块
    |   +---***业务模块与后端模块一一对应
    +---resources //静态资源目录
        +---pkg   //通过fis-conf配置后的合并文件
    |   |    |---lib.js
    |   +---demo  //业务模块 demo
    |   |   +---widget //组件目录
    |   |   |   +---header
    |   |   |   |   +---img
    |   |   |   |   |---header.js
    |   |   |   |   |---header.css
    |   |   |   +---***
    |   |   +---static //page static目录
    |   |   |   +---index //目录名与jsp页面一一对应
    |   |   |   |   |---index.js
    |   |   |   |   |---index.css
    |   +---map
    |   |   |---map.json
```
[slide]
### widget组件示例-header.jsp

```
<%@ taglib uri="/fis" prefix="fis"%>
<div class="header">
    <div class="header-banner"><img src="img/w6.jpg"/></div>
    <div class="header-nav">
        <jsp:include page="../nav/nav.jsp"/>
    </div>
</div>
<fis:require id="demo/widget/header/header.css"/>
<fis:require id="demo/widget/header/header.js"/>
<fis:script>
    var header = require('demo/widget/header/header.js');
    header.show('header loaded');
</fis:script>
```
header.js
```
/*global exports*/
exports.show = function(msg) {
    window.console.log(msg);
};
```

[slide]
###  page页面示例-index.jsp
```
<%@ page contentType="text/html;charset=utf-8" %>
<%@ taglib uri="/fis" prefix="fis"%>
<%-- 使用<fis:html>标签替代传统<html>标签o，并设置map.json文件部署路径，缺省是“/” --%>
<fis:html mapDir="/map"> 
    <head>
        <meta charset="utf-8"/>
        <title>my jsp page</title>
        <%-- 使用<fis:require>替代传统<link href>、<script src>标签来加载静态资源 --%>
        <fis:require id="common/lib/jquery/jquery-1.7.1.min.js"/>
        <fis:require id="common/lib/mod/mod.js"/>
        <%-- 使用<fis:styles/>标签显示<fis:require>标签收集到的所有css资源 --%>
        <fis:styles/>
    </head>
    <body>
        <div class="main">
            <div class="main-header">
                <jsp:include page="widget/header/header.jsp" flush="true"/>
            </div>
            <div class="main-body">
                <jsp:include page="widget/body/body.jsp" flush="true"/>
            </div>
            <div class="main-footer">
                <jsp:include page="widget/footer/footer.jsp" flush="true"/>
            </div>
        </div>
        <%-- 在其他widget加载完毕后再加载页面的js、css，效果更好 --%>
        <fis:require id="demo/static/index/index.css"/>
        <fis:require id="demo/static/index/index.js"/>
        <%-- 使用<fis:script>标签代替传统<script>标签，它可以帮你收集页面上的js统一放到尾部 --%>
        <fis:script>console.log('1111');</fis:script>
        <%-- 使用<fis:scripts/>标签显示<fis:require>标签收集到的所有js资源 --%>
        <fis:scripts/>
    </body>
</fis:html>
```

[slide]
###  page页面访问后的源代码
```
<html>
<head>
<title>my jsp page</title>
<link rel="stylesheet" type="text/css" href="/resources/demo/widget/header/header.css"/>
<link rel="stylesheet" type="text/css" href="/resources/demo/widget/body/body.css"/>
2q
 * 需要传入的参数全部包裹在一个对象里
 * @param {Object} opt {self:$('#id')}
 */
function Widget(opt) {
    //所有属性使用this._propertyName来命名，并且尽量写到构造函数里,包括在未来才可赋值的属性
    this._self = opt.self;
    this.init();
}
$.extend(Widget.prototype, {
    //组件业务逻辑执行唯一入口
    init:function(){
        this.bindEvent();
        this.otherFun();//其他执行函数
    },
    //组件节点事件绑定入口,所有事件绑定相关的函数放在这个里面
    bindEvent: function(){
        this.bindNodeName();
    },
    //事件绑定相关需以“bind+节点功能名称”命名如：bindSubmitBtn,
    bindNodeName:function(){},//一个方法内建议只绑定一个节点事件
    //渲染UI界面相关的函数建议以“rander+界面功能名”
    renderUIName: function(){},
    //其他执行函数，尽量一个执行函数内代码不超过50行
    otherFun: funciton(){}
});
module.exports = Widget;
```

[slide]
## 全局事件机制
---------------------------------------
+ 全局事件基于观察者模式设计，是封装在window上的一个单例，用于隔离组件间的耦合关系

```
window.PAGE_EVENT = require('common/widget/event/pageEvent.js');//引入全局事件
//订阅方
window.PAGE_EVENT.on('task-filter-change', function(data) {
    doSomeThing(data);
});
//发布方
window.PAGE_EVENT.fire('task-filter-change',data);
```


[slide]
##fis开发环境配置
-----------------------------------
###fis是基于node的前端集成工具，需要先安装node

+ **安装node** 打开[官网](http://nodejs.org),点击绿色的INSTALL按钮即可;
+ **安装fis** 执行如下命令安装fis
```
npm install -g fis
```

[slide]
##FIS开发命令
+ 打开cmd执行如下命令，不要关闭cmd窗口,fis会编译并监控webapp目录下的内容到mario-fis目录下
```
fis release -r .\mario-web\src\main\webapp -opwd .\mario-fis 
```
//o压缩，p打包，w实时监控，d目标目录，d参数需放在最后面
