# 大胆预测下未来5年的Web开发

码农翻身 2020-04-01 08:50:00  4978  已收藏 8

前言：可以大致参考，后续如果有更合适的内容，我就更新。想了解这个未来五年的web开发是因为不想自己把技术栈学好，然后这个这个技术栈就被新的技术栈给取代了。



在2019年的ReactiveConf 上，《Elm in Action》的作者Richard Feldman对未来5年Web开发的发展做了预测，很有意思，分享给大家。

如果你有机会从头做一个项目，你会怎么选择技术栈？

这是演讲开始之前Richard提的问题， 相信很多人都会选择成熟稳定的、主流的技术栈。

如果时间回到2006年，这个主流的技术栈就是LAMP：





L : Linux

A: Apache

M: MySQL

P : Perl 或者 Python 或者PHP

Richard在2006年创业的时候，就选择了LAMP， 选择了Perl 。但是选择稳定的东西并不能保证安全，Perl很快就走了下坡路，慢慢地连Perl 程序员都不好招聘到了。



所以Richard 说：“不管我们选择的技术多么流行，多么主流，在今天多么吸引人，我们依然是在下注赌博。所以预测当前技术会向什么方向发展并且跟随，要比一开始就盲目接受别人所用的技术要更安全一些。”

有了这么一个前提， 他的预测开始了：

1. TypeScript将会接管JS世界

到2020年底，TypeScript将会成为新的商业项目最常见的选择。

到2025年底，每天使用TypeScript编程的程序员将超过使用普通JavaScript的程序员。 

TypeScript很多人都知道，它是JavaScript的一个超集，对JS增加了静态类型的检查， 这个关键的特性受到了很多程序员的欢迎，很多错误可以在编译时就被发现，而不是遗留到运行时，并且有了静态类型以后，阅读、修改、重构现有代码也变得更加轻松。

从Google 趋势来看，TypeScript正处于蓬勃发展的阶段，而CoffeScript则走向下坡路。





不仅如此，很多框架都已经支持TypeScript：





尽管如此，还有很多人不喜欢TypeScript，觉得TypeScript代码变得像Java一样冗长，设计也不健全，在某些情况下给人以错误的安全感。

Richard说预测未来的最重要因素就是看看这门技术如何影响团队， 很多团队都会说：“我们会尝试TypeScript， 我们已经使用TypeScript”， 从来没有团队说：“我们尝试了TypeScript，后来又回到了JavaScript。”

值得一提的是，现在微软养着两位大神，都在TypeScript和JavaScript领域耕耘，一个就是TypeScript的设计师Anders Hejlsberg， 他同时是Turbo Pascal , Delphi, C#等知名语言的设计者。另外一位是Erich Gamma ，他专注于编辑器和IDE，设计模式，Eclipse，VS Code就是他的得意之作。

2. WebAssembly 会扩大WebApp的领域

到2020年末，WASM对Web的组成不会有太大影响。

到2025年末， WASM将会创建一个新的领域：“重量级的Web App”。

WebAssembly 是什么东西？可以简单理解为在浏览器中执行的“汇编语言”， 可以提供接近本地代码的速度，肯定要比JavaScript快得多。

程序员肯定不会直接写“汇编语言”，程序员可以用C/C++/Rust来写程序，编译成WebAssembly后在浏览器中执行，当然，WebAssembly代码也可以被JavaScript调用。

可能会有人说，现在有了V8 之类的执行引擎，大家觉得JavaScript的性能已经不错了啊，为什么还要搞个Web汇编？

Richard举了一个例子：Figma，这是一个重量级的图像编辑软件，像Photoshop, Sketch 那样，但是它与众不同的是在浏览器中运行的。



这个软件是用C++开发的，最早的时候编译成了JS的一个子集ASM.js在浏览器中执行，采用了WebAssembly以后，速度提升了3倍之多。

另外一个更好的例子是游戏。比如下面这个场景，如果想使用CSS,估计是不行的， 但是WebAssembly可以搞定。



这就意味着WebAssembly打开了一扇门， 那些重量级的本地应用，可以通过Web的方式来安装，分发了。Web浏览器将会和传统的App Store, 安装程序做竞争了！





以后你想用某个应用，只需要浏览器中输入网址，立刻开始使用，不用安装。和别人分享也非常的方便，发个link就行了。 （是不是和小程序的理念有点像？但是本质是不同的。）

HTML/CSS/JS就此死去？当然不会，WebAssembly扩大的Web开发的基本盘， WebApp 的盘子会更大。

3. npm将在更多的问题中艰难生存

到2020年末， 至少一个npm的安全事件会登上新闻头条。

到2025年末， 至少一个恶意的npm package 感染大量开发者的机器。

这几年，开发人员已经目睹了好几次npm的灾难。

2016年， 一名 npm（Node.js Package Manager）的贡献者 Azer Koçulu 出于对 npm管理层的怨愤，删除了自己在 NPM 的250个模块，其中一个叫做left-pad，非常简单，就是用特定字符填到一个字符串的左边，达到指定的长度，但是这个模块被引用得非常广泛， 导致了一次NPM生态系统的大地震，Node.js， Babel ， 还有其他数千个项目直接罢工。

2018年npm又爆发了著名的event-stream事件， 一个叫right9ctrl的家伙，骗取了event-stream这个著名package的作者的信任，获取了代码所有权，然后向其中植入了恶意代码。

此外npm的packagte安装脚本中的也存在安全隐患，Richard建议在本机执行：npm config set ignore-scripts true 。





4. JS的替代品会稳健成长

到2020年末，编译成JavaScript的那些语言会继续增长，但是都没有TypeScript增长快速。

到2025年末， 那些非JS的方言还会稳健成长，虽然TypeScript会很流行。

JavaScript有两类替代品，一类是JavaScript方言，如TypeScript, Dart, Coffeescript等，还有一类是非JavaScript方言，例如ClojureScript, ReasonML, 和Elm， 虽然都是编译到JavaScript来执行，但是它们提供的体验和JavaScript不同。

Richard本人是Elm的开发人员，自然给Elm做了广告，渲染速度快，体量小，不崩溃，有自己的生态体系，并且因为有非常详细的错误信息而广受赞誉。

所以Richard认为，虽然以后TypeScript会更受欢迎，但是选择了这些小众的替代替代品的“粉丝”将会继续使用它们。
————————————————
版权声明：本文为CSDN博主「码农翻身」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/coderising/article/details/105259880