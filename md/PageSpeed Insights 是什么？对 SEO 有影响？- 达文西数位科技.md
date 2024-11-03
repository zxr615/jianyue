> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.da-vinci.com.tw](https://www.da-vinci.com.tw/cn/blog/pagespeed-insights-psi)

> PageSpeed Insights (PSI) 是测试网站架构工具，PSI 分数达到 80 分以上才适合 SEO 关键字排名，网站架构当然还有其他因素，但 PSI 是最基本的。

很多 SEO 公司说 PageSpeed Insights (PSI) 跟 SEO 无关，其实错了，Google 早已经明确表达「网站使用者体验」与「网站效能」跟 SEO 有关，而 PSI 就是在帮助网站检测「网站使用者体验」、「网站效能」的重要工具，网站架构影响了 SEO 成效，如果能在 PSI 拿到高分，就等于在 SEO 有了更好的起跑点，这也是为什么 SEO 必须跟网页设计做深度整合的原因。  
〈**延伸阅读：**[网页设计公司不会告诉你的 5 个真相](https://www.da-vinci.com.tw/tw/blog/webdesign-5fact)〉

  
什么是 PageSpeed Insights (PSI)？
--------------------------------

PageSpeed Insights (PSI) 是由 Google 提供的网站测试工具，主要是测试「网站使用者体验」与「网站效能」这两项，Google 定义了许多标准，让网站开发者或是网路行销可以依照这些指标去改善网站，让网站可以更符合使用者体验 (UX)，可以更快更好用。

〈**延伸阅读：**[网页设计的使用者体验 (UX) 如何执行？](https://www.da-vinci.com.tw/tw/blog/ux-webdesign) 〉

  
PageSpeed Insights 怎么测试？
---------------------------

首先到 [PageSpeed Insights](https://pagespeed.web.dev/?hl=zh-TW)  测试网站，输入想测试的网址，按下【分析】按钮，等待结果出来，结果会分成行动装置、电脑结果，通常我们会以行动装置报告为主，因为 Google 自然排名是以手机版网站作为排名依据。  
〈**延伸阅读：**[SEO 怎么做？ 2024 重点教学](https://www.da-vinci.com.tw/tw/blog/seo-study)〉

#####   
用 PSI 测试网站效能与使用者体验

##### ![](https://www.da-vinci.com.tw/uploads/editor/files/psi-TEST-step.png)

#####   
第一区测试结果是「使用者体验」

![](https://www.da-vinci.com.tw/uploads/editor/files/Core-Web-Vitals-3-points-ok.png)

##### 

往下的第二区测试报告是「网站效能」  
![](https://www.da-vinci.com.tw/uploads/editor/files/psi-6-type-test-ok.png)

PageSpeed Insights 测试指标有哪些？


-------------------------------

PSI 测试分成「使用者体验」与「网站效能」这两项，使用者体验包含 3 项核心指标 (LCP、FID、CLS) ＋ 3 项其他指标 (FCP、INP、TTFB)，网站效能则有 6 项指标 (FCP、SI、LCP、TTI 、TBT、CLS)，其中的 LCP、CLS、FCP 在两项测试指标是重复的。  
〈**延伸阅读:** [具备 SEO 架构的网站，SEO 成功率才会高](https://www.da-vinci.com.tw/tw/seo-sef)〉

<table><thead><tr><th>项目</th><th>使用者体验</th><th>网站效能</th></tr></thead><tbody><tr><td>LCP (最大内容绘制)</td><td>V (核心指标)</td><td>V</td></tr><tr><td>FID (首次输入延迟)</td><td>V (核心指标)</td><td>&nbsp;</td></tr><tr><td>CLS (累计版面配置转移)</td><td>V (核心指标)</td><td>V</td></tr><tr><td>FCP (首次内容绘制)</td><td>V</td><td>V</td></tr><tr><td>INP (下个画面的互动)</td><td>V</td><td>&nbsp;</td></tr><tr><td>TTFB (跑出第一字节时间)</td><td>V</td><td>&nbsp;</td></tr><tr><td>SI (速度指数)</td><td>&nbsp;</td><td>V</td></tr><tr><td>TTI (可互动时间)</td><td>&nbsp;</td><td>V</td></tr><tr><td>TBT (封锁时间总计)</td><td>&nbsp;</td><td>V</td></tr></tbody></table>

什么是网站体验核心指标？
------------

Google 在 2020 年推出网站体验核心指标 (Core Web Vitals)，用来测量网站的使用者体验是不是良好，以 LCP (最大内容绘制)、FID (首次输入延迟)、CLS (累计版面配置转移) 这三项作为核心指标，测试结果绿色是优良，黄色是待改善，红色是不及格，可以从 PageSpeed Insights 测试中得到数据，如果想更进一步知道哪些页面的 Core Web Vitals (网站体验核心指标) 需要改善，可以到 Google Search Console 的网站体验核心指标找到资讯。

##### 

Core Web Vitals 的三个测试指标

![](https://www.da-vinci.com.tw/uploads/editor/files/Core-Web-Vitals-3.png)

##### 

GSC 的网站使用体验核心指标

![](https://www.da-vinci.com.tw/uploads/editor/files/Core-Web-Vitals-reports.png)  
 

PageSpeed Insights 的 9 种优化指标
----------------------------

使用者体验、网站效能加起来总共有 9 种指标，包含 LCP (最大内容绘制) 、FID (首次输入延迟) 、CLS (累计版面配置转移) 、 FCP (首次内容绘制) 、INP (下个画面的互动) 、TTFB (跑出第一字节时间) 、SI (速度指数) 、TTI (可互动时间)、TBT (封锁时间总计)，让我们看一下各代表什么意思，以及该如何优化，因为涉及太多技术，我们尽量深入浅出让大家理解。  
〈**延伸阅读：**[前端工程师 - 网站架构的重要推手](https://www.da-vinci.com.tw/tw/blog/front-end-webdesign)〉

LCP (最大内容绘制) 如何优化？
------------------

LCP (Largest Contentful Paint) 最大内容绘制，把网页想像是一块画布，渲染就是作画，LCP 就是画布上最大那一块的绘制时间，LCP 在测试网站最大内容载入的时间，最大内容可能是图片或影片，也可能是文字，LCP 时间越快越好，一般网站为例，LCP 通常是形象大图，或者是影片，这些内容优化就变得非常重要，也是影响 LCP 的最大因素。

#####   
LCP 是网页中最大内容 (此例是大图)

![](https://www.da-vinci.com.tw/uploads/editor/files/lcp-web-concent.png)

#####   
LCP 测试标准最佳是低于 2.5 sec

![](https://www.da-vinci.com.tw/uploads/editor/files/PSI-LCP-TEST.png)

###   
使用 PRPL 模式做到即时加载

*   Preload：预先加载重要档案。 (例如：预先加载 CSS)。
*   Render：加速渲染初始路线。 (例如：使用 SSR 伺服器端渲染)
*   Pre-cache：预缓存原本有的档案。 (例如：使用 API 预缓存)
*   Lazy load：延迟加载其他路线和非关键的档案。   (例如：延迟载入图片)

###   
优化关键渲染路径

精简 DOM 的架构，优化 HTML 程式码，与各种路径流程，包含 CSS、JavaScrip...

###   
优化您的 CSS

精简 CSS 提升载入速度，没有用到的 CSS 一定要移除，可减少行数并整合语法。

###   
优化网站图片

压缩图片提升载入速度，图片压缩到肉眼无法分辨的至质感即可，不要使用原图直接上架。  
**〈延伸阅读：[img alt 是什么？对于 SEO 来说很重要吗？](https://www.da-vinci.com.tw/cn/blog/img_alt) 〉**

###   
优化网页字体

使用网页加载速度快的字体，可以的话，尽量用浏览器预设的字体。  
 

### 优化您的 JavaScrip

优化 Client 端的 JavaScrip，避免使用载入慢的 JavaScrip，尤其是复杂的动画或效果。

FID (首次输入延迟) 如何优化？


----------------------

FID (First Input Delay) 首次输入延迟，就是网页被使用者第一次点击 (Click) 所需要等待的时间，无论是点击连结、按钮、下拉选单，等待时间低于 100 毫秒就算是好的 FID，会用首次输入作为指标的是因为首次使用者体验是最重要的感受。

#####   
FID 测试标准需低于 100ms

![](https://www.da-vinci.com.tw/uploads/editor/files/fid_psi_tset.png)

###   
减少第三方代码的影响

把没有用的第三方代码移除，或是减少使用不必要的代码

###   
减少 JavaScript 执行时间

避免使用又大又慢的 JavaScript，没用到的 JavaScript 要移除，压缩程式码，拆解 JavaScript 程式码分开执行。

###   
最小化主线程工作

检视网站内容显示的主要流程，将每一个步骤最小化。

###   
保持较低的请求数和较小的传输大小

减少请求的数量，包含 html、CSS、JavaScript、图片、字体、媒体、动画 (GIF)

CLS (累计版面配置转移) 如何优化？
--------------------

CLS (Cumulative Layout Shift) 累计版面配置转移是在测试网站的「视觉稳定性」，你有没有过一种经验，要点一个按钮或是连结的时候，画面忽然跳掉或是画面错位，甚至跳出广告，造成你无法点击的状况，记录版面配置转移这就是 CLS 指标存在的目的。

#####   
CLS 测试标准需低于 0.1 分以下

![](https://www.da-vinci.com.tw/uploads/editor/files/cls-psi-test.png)

###   
固定图片或影片尺寸

如果网页有图片或是尺寸建议就是设定尺寸，或是使用 CSS 容器去预留需要的网页配置，避免内容重叠或是跑版，可以用 unsized-media 强制执行此行为 (有支援的浏览器才可以)。

###   
避免使用跳出视窗功能

除非是使用者点击按钮或连结，否则就不要制作自动跳出视窗的任何内容，以免发生内容布局的偏移，造成不佳的使用者体验。

###   
选择简单的动画

尽量采用单纯的换图动画，而不是会跳来跳去的动画，避免产生布局偏移，动画是为了示意与转场，帮助内容的顺畅连续性，而不是花俏动画。

FCP (首次内容绘制）怎么优化？
-----------------

FCP (First Contentful Paint) 是跑出网站第一个内容的时间，FCP 的内容可以是文本、图片、元素，把第一个出现的内容时间作为指标，也代表整个网站流程优化的展现。

#####   
FCP 首次出现内容的样子

![](https://www.da-vinci.com.tw/uploads/editor/files/fcp-web-concent.png)

#####   
FCP、FID、TTI 指标之间差异

![](https://www.da-vinci.com.tw/uploads/editor/files/FCP-TTI-FID-toger.png)

#####   
FCP 首次内容绘制时间需低于 1.8 sec

![](https://www.da-vinci.com.tw/uploads/editor/files/psi_fcp_test.png)

###   
消除阻塞渲染的资源

找出阻碍网页显示内容的原因，并将它排除，包含 html、CSS、JavaScript、第三方程式…。

###   
优化 CSS

减少 CSS 程式码，把没有用到的 CSS 移除

###   
预连接到所需的来源

如果有需要预先连结的第三方网站，可以先预先设定连接。

###   
减少服务器响应时间 (TTFB)

TTFB 是资源请求到回应的时间指标，减少 TTFB 时间就能加速 FCP 的时间。

###   
避免多个页面重定向

从一个 http 跳到另一个 http 是很耗时间的，所以尽量不要使用页面重定向，尤其是多个页面重定向 (301/302)

###   
预加载关键请求

把关键重要的 CSS、JavaScript 预先加载进来，可以加快载入的时间。

###   
避免巨大的网路负载

避免使用需要从外面载入网站的资源，以免连外面网站的时候花费太多时间。

###   
高效缓存静态资料

利用 Cache-Control 暂存字型、图像、媒体… 静态资源，加快载入的速度。

###   
避免 DOM 过大

写 DOM 架构的时候，必须精简程式，需要时才创建 DOM 节点，不需要时应把节点移除，不要让 DOM 结构过大。

**DOM 是什么？**  
DOM 全名是 Document Object Model 中文称作「文件物件模型」，DOM 就是把 HTML 的各个标签，包括文字、图片…，定义成物件，物件会形成一个树状结构，也就是网页原始码结构。

###   
最小化关键请求深度

最小程度的使用关键资源连结数量，或者延迟下载，改变加载顺序，缩短下载路径长度

###   
确保文字在网页加载时可以看到

字体需要时间才能载入完成，还没载完之前会看不到文字，要先用浏览器预设字体先暂时显示载完再换字体，以免 FCP 时间拉长。

INP (下个画面的互动) 怎么优化？


-----------------------

INP (Time to First Byte) 下个互动画面的时间指标，INP 是在测量网页操作流程的所有点击的反应能力，当使用者点击后产生反应的时间，越不顺畅的就会花上更多时间，主要是再测试滑鼠、触控银幕、键盘的点击后的反应时间，跟 FID 有一点相似，但 FID 只测量第一次，INP 却是测量全部的点击反应，是更全面的指标。

#####   
INP 测试标准要低于 200ms

### ![](https://www.da-vinci.com.tw/uploads/editor/files/inp-test-psi.png)

减少不需要的程式码

把多余的 CSS、JavaScript 移除，没有用的一定要移除，减少加载的负载

###   
把程式码拆开执行

在网页加载期间延迟加载比较不重要的 JavaScript

###   
避免 DOM 过大

精简 DOM 架构，减少 DOM 节点，把不需要的节点移除，不要让 DOM 过大。

###   
移除没有用到的第三方程式码

检查是不是有没用到的第三方程式，如果有就移除，或者用更精简的方式使用。

TTFB (跑出第一字节时间) 怎么优化？
---------------------

TTFB (Time to First Byte) 是测量从网站请求到回应完成的时间指标，主要在测试从主机、系统、程式之间的效能速度，从这个指标就能知道网站主机效能、频宽速度。

#####   
TTFB 测试标准需低于 800 ms

### ![](https://www.da-vinci.com.tw/uploads/editor/files/ttfb_PSI_test.png)

选择好的网站主机

网站代管商的主机效能会影响 TTFB 数据，所以有足够效能与频宽是非常重要的。

###   
采用专业的程式

好的网站设计公司可以写出效能好的程式，连接外速稳定的资料库。

###   
使用 CDN 服务

如果希望全世界的节点都有一定的反应速度，可以采用 CDN 服务，可以让速度加快，以提升 TTFB 效率。

###   
避免多次重定向

网站重定向很浪费时间，一定要避免多次的网址重定向，将 CLS 预先提交给 HSTS 预载列表，减少 HTTP 重定向到 HTTPS 的时间。

###   
预先连结网站外的资源

如果有需要外连的资源，可以提前预先连结，减少加载时间

###   
使用 HTTP/2 或 HTTP/3

使用新一代的网页伺服器，可以提升反应时间。

###   
预先加载需要的资源

把关键重要的 CSS、JavaScript 预先加载进来，可以加快载入的时间。

SI (速度指数) 怎么优化？
---------------

SI (Speed Index) 指数是测量「内容的视觉显示速度」，就是从没有到看到完整视觉页面的时间，是跟身体感觉的速度是很接近的数值，速度要低于 3.4 秒才算快。

#####   
SI 标准需低于 3.4 秒

<table><thead><tr><th>速度指数 (秒)</th><th>颜色意思</th></tr></thead><tbody><tr><td>0 – 3.4</td><td>绿色 (快速)</td></tr><tr><td>3.4 – 5.8</td><td>橙色 (中等)</td></tr><tr><td>超过 5.8</td><td>红色 (慢)&nbsp;</td></tr></tbody></table>

### 最小化主线程工作

这个主线程优化工作范围是很大，包含 html、CSS、JavaScript、图片、动画，整个流程都是。

###   
减少 JavaScript 执行时间

JavaScript 是一个很吃时间的程式，载入过多复杂的 JavaScript (动画效果)，都会严重影响 SI 数值。

###   
确保字体保持显示状态

字型载入是需要时间的，尤其是非浏览器预设的字型，都是需要时间载入的，如果无法使用预设字体，至少要先让网页显示，避免画面缺字，也会影响 SI 的时间。

TTI (可互动时间) 怎么优化？
-----------------

TTI (Time to Interactive) 可互动时间是指「网页进入可互动状态」所花费的时间，简单来说就是网站要载入完成才能开始互动，HTML、CSS、JavaScript、图片… 必须都已经载入完成，互动的点击或功能才能真正使用，而 TTI 就是载完可互动时所花的时间。

#####   
TTI 标准需低于 3.8 秒

<table><thead><tr><th>速度指数 (秒)</th><th>颜色意思</th></tr></thead><tbody><tr><td>0 – 3.8</td><td>绿色 (快速)</td></tr><tr><td>3.9 – 7.3</td><td>橙色 (中等)</td></tr><tr><td>超过 7.3</td><td>红色 (慢)&nbsp;</td></tr></tbody></table>

### 减少不必要的 JavaScript

删除不需要 JavaScript，或是延后载入不重要的 JavaScript，都可以提升 TTI 的效能。

###   
以 PRP 模式减少负载

*   Preload：预先加载重要档案 (例如：预先加载 CSS)。
*   Render：加速渲染初始路线。 (例如：使用 SSR 伺服器端渲染)
*   Pre-cache：预缓存原本有的档案。 (例如：使用 API 预缓存)
*   Lazy load：延迟加载其他路线和非关键的档案 (例如：延迟载入图片)

###   
优化第三方 JavaScript

很多第三方 JavaScript 都会拖垮网站速度，可以试着整理一下第三方 JavaScript，不需要的 JavaScript 移除，或者与先载入需要的 JavaScript。

TBT (封锁时间总计) 怎么优化？
------------------

TBT (Total Blocking Time) 是测量用户输入后的延迟累计的时间，包含滑鼠点击、银幕点击、按下键盘的等待时间，主要是把 FCP(首次内容绘制)、TTI(可互动时间) 的时间加总。

##### TBT 标准需低于 200 毫秒

<table><thead><tr><th>速度指数 (毫秒)</th><th>颜色意思</th></tr></thead><tbody><tr><td>0 – 200</td><td>绿色 (快速)</td></tr><tr><td>200 – 600</td><td>橙色 (中等)</td></tr><tr><td>超过 600</td><td>红色 (慢)&nbsp;</td></tr></tbody></table>

### 优化网站程式

程式码包含 HTML、CSS、JavaScript、图片压缩、第三方程式码…，只要会延迟时间的因素都要排除。

###   
提升主机与系统效能

主机效能与反应时间，资料库的回应效率，都会影响 TBT 数值，所以要把主机、系统都提升到一定程度的规格跟效能。

####   
结论

PageSpeed Insights(PSI) 不只对「网站速度做测试」，还包含了前端程式、主机效能、使用者体验、网站内容…，进行全面性的测试，把 PSI 分数优化到高分，就代表「网站符合 Google 定义的优良网站条件」，要做 Google 的 SEO 当然要按照 Google 的网站标准来优化，PSI 的分数低不代表网站速度慢，也不代表 SEO 完全没有希望，但如果网站跟产业是高竞争，那 PSI 检测与调教肯定是不能马虎了，必须找真正可以制作 PSI 高分的网页设计公司。  
〈**延伸阅读：**[SEO 是什么? 简单说让你听得懂](https://www.da-vinci.com.tw/tw/blog/seo-what)〉  
〈**延伸阅读：**[网页设计公司不会告诉你的 5 个真相](https://www.da-vinci.com.tw/tw/blog/webdesign-5fact)〉

**(****本文为达文西数位科技所有，转载文图请注明出处****)**