---
title: What CORS is
category: Computer Science
order: 1
---

# 跨源资源共享（CORS）


## 名词解释：
### 跨域(cross-orgin)：
    一个url是由：协议、域名、端口 三部分组成,当一个网页向另一个网页发起请求时，请求的url的协议、域名、端口三者之间的任意一个与当前页面url不同即为跨域
![avatar](./statics/cors01.png)

### 同源策略(same-orign policy)：
    同源策略是一种约定，它是浏览器核心也最基本的安全功能，它会阻止一个域的js脚本和另外一个域的内容进行交互，如果缺少了同源策略，浏览器很容易受到XSS、CSRF等攻击。
    所谓同源（即在同一个域）就是两个页面具有相同的协议（protocol）、主机（host）和端口号（port）。
    

### 跨域资源共享(Cross-origin resource sharing)：
    用于让网页的受限资源能够被其他域名的页面访问的一种机制。通过该机制，页面能够自由地使用不同源（英语：cross-origin）的图片、样式、脚本、iframes以及视频。[2]一些跨域的请求（特别是Ajax）常常会被同源策略（英语：Same-origin policy）所禁止的。跨源资源共享定义了一种方式，为的是浏览器和服务器之间能互相确认是否足够安全以至于能使用跨源请求（英语：cross-origin requests）。比起纯粹的同源请求，这将更为自由和功能性的（functionality），但比纯粹的跨源请求更为安全。

跨域资源共享是一份浏览器技术的规范，提供了 Web 服务从不同网域传来沙盒脚本的方法，以避开浏览器的同源策略[4]。


## 解决跨域的常用方法
1. 代理：  
    一般有前端实现，
    原理是利用同源策略只会作用于浏览器-服务之间，而不限制服务-服务的通信。所以我们可以通过像nginx这种代理工具或者是自己在前端写个代理将请求放在同源环境下处理。

    正向代理：a不能直接访问b，但中间有个服务器c，c转发a的请求给b，b再把资源给c，c再给a;（作用：解决访问限制，提供安全保障）
    反向代理：a不能直接访问b，但a可以访问c，c可以从b拿到a需要的资源,代理b处理a的请求，那么a访问c拿到b的资源，这个就是反向代理，a始终不知道c的资源是从哪来的，也不知道b的存在。(作用：负载均衡，提高访问速度，提供安全保障)

2. CORS:  
    前端和后端均可实现，
    本质上是服务端的响应头添加一些跨域配置信息：
    Access-Control-Allow-Credentials: true,
    Access-Control-Allow-Origin: *,
    Access-Control-Allow-Headers: 'header',
    Access-Control-Expose-Headers: 'serve-header',
    Access-Control-Allow-Methods: 'methods',
    Access-Control-Max-Age: '1800', // 30min = 1800s
    这一步在很多后端框架的三方库中已实现自动处理了，所以用后端处理CORS直接用三方库即可



3. nginx跨域和cors区别:  
    Nginx是间接跨域，而CORS则实现了直接跨域。Nginx的反向代理“欺诈了”浏览器，所以浏览器和服务器都认为是同源访问，所以Session不会丢失。（PS：如果发生跨域访问，服务器会每次都创建新的Session，所以才造成了前后端分离的Session丢失问题。） 至于CORS这种跨域机制的安全性和灵活性更高，但需要自己解决跨域访问Session丢失的问题，通常情况可以采用Session+Redis来实现Session共享。）


## 项目实践
以oceanus platform项目为例，该项目是以flask作为后端框架，以react作为前端，
按照以上所述，在本项目中采用的是使用第三方库flask-cors实现，将flask-cors导入后，一旦有跨域的请求，服务端响应就会自动添加一些附加的头信息，有时还会多出一次附加的请求，

## 链接
1. http://www.ruanyifeng.com/blog/2016/04/cors.html
2. https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS
3. 解决跨域的10种方案：https://segmentfault.com/a/1190000022398875

