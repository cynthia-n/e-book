#简介

>在翻译简介之前，我突然想说点什么。在书里我看到了这样一句话“Will write code that writes code that writes code for food”(Martin Rodgers)。突然觉得它一语道破了元编程的精髓。如果说我们写的代码是在```编写食物代码的代码```，那么元编程将是带领我们编写```编写食物代码的代码```的代码。

元编程...听起来多酷！这听起来像是一个高层次企业设计师的设计技巧或者是一个已经进入新闻发布的时尚流行语。  
  
事实上，它并不是一个抽象的改变，也不是一个营销说(例如神秘的互联网思维)。元编程是一个脚踏实地，务实的编码技术方法。它不是听起来很酷，它是真的很苦。这里有一些你可以用ruby元编程来做的事：  

* 如果说你想写一个链接外部系统的ruby程序 —— 可能是一个web服务或者是一个java程序。使用元编程，你可以把这些打包，封装成一个包，任何方法都可以调用，并将其路由（链接）到外部系统。如果有人稍后向外部系统添加了一些方法，你则不需要去更改你的“ruby封装包”。它会立刻支持这些新的方法。是不是很神奇？！
* 也许你有一个问题，你想用一种专门针对这个问题的编程语言来解决这个问题.你一定会遇到一些麻烦，因为你在用你自己的语言，你可能需要自定义新的语言的解析器等等一系列问题。或者你可以继续用ruby这个语言，但是改变它的语法知道它看起来像那个专门针对这个问题的编程语言。你甚至可以编写你自己的小翻译程序，从文件中读取基于ruby语言编写的代码。
* 你可以干脆俐落的删除重复的代码从你的ruby代码中，同时保持代码的干净和优雅。想想在一个类中有20个方法都看起来长得差不多。那么你为什么不只定义一次这个方法，这样只会需要几行代码而已？或者你可能想要按顺序调用一些列有规律命名的方法。那为什么不只写短短几行代码，让它调用所有名字符合的方法？换句话说，就像所有的方法都是从检测名字开始的？
* 你可以拉伸和扭曲ruby来满足你的需求，而不应该是你去适应ruby这个语言。举个例子，你可以扩展一个类（不论是不是array数组类这样核心类），添加一些你特别想要的方法，你可以在你想要监视的方法周围封装一些日志记录功能，你甚至可以在一个子类继承你最喜欢的类时让它执行一些特定的代码。这一切都取决于你，只有你想不到，没有你做不到。

元编程能做所有这些事情。让我们看看这本书将如何帮助你了解它。  

##关于这本书

##咒语(语法)

##小测验

##约定的符号

##单元测试

##ruby版本

##这本书的版本

这本书的第一版是关于ruby1.8，但它现在已经被废弃了。我更新了文本，包含了ruby的新特性，特别是ruby2.x版本。  
  
第二部分中的章节将使用Rails源代码作为示例的源代码。自从第一版之后，rails改变了很多，所以对比第一版的内容，这些章节几乎全部重写了。

##关于你

大多数人都认为元编程一个比较高层次的编写代码话题。想要玩转ruby程序的结构,你就必须知道这些结构都是如何在前线工作的。你如何知道你是不是一个学习元编程的高级ruby程序员？好吧，如果你可以很轻松的理解第一张的代码，那么你完全没有问题，完全可以继续往下学习。但如果你对自己的技术不自信，那么你可以进行一个简单的自我测试。你知道如何遍历数组么？如果你想到了```each```这个方法，那么你足够了解ruby了，完全可以继续往下学习。如果你想到了```for```这个关键字，那么你可能是个ruby新手，但别担心，你仍然可以踏上元编程的探险之路 —— 只是你可能需要带上一本ruby语法说明书，或者选择一个优秀的交互教程去学习ruby！(http://tryruby.org)  
  
准备好了么？好，让我们开始吧！


[返回目录](https://github.com/cynthia-n/e-book/blob/master/metaprogramming_ruby2/metaprogramming_ruby2_index.md)