---
title: Goagent 关闭
date: 2015-09-24
---

#### Goagent 即将关闭时 Google group 上的一些讨论，留作纪念。
-----------------------------------------------------------


Reported by tonghua5...@gmail.com, Today (11 hours ago)

> 最早接触Google是在08年，刚刚大学毕业，随便申请个Gmail邮箱，后来工作后，发现上不了了。一个同事恰好是邮电学院毕业的，告诉我有个通信行业的最高学府：“北京邮电大学”，他忙于考研，需要查资料，所以对FCUK-GFW有一定的研究。顺便告诉我有个方校长。他有个工程叫GFW,给我讲完，我才知道事实的真相！
最初翻墙的一个方案：
1、利用：“世界通+Skype” 这是我的第一次翻墙方案，很不稳定，慢。 
   相关教程：https://sites.google.com/site/askofv/home/shi-jie-tong-skype
2、在google中搜索翻墙后，认识了:"freegate" 也就是自由门。还有无界，相对稳定一些，但涉及政治事件后，会被全面封杀。不过对于初级小白已经很方便了。当然，涉及政治色彩，新闻可以忽略。真假自己判断。相关地址：http://dongtaiwang.com/loc/phome.php?v=0
              http://www.wujieliulan.com/
3、在被GFW玩了这么惨以后，在也受不了了，后来认识基于GAE的 wallproxy和goagent,用着那个酸爽！地址：https://github.com/goagent/goagent/
         https://github.com/phuslu/goproxy（基于go）
         https://github.com/wallproxy/wallproxy(GUI不错，不过好像作者对天朝政策累了，目前项目处理停止状态)
   XX-NET:https://github.com/XX-net/XX-Net 一个整合Goagent和自动扫IP功能的好项目。目前作者说正在开发android版本。IOS版本暂时未听到相关消息。
所有翻墙工具里，我最喜欢的就是goagent&wallproxy。
4、GAE失效后，让我发现了有个基于socks4/5的代理，shadowsocks 中文名：“影梭” 
   比较好的教程在这里：http://shadowsocks.blogspot.sg/2015/01/shadowsocks.html
5、tor(高度隐藏IP代理) 特点相对稳定，就是速度慢。可以做为翻墙失败后的备选翻墙方案。
官方下载网址：https://www.torproject.org/download/download.html.en
还有一个不错的tor项目在这里：https://github.com/DarkSpyCyber/toranger
6、VPNgate:官方地址：http://www.vpngate.net/cn/ 据说被天朝在协议面给强奸了。不过大家可以用自由门或者无界做它的前置代理，还是可以连接到很多优秀服务器的。
7、google资助的lantern项目。中文名称：“灯笼” （哥现在用这个呢。对了，用它做VPNgate的前置代理效果也不错）官方地址：https://www.getlantern.org/
                github:https://github.com/getlantern/lantern/releases
8、赛风 https://psiphon.ca/ （自动配置代理）速度一般，不过有一些优化措施，没时间，没有弄。
9、I2P 官方地址：https://geti2p.net/en/
我的翻墙方案差不多就这些
如果大家感兴趣可以看看这个博客：
http://program-think.blogspot.com/2009/05/how-to-break-through-gfw.html
还有一个介绍翻墙的地址：http://allinfa.com/
我知道的就这些，如果哪位大神有更好的方案，请多多指教分享。
再次真心感谢所有开发者。向phus.lu致敬！


Today (9 hours ago) #1 chum...@gmail.com
> 差不多全了！


Today (8 hours ago) #2 hongwang...@gmail.com
>补充一下：
2，自由门，无界的地址是：http://forums.internetfreedom.org/
关于tor,以蓝灯，赛风作前置的效果还是很不错的！


Today (8 hours ago) #3 warmingf...@gmail.com
> 放在这里已不是长久之计，建议楼主及各位网友将经验写进 https://github.com/XX-net/XX-Net/wiki 。


Today (7 hours ago) #4 warmingf...@gmail.com
> 在 GitHub 上分享翻墙经验的途径：

1. 建立仓库，如 https://github.com/phuslu/goproxy/tree/wiki

	优点： 
	1. 可多人协作
	2. 不会被恶意编辑或删除

	争议点：
	1. 提交的内容需被仓库所有者审核才能通过

2. 在 GitHub Wiki 上编辑，如 https://github.com/XX-net/XX-Net/wiki

	优点：
	1. 可多人协作

	缺点：
	1. 条目易被恶意删除 （但可用历史记录补救，不知是否有防止 WiKi 被恶意删除的措施）
	2. 内容易被恶意修改

	争议点：
	1. 内容提交即发表，不需审核

