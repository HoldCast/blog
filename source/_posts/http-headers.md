title: 前端获取服务器时间及其他Headers信息
tags:
    - http
    - header
    - 服务器时间
---
前端页面访问服务器时,获取服务器返回的http请求回来的header信息,如下图:
![](/assets/img/header.png)
获取Response Header的方法:
<!-- more -->
1.js-ajax方法获取:
```
function ajax(){
    var xhr = null;
    if(window.XMLHttpRequest){
      xhr = new window.XMLHttpRequest();
    }else{ // ie
      xhr = new ActiveObject("Microsoft")
    }
    // 通过get的方式请求当前文件
    xhr.open("get","/");
    xhr.send(null);
    // 监听请求状态变化
    xhr.onreadystatechange = function(){
        if(xhr.readyState===2){
            var time = xhr.getResponseHeader("Date");
            var curDate = new Date(time);
        }
    }
  }
```
2.jquery-ajax方法获取:
```
$.ajax({
    type: 'HEAD', // 获取头信息，type=HEAD即可
    url : window.location.href,
    complete: function(xhr,data){// 获取相关Http Response header
        var wpoInfo = {
            "date" : xhr.getResponseHeader('Date'),// 服务器端时间
            "contentEncoding" : xhr.getResponseHeader('Content-Encoding'),// 如果开启了gzip，会返回这个东西
            "connection" : xhr.getResponseHeader('Connection'),// keep-alive ？ close？
            "contentLength" : xhr.getResponseHeader('Content-Length'),// 响应长度
            "server" : xhr.getResponseHeader('Server'),// 服务器类型，apache？lighttpd？
            "vary" : xhr.getResponseHeader('Vary'),
            "transferEncoding" : xhr.getResponseHeader('Transfer-Encoding'),
            "contentType" : xhr.getResponseHeader('Content-Type'),// text/html ? text/xml?
            "cacheControl" : xhr.getResponseHeader('Cache-Control'),
            "exprires" : xhr.getResponseHeader('Exprires'),// 生命周期？
            "lastModified" : xhr.getResponseHeader('Last-Modified')
        };
        var curDate = new Date(wpoInfo.date);
    }
});
```
!!!
注意:通过header获取的时间是格林威治时间,北京时间与格林威治时间或UTC时间相差8个时区，北京、上海、重庆位于东8区，
所以北京时间过了8小时,获取之后记得换算成北京时间!!!
