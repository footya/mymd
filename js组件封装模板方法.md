#js组件封装模板方法[草稿]#
>为了增强团队代码可读性和可维护性，计划约束组件的编写方式，组件初始化方式以及方法命名提供指导性建议

##示范代码##

    ```
    /**
     * 组件封装示例
     * 需要传入的参数全部包裹在一个对象里
     * @param {Object} opt {el:''}
     */
    define(function(require, exports, module) {
        function Widget(opt) {
            //所有属性使用this._propertyName来命名，并且尽量写到构造函数里,包括在未来才可赋值的属性
            this._el = opt.el;
            this.init();
        }
        $.extend(Widget.prototype, {
            /**
             * 组件业务逻辑执行唯一入口
             */
            init:function(){
                this.bindEvent();
                this.otherFun();//其他执行函数
            },
            /**
             * 组件节点事件绑定入口,所有事件绑定相关的函数放在这个里面
             */
            bindEvent: function(){
                
            },
            /**
             * 事件绑定相关需以“bind+节点功能名称”命名如：bindSubmitBtn,一个方法内建议只绑定一个节点事件
             */
            bindNodeName:function(){
                //
            },
            /**
             * 渲染UI界面相关的函数建议以“rander+界面功能名”
             */
            renderUIName: function(){

            },
            /**
             * 其他执行函数，尽量一个执行函数内代码不超过50行
             */
            otherFun: funciton(){

            },
            //接口看情况尽量通过事件对外暴漏
            /**
             * [自定义事件] 事件绑定
             * @param  {String} name 自定义事件名
             * @param  {Function} fun 回调函数
             */
            on: function(name, fun) {
                if (!this.events[name]) {
                    this.events[name] = [];
                }
                this.events[name].push(fun);
            },
            /**
             * [自定义事件] 事件触发
             * @param  {String} name 事件名
             * @param  {Object} data 数据
             */
            fire: function(name, data) {
                if (name in this.events[name]) {
                    while (this.events[name].length > 0) {
                        this.events[name].shift()(data);
                    }
                }
            }
        });
        module.exports = Widget;
    });
    ```