3. 在 GitHub Issues 上发表，如 https://github.com/phuslu/goproxy/issues

	优点：
	1. 不会被恶意编辑或删除

	缺点：
	1. 不能多人协作

	争议点：
	1. 内容提交即发表，不需审核（但仓库所有者有权限对 Issue 作出处理，例如 https://github.com/phuslu/goproxy/issues/63 ）


Today (2 hours ago) #5 zh919580...@gmail.com
> 怎么把蓝灯用作前置代理

--------------------

Reported by hongwang...@gmail.com, Yesterday (31 hours ago)

> 2015年8月25日，这块阵地就要转移了。但历史会记住GoAgent走过的路。大家收藏一下网页的截图吧，留个纪念，也留下历史的见证。将来，在中国的自由民主纪念馆，在翻墙展区，这颗璀璨的明星一定会与大家再相逢。这儿曾经有过80后，90后...还有40后，不知道是否有过00后。
在翻墙展区，人们或许会听到音乐家谱写的G大调《翻墙交响曲》，她将伴随着GoAgent直到永远....



Yesterday (31 hours ago) #1 hongwang...@gmail.com
> 自己顶一下！


Yesterday (31 hours ago) #2 jiangxin...@gmail.com
> 80后至此一游。我曾来过


Yesterday (31 hours ago) #3 fid...@gmail.com
> 说的好，支持。
过两年墙就没了，最多最多5-10年。


Yesterday (30 hours ago) #4 wcg...@gmail.com
> 这里要关了? 以后去哪里?


Yesterday (30 hours ago) #5 tgy.ch...@gmail.com
> 我这不好使呢，你别关啊


Yesterday (30 hours ago) #6 fswl1...@gmail.com
> 去哪里都可能再次面对“这里要关了? 以后去哪里?”
终极解决方案只有。。。锻炼身体！XD

> Fired up. (Fired up)
Fired up. (Fired up)
Twenty-Seven (Twenty-Seven)
Fired up. (Fired up)
Here we go. (Here we go)
On the road. (On the road)
Twenty-Seven. (Twenty-Seven)
Fired up. (Fired up)
https://www.youtube.com/watch?v=NssStw9z3WE


Yesterday (29 hours ago) #7 jasonli...@gmail.com

> 哪来这许多娘娘腔的伤感?

> 若日後大家再見面
必回贈一雙虎眼
明知要去此際不平凡
行者笑帶傲慢
頭上朗月明燈一盞
何懼無路往返
https://www.youtube.com/watch?v=ZJwUWCwN8Ts


Yesterday (29 hours ago) #8 blues.ji...@gmail.com
> 用goagent5～6年了吧。。时间好快，在没有goagent的年代，只能用无界自由门，打开个网页都吃力。


Yesterday (26 hours ago) #9 agrochem...@gmail.com
> jasonli...@gmail.com

> 再向虎山行，当年大陆第一次放这个片子，本人还在上初中，现在想起来晃若隔世啊


Yesterday (26 hours ago) #10 TMH8...@gmail.com
> 70后的路过


Yesterday (26 hours ago) #11 fswl1...@gmail.com
> 甜甜的姐姐稍稍留步
姐姐呀你赶路啊
哎哟哎哟请息怒 我爱你齿儿露

> XD XD XD


Yesterday (26 hours ago) #12 meilizix...@gmail.com
> 封鎖厲害，有生在會


Yesterday (25 hours ago) #13 ghl3318...@gmail.com
> GFW用全国的资源和小小的GoAgent进行极度不对称战争，GoAgent向人民演绎了什么叫真正的虽败犹荣！感谢GoAgent陪伴我的3年时间，GoAgent必将柏林墙一样成为一个时代的象征！GoAgent的精神不死！不说再见！


Yesterday (25 hours ago) #14 lxok1...@gmail.com
> 70后的我们才是中国互联网GFW从无到今的见证者。


Yesterday (24 hours ago) #15 syhtfb...@gmail.com
> 留个脚印，伟大的GoAgent的见证者，不单单是网络工具，是意味着一个民族思想自由的权利。


Yesterday (24 hours ago) #16 tankbust...@gmail.com
> Goagent不仅仅只是一个简单的软件，它代表了整个中华民族追求自由的时代。


Yesterday (20 hours ago) #17 paulchan...@gmail.com
> 留个脚印。。。


Today (12 hours ago) #18 hongwang...@gmail.com
> lxok1...@gmail.com:不错，70后是互联网的见证者。问题是谁将是推倒GFW的主力军。


Today (8 hours ago) #19 781...@gmail.com
> 70后是互联网的见证者


Today (4 hours ago) #20 mike0wang0
> 00后至此一游。用了GoAgent近4年了。


Today (36 minutes ago) #21 pcman1...@gmail.com
> 80后到此一游，用goagent三年


Today (8 minutes ago) #22 chinasun...@gmail.com
> 90后到此一游 用gae已经4年！！