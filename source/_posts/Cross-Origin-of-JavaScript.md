title: 初涉JS 跨域
date: 2016-02-25 16:57:48
categories:
tags: [js]
---
最近在公司项目中真真实实的接触到了跨域，相比之前的纸上谈兵，这一次也是长了不少见识，总结一下：


#### 1.什么是跨域：
&nbsp;&nbsp;&nbsp;&nbsp;由于JavaScript **_同源策略_** 的限制，不允许跨域调用其他页面的对象。何为“同源策略”呢？同源策略，它是由Netscape提出的一个著名的安全策略，为了防止页面资源被随意或恶意修改，以保证数据的安全性，现在所有的可支持javascript的浏览器都会使用这个策略。同源策略规定 **_跨域之间的脚本是隔离的，一个域的脚本不能访问和操作另外一个域的绝大部分属性和方法_**。 所以当你请求或访问某一些数据时，当前地址与请求地址只要 协议、域名、端口任意一个不同，就形成了跨域。需要注意的是，前端手法可以解决的是域名不同的这种跨域，而协议和端口上的跨域还要由后端来解决。
  
### 2.解决跨域的方法
##### 1）跨域资源共享（Cross-Origin Resource Sharing）
&nbsp;&nbsp;&nbsp;&nbsp; CORS，基本思想就是使用自定义的HTTP头部让浏览器与服务器通信，也就是使用绝对路径，注意：服务器端对于CORS的支持，主要就是通过设置Access-Control-Allow-Origin来进行的。如果浏览器检测到相应的设置，就可以允许Ajax进行跨域的访问。
&nbsp;&nbsp;&nbsp;&nbsp;缺点：对老版本浏览器支持的不好。

_//单项通信_
#### 2）JSONP
&nbsp;&nbsp;&nbsp;&nbsp;JSONP也叫填充式JSON，是应用JSON的一种新方法，只不过是被包含在函数调用中的JSON,是资料格式 JSON 的一种“使用模式”，可以让网页从别的网域要资料。JSONP由两部分组成：回调函数和数据。回调函数是当响应到来时应该在页面中调用的函数，而数据就是传入回调函数中的JSON数据。jsonp是需要服务器端的页面进行相应的配合的。

    <script type="text/javascript">
      function callback(jsondata){
              //处理获得的json数据
          }
    </script>
    <script src="http://example.com/data.php?callback=dosomething"></script>
    
&nbsp;&nbsp;&nbsp;&nbsp;JSONP的优点是：它不像XMLHttpRequest对象实现的Ajax请求那样受到同源策略的限制；它的兼容性更好，在更加古老的浏览器中都可以运行，不需要XMLHttpRequest或ActiveX的支持；并且在请求完毕后可以通过调用callback的方式回传结果。
&nbsp;&nbsp;&nbsp;&nbsp;JSONP的缺点则是：它只支持GET请求而不支持POST等其它类型的HTTP请求；它只支持跨域HTTP请求这种情况，不能解决不同域的两个页面之间如何进行JavaScript调用的问题。


#### 3 ) window.name
#### 4 ) flash URLLoader
#### 5 )Access Control
#### 6 ) Server Proxy
//双向通信
#### 7 )document.domain
#### 8 ) window.postMessage
#### 9 ) Cross Frame
#### 10)FIM-Fragment Identitier Messaging

