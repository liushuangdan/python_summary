ajax是什么?
===

----

**AJAX 是与服务器交换数据并更新部分网页的艺术，在不重新加载整个页面的情况下。**

> AJAX 指异步 JavaScript 及 XML（Asynchronous JavaScript And XML）。
> 
> AJAX 是一种在 2005 年由 Google 推广开来的编程模式。
> 
> AJAX 不是一种新的编程语言，而是一种使用现有标准的新方法。
> 
> 通过 AJAX，你可以创建更好、更快以及更友好的 WEB 应用程序。
> 
> AJAX 基于 JavaScript 和 HTTP 请求（HTTP requests）。


**通过 HTTP 请求加载远程数据**

**jQuery 底层对 AJAX 实现进行了封装.使得我们在进行ajax操作时,不必像原生js中那么复杂**

**`$.get`, `$.post`, `$.ajax()` 返回其创建的 XMLHttpRequest 对象。多数情况下我们不需要去操作返回的对象**


* ### 如何使用ajax技术?

    > 首先你得有web服务器,能够通过浏览器去执行你的html和你的python

    > 注意一点:我们平常写的html,直接在浏览器打开时 使用的是file协议
    > 而ajax是基于HTTP请求的,所以要求你的html能够使用http的协议打开
    >如果你能做到用http协议去打开你的html并且能够正常显示的话,就代表你的web服务器搭建成功

    * ##### $.get() 方法:

        ```js
        //发送ajax请求 1.url  2.可选 发送get请求时携带的参数  ,3,可选 回调函数,请求完之后做什么事  4,可选,返回的数据类型 json

        $.get(url,{请求的参数},function(data){},'json')
        ```

    * ##### $.post()

        ```js
        $.post(url,{请求的参数},function(data){},'json')
        ```

    * ##### $.ajax()

        ```js
        $.ajax({
            url:'/cgi-bin/5.py',//当前请求的url地址
            type:'get',//当前请求的方式 get  post
            data:{id:100,username:'zhangsan'},//请求时发送的参数
            dataType:'json',//返回的数据类型
            success:function(data){
                //ajax请求成功后执行的代码
                console.log(data);
            },
            error:function(){
                //ajax执行失败后执行的代码
                alert('ajax执行错误');
            },
            timeout:2000,//设置当前请求的超时时间  毫秒,必须时异步请求才会生效
            async:true// 是否异步  true为异步  false 同步
        })
        ```

* ### ajax异步 同步

    ```js
    //设置ajax的全局配置  async:false 设置当前请求为同步
    $.ajaxSetup({
        async:false
    })

    关于ajax中 异步 和 同步 

    ajax默认就是异步请求,

    async (默认: true) 默认设置下，所有请求均为异步请求。
    如果需要发送同步请求，请将此选项设置为 false。

    同步请求,就发ajax请求发出去后必须等待ajax的结果返回后才能继续往下执行

    一般情况下都使用异步操作就可以,除非有特殊情况,必须等ajax的结果回来后才能做处理的,就用同步
    ```

* ### 注意

    ```js
    1.ajax是无刷新请求服务器,所以我们在浏览器中是感觉不到,也看不到ajax的具体请求和执行情况的.,
        因此我们需要借助浏览器的调试工具 (F12打开) 进行查看

    2.ajax的请求是基础HTTP协议的,就要求你当前打开这个带有ajax的html时必须使用http协议

    3.ajax要求同源策略
        http://127.0.0.1:8000/cgi-bin/1.py
        即: 协议(http https)  域名或IP 以及端口(80 443 8000 8080 ...)都必须一致

    4.关于返回的数据类型 在get() post() ajax() 都可以设置返回的数据类型 'json'
        如果要求返回json格式数据,那么就必须返回json,如果不正确,
        在get和post方法将拿不到data中返回的数据,在ajax方法中则会进去error方法

    5.在python中返回json格式数据,
        引入 json模块
        json.dumps(数据)  使用json_dumps方法进行json格式的编码转换

    6.在使用ajax方法时.会创建一个对象 XMLHttpRequest
        那么在ajax的方法中使用的 $(this) 就代表 ajax的对象

        $(this) 永远代表一个对象,没有指明对象时 代表的时window对象,
        在它有对象时 代表的就是当前的这个对象
    ```

* ### 了解json格式数据

    json是 JavaScript Object Notation 的首字母缩写，单词的意思是javascript对象表示法，这里说的json指的是类似于javascript对象的一种数据格式，目前这种数据格式比较流行，逐渐替换掉了传统的xml数据格式。

    javascript对象字面量：
    ```js
    var tom = {
        name:'tom',
        age:18
    }
    ```

    json格式的数据：

    ```js
    {
        "name":'tom',
        "age":18
    }
    ```

    与json对象不同的是，json数据格式的属性名称需要用双引号引起来，用单引号或者不用引号会导致读取数据错误。

    json的另外一个数据格式是数组，和javascript中的数组字面量相同。

    ```js
    ['tom',18,'programmer']
    ```
