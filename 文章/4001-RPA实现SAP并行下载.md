上篇文章谈了谈企业应该如何定位RPA技术以及建立卓越中心的一些思考。

本文是个技术文章，谈谈如何用RPA实现SAP GUI中数据导出的并发执行，以缩短RPA的运行时间。

# 一. 源起

最近参与了一个RPA的POC，和来自四大的同行（共五家入围POC）一起，针对同一个场景进行可行性实现。

由于总体流程比较清晰，需求就比较简单，而我们RPA团队做项目总是需要追求极致，要有亮点的。

亮点之一便是采用从SAP系统导出原始数据时，采用了并发执行的方式，以提升数据导出的效率，缩短RPA完成整个流程的时间。

# 二. 实现总体思路
## 2.1. 关于SAP系统数据
粗暴的来分，SAP ERP数据在系统中有两种存放方式：实际生成的数据（例如会计分录BSEG表）和需要动态计算的数据（例如科目余额表FS10N）。前者可以通过SE16直接找到透明表导出来，后者则需要有ABAP代码动态计算生成。

数据导出的所需时长取决于：原始数据量、计算复杂度、服务器性能。

## 2.2. 数据导出的步骤
步骤1：打开新窗口、输入事务码、输入筛选条件

步骤2：执行数据查询

步骤3：导出结果为Excel

## 2.3. 并行原理
在只有一个机器人的情况下，所谓的并行，其实就是多线程。

总体来讲还是串行执行，只是在不同的线程任务之间进行切换。

纯本地化的操作，并行是没有意义的；并行的意义在于让等待远端服务器计算的操作能够同时执行，以节省等待时间。

