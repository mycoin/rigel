cloaked-wookie
==============

简易的项目常用的函数整理。


## MVC基本职责

   * View 提供批量绑定事件，解除事件的方法、 模板的基本渲染。
   * Model 基本的数据读取/写入，最好支持多级操作，例如 `set('userInfo.isLogin', true)`，异步请求统一分发管理。
   * Action 控制器监听 `View`，以及 `Model`抛出来的事件，配置Model需要的数据，操控View视图。

## get started


### 视图层

```javascript
var view = View.create({
    init: function(d) {
        var me = this;
        this.renderList();
        
        // 通知View以及就绪
        me.trigger('ready');
    },

    // HTML模板代码，etpl
    template: require('template/common'),

    // 批量绑定事件，在ready之后执行
    event: {
        '@[tap] .lisy>li': function(e, el) {
            console.log('delegate');
        },

        '![tap] .form .sin': function(e, el) {
            console.log('只执行一次');

            // return false; 阻止Once功能
        },

        // 普通事件绑定
        '[tap] .form .submit': function(e, input) {
            console.log('login..');
            this.trigger('login', [1, {}]); // 发布消息，在Action里面监听
        }
    },

    // 事件绑定OK后的执行函数
    ready: function() {
        console.log('DOM ready')
    },

    // 自定义函数，一般在Action里面 this.view.xxxx() 使用
    renderList: function() {
        this.render('test', {}, '#main .list');
    }
});
```


### 模型层
``` javascript
var model = Model.create({
    // 页面数据
    data: {
        sugg: {
            val1: '百度',
            list: [1, 2, 3, 4],
            q: true
        }
    },

    init: function(r) {
        this.setData('sugg.q', false);
        this.param('id', 123);
    },

    queryList: function(name) {
        var param = this.param();
        param.name = name;
        this.request('query.php', param, function (data) {
            // xxxx, 清理啊什么等
            this.trigger('queryfinish', data);
        });
    }
});
```


### 控制器
``` javascript
var action = Action.create({
    view: view,
    model: model,

    // 事件
    event: {
        'view:login': function(arg0, arg1) {
            console.log('view login..');
            this.model.queryList(arg1);
        },

        'view:queryfinish': function () {
            this.view.render('index', data, '#main .query-list');
        }
    },

    // Model 初始化的参数
    datasource: {
        model: 1
    },
    // View 初始化的参数
    config: {
        'id': 123456,
        'agg': {
            dio: [1, 2, 3]
        }
    },

    init: function () {
        /// init
    }
});

action.init();
```
