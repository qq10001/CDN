I am an outsourcer and have recently taken on a lot of website projects with front and back-end separation architecture. Since this architecture is not inherently conducive to search engine indexing, the Nuxt.js component is used to render pages on the server side to return to the spiders.
After doing more websites like this, we found that we don't need to bother at all, and we can improve the CDN and let it help to finish the task of page rendering. So there is the following solution. This program is my original, I went through Baidu, Google
I found that no one is doing it at home and abroad, and now it is the high-speed growth period of front-end and back-end separation projects, many projects need this service. I don't do CDN projects myself, so I share my idea for those who have resources to learn and implement it.
I'm not doing CDN projects myself, so I'd like to share my idea for those who have the resources to learn and implement it, so as to provide a new profitable growth point for CDN services.

**********************************************************************************************************

Problem Description.
    1. The first time a small program or mobile browser opens a web page with front and back-end separation, it loads very slowly because it needs to download a lot of js css files and then cache them locally.
    2. The front and back-end separation of the site is not conducive to search engine inclusion, such as the mall website, commodity profiles are rarely included to, resulting in dismal sales.

Application scenarios.
    1. Static first page, improve the opening speed of small programs, cell phone pages
    2. Static content page, easy to search engines included

Solution.
    Separate the front and back end of the website domain name resolution to the CDN server, CDN according to the User-Agent to determine whether it is a spider.
    If yes, then call the CDN on the client (can be Selenium ChromeDriver open source program to streamline) to static pages, the results returned to the spider.
    If not, return js, css to the user's browser to dynamically render the page.
    Note: You can deploy a separate set of upgraded CDN servers, isolated from the existing ones, to make a solution dedicated to serving front- and back-end separated websites, which will not affect the performance and throughput of the original servers.

    The advantage of using CDN to staticize pages is that it is versatile and suitable for different types of front- and back-end separated websites, and can be made into a platform [rented to] others to use.
    Reduce the amount of server-side code (no need for Nuxt.js), reduce the difficulty of deployment (no need to spider on Nginx and then route requests), and improve server performance (no need for servers to render pages).

Notes.
    CDN must be able to receive parameters that specify which pages need to be static and which pages do not need to be static.
    I hope that the CDN service provider can provide an SDK to facilitate the forwarding of Post requests to the source server, so as to hide the source server IP and improve the security of the source server.
    In addition, the SDK can also add the function of specifying a static partial page, rather than the entire page, so that the page call is more modular, convenient for programmers to splice the page, local function iteration.

Security risks.
    CDN may be hacked, hackers forged User-Agent for the search engine, and then let the CDN static the whole site page, wasting the CDN's CPU, memory resources.
    Solution: You can introduce black and white lists, and write the URLs that need to be static into the white list, so as to avoid the CDN resources being consumed by hackers.

**********************************************************************************************************

If there is a mistake in the above solution, no feasibility, I hope to leave a message to inform me, so that I can also brainstorm.


我是做外包的，最近接了很多前后端分离架构的网站项目。由于这种架构先天不利于搜索引擎收录，所以使用了 Nuxt.js 组件在服务器端渲染页面返回给蜘蛛。
这样的网站做多了，发现根本不用这么麻烦，可以改进 CDN，让 CDN 帮助完成页面渲染的任务。所以有了下面的方案。这个方案是我原创的，我翻遍了百度、Google
发现国内外现在都没有人在做，而现在正是前后端分离项目的高速成长期，很多项目需要这个服务。我自己不是做 CDN 项目，所以把我的想法分享出来，供有资源的
朋友借鉴、实施，给 CDN 服务提供一个新的盈利增长点。

**********************************************************************************************************

问题描述：
    1.小程序、手机浏览器第一次打开前后端分离的网页时加载很慢，因为需要下载大量 js css 文件，然后本地缓存。
    2.前后端分离的网站不利于搜索引擎收录，如商城类的网站，商品简介很少被收录到，导致销量惨淡。

应用场景：
    1.静态化首开页，提高小程序、手机端的网页的打开速度
    2.静态化内容页，便于搜索引擎收录

解决方案：
    将前后端分离的网站域名解析到 CDN 服务器上，CDN 根据 User-Agent 去判断是不是蜘蛛，
    如果是，则调用 CDN 上的客户端(可以对Selenium+ChromeDriver开源方案进行精简)去静态化页面，结果返回给蜘蛛；
    如果不是，返回 js、css 给用户的浏览器去动态渲染页面。
    注：可以单独部署一套升级版的 CDN 服务器，与现有的隔离，做成专为前后端分离网站提供服务的方案，这样不会影响原有服务器的性能和吞吐量。

    用 CDN 静态化页面的好处是通用性强，适合不同类型前后端分离的网站，可以做成平台【租给】其他人使用。
    减少服务器端的代码量(不用 Nuxt.js 了)、降低部署难度(不用在 Nginx 上进行蜘蛛判断，再路由请求)，提高服务器性能(不用服务器去渲染页面了)。

备注：
    CDN 必须可以接收参数，指定哪个页面需要静态化，哪个页面不需要静态化。
    希望 CDN 服务商能提供 SDK，便于将 Post 请求转发给源服务器，这样隐藏源服务器 IP，提高源服务器的安全性。
    另外 SDK 也能加入指定静态化局部页面的功能，而不是整个页面，这样网页调用更加模块化，方便程序员拼接页面、局部功能迭代。

安全隐患：
    CDN 可能受到黑客攻击，黑客伪造 User-Agent 为搜索引擎，然后让 CDN 静态化全站页面，浪费 CDN 的 CPU、内存资源。
    解决方案：可以引入黑、白名单，将需要静态化的 URL 写入白名单，这样避免被黑客消耗掉 CDN 资源。

**********************************************************************************************************

如果上面的方案有纰漏，无可行性，望留言告知我，让我也能集思广益。