## 2.4. 理想和现实
理想的预期是这样的：
![](https://github.com/rrenzixu/RPA/raw/master/%E5%9B%BE%E7%89%87%E5%BA%93/4001-02.jpg)

现实能够实现是这样的：
![](https://github.com/rrenzixu/RPA/raw/master/%E5%9B%BE%E7%89%87%E5%BA%93/4001-03.jpg)

“理想”和“现实”的差异就在于本来能够节省的两次“导出结果”操作的时间没有能够被有效节省。

对于可能的原因分析：

软件产品的问题：这是一个bug，或者待优化点；

实施人员的问题：对于软件的理解有待加深。

比较倾向于是由于软件产品的问题。

**如果您有实现“理想”的方案，跪求思路和方法！**

# 三. 操作细节
非技术人员不会看到这里，为节省时间，后面的内容就只提问题，答案先空着。

想了解细节的，请私信或留言。

**a. 需要打开SAP GUI支持RPA的开关**

**b. 需要有效定位和区分SAP GUI的不同窗口，并行才能可行**

**c. RAP软件并行机制要合理设计**



这篇文章就先聊到这儿，下周见！

（正文结束） 

----------


## 附1. 案例资讯

 “案例资讯”的板块已上线一段时间了。

出发点：以RPA咨询和实施的视角，点评研究和记录RPA案例。

玩法：不主动推送，不定期更新；需要自行点击查看。

我们还在不断探索更好玩儿的，更灵活的交互方式，继续卖个关子，敬请期待。


## 附2. 原创RPA文章列表

[1001-什么是RPA？(上)](http://mp.weixin.qq.com/s?__biz=MzU3MDM0Mjg3OA==&mid=2247483663&idx=1&sn=6bc97a8abefc71aab1ef4da65823536e&chksm=fcf1adbecb8624a834b7411eeb7d346fa3349f23b6c63902ed8c499325646a15a3c2131d9b78&scene=21#wechat_redirect)

[1002-什么是RPA？(下)](http://mp.weixin.qq.com/s?__biz=MzU3MDM0Mjg3OA==&mid=2247483662&idx=1&sn=9f1984baf97192e5c55fc4dc5de0bc6b&chksm=fcf1adbfcb8624a97b0b509084f1619e9436371decae416061f7a526d6c6a02626bbafe3f1bf&scene=21#wechat_redirect)

[1003-RPA的优势](http://mp.weixin.qq.com/s?__biz=MzU3MDM0Mjg3OA==&mid=2247483676&idx=1&sn=623dc5aa79c63c7b9631ded303bd847a&chksm=fcf1adadcb8624bb3910c2c1b6f39d22003c0109d76171cd8acc97d1684726156496f1c5159a&scene=21#wechat_redirect)

[1004-RPA的软件选择](http://mp.weixin.qq.com/s?__biz=MzU3MDM0Mjg3OA==&mid=2247483681&idx=1&sn=f3f19e8aded6a336ffd48bd1c241d9d0&chksm=fcf1ad90cb8624861c830088331f4c51e270009ffd5ff6122d7413fb7a7ab2de3537cf636555#rd)

[1005-RPA的技术架构](http://mp.weixin.qq.com/s?__biz=MzU3MDM0Mjg3OA==&mid=2247483689&idx=1&sn=8781193cd9ee5b1a4280ef56a68c18d6&chksm=fcf1ad98cb86248e5422d2a47c26a7d01ab63e1c308b4af04b0b78f2fce0e3ce457ba1aaa773&scene=21#wechat_redirect)

[1006-RPA的实施方法](http://mp.weixin.qq.com/s?__biz=MzU3MDM0Mjg3OA==&mid=2247483695&idx=1&sn=3e5cded5e8627b7d8a3819e90b6c8833&chksm=fcf1ad9ecb862488bb48e9f2a631b8f51f0b5cb9ab33bd023a34901b11ff0c2387995f2cd1b0&scene=21#wechat_redirect)

[1007-RPA的演进路线](http://mp.weixin.qq.com/s?__biz=MzU3MDM0Mjg3OA==&mid=2247483702&idx=1&sn=2f48ee26eddd6141695c627e964da641&chksm=fcf1ad87cb862491af612cd7a9e02f3dfcba4e38a28cde5c2b2f51c1f738e38051ae41617464&scene=21#wechat_redirect)

[1008-RPA与卓越中心](http://mp.weixin.qq.com/s?__biz=MzU3MDM0Mjg3OA==&mid=2247483739&idx=1&sn=67887bfc070de727bc3bf1dc076011f1&chksm=fcf1adeacb8624fc08ff24ca7efe866985f4008a7f6454e5b28eb5ce2e64eb83c28d3348f9b8&scene=21#wechat_redirect)

[2001-RPA与爬虫](http://mp.weixin.qq.com/s?__biz=MzU3MDM0Mjg3OA==&mid=2247483715&idx=1&sn=cbb8b2a86464ea473cc35b6a453f05d1&chksm=fcf1adf2cb8624e42f0b65b9e78b3722b964d8ac18e9d4933be1a2fb193e1868aaacfef8670c&scene=21#wechat_redirect)

[2002-RAP与网页（增值税发票验真场景）](http://mp.weixin.qq.com/s?__biz=MzU3MDM0Mjg3OA==&mid=2247483726&idx=1&sn=ea0bed6ee4707dcc357a12fd926c5905&chksm=fcf1adffcb8624e99e9b21c2ce3f7f4c4e9538523755881c987410681ee90a42223cd99a0a6b&scene=21#wechat_redirect)

[3001-RPA与财务共享中心](http://mp.weixin.qq.com/s?__biz=MzU3MDM0Mjg3OA==&mid=2247483731&idx=1&sn=e0bf1973c30f6824c47818050557fce9&chksm=fcf1ade2cb8624f4c2766895a3c3b96c3cf54c08f7ef64e80ff9a01e523bf1d69f325c6a3c7a&scene=21#wechat_redirect)

[3101-RPA与全面预算管理](http://mp.weixin.qq.com/s?__biz=MzU3MDM0Mjg3OA==&mid=2247483735&idx=1&sn=e47a0b06d60e374a64c56f8b76bf201d&chksm=fcf1ade6cb8624f0b72a37b09db6bc1e3fb49ebdb29411b5e15fe3b07a967f2d82989c4c150f&scene=21#wechat_redirect)
 
## 附3. 关于微信公众号
**微信公众号ID：RPA2018**

微信公众号名称：RPA流程自动化机器人

感谢您的关注和阅读，希望这篇文章能为您带来帮助。

欢迎转载与分享，也请注明出处。

如果您有需要了解的关于RPA的其他内容，也可以给我留言或发邮件
（rrenzixu@126.com）。

识别以下二维码，可以关注本公众号。

![](https://github.com/rrenzixu/RPA/raw/master/%E5%9B%BE%E7%89%87%E5%BA%93/9002-%E5%85%AC%E4%BC%97%E5%8F%B7%E4%BA%8C%E7%BB%B4%E7%A0%81.jpg)


## 附4. 关于本文作者
本文作者：任子旭 Zack Ren
微信号：rrenzixu

识别以下二维码，可以与作者进行更为深入的交流。

![](https://github.com/rrenzixu/RPA/raw/master/%E5%9B%BE%E7%89%87%E5%BA%93/9001-%E5%BE%AE%E4%BF%A1%E4%BA%8C%E7%BB%B4%E7%A0%81.jpg)
