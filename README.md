# ElemeProject
![](https://raw.githubusercontent.com/samlaudev/ElemeProject/master/ScreenShots/Eleme-Images.jpg)

由[Sam Lau](http://www.jianshu.com/users/256fb15baf75/latest_articles)用Objective-C编写的一个模拟的[**饿了么**](http://bzclk.baidu.com/adrc.php?t=00KL00c00fAoF900FWu70nsem00kZAIN00000aMzyzf00000usuy7Q.THvvq_ZQsef0UWdBmy-bIy9EUyNxTAT0T1Y3mHfduH7BmW0snjD3uWfs0ZRqPjmLPHcvfWPKwbNjnYn4nbnYnjRLwRczwWm1fW0vPj60mHdbXWKVmLCsP7-RRH7pNDuGyyGKIYdDwHwpp-7LihYkph7gRH-PNDY1HyGunR4DHgG5fdGLmvY4pv7gRH-PN7-VyNfsX79lfydbw104ih4yI7KHyMuWUy_4HNPpXhwgiMuWUy_4ih4aXy7RnZ-2URuom1P2p-KRfiR1w0K-5y9YIZ0lQzq-UAR8UyR0mLFW5HfLn1Tz&wd=饿了么&issp=1&f=8&ie=utf-8&tn=baiduhome_pg)客户端

##Table of Contents
###1. [Prerequisite (先决条件)](#prerequisite)
###2. [Development Process (开发过程)](#development_proces)
###3. [Best Practices (最佳实践)](#best_practices)
###4. [Join Us (共同参与项目)](#join_us)

<b id="prerequisite"></b>
#Prerequisite
##敏捷开发
* 掌握如何收集、编写和测试用户故事，估算已有的用户故事并发布计划 --- 参考书籍：[用户故事与敏捷方法](http://book.douban.com/subject/4743056/)
* 熟悉Scrum开发过程和如何管理和跟进项目进度 --- 参考书籍[硝烟中的Scrum和XP](http://book.douban.com/subject/3390446/)
* 了解XP极限编程的基本实践 --- 参考书籍[解析极限编程](http://book.douban.com/subject/6828074/)


##MVVM(Model-View-View Model)
![MVVM high level.png](http://upload-images.jianshu.io/upload_images/166109-81012f4948373da5.png)
在MVVM架构中，通常都将view和view controller看做一个整体。相对于之前MVC架构中view controller执行很多在view和model之间数据映射和交互的工作，现在将它交给view model去做。
至于选择哪种机制来更新view model或view是没有强制的，但通常我们都选择[ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa)。ReactiveCocoa会监听model的改变然后将这些改变映射到view model的属性中，并且可以执行一些业务逻辑。

举个例子来说，有一个model包含一个dateAdded的属性，我想监听它的变化然后更新view model的dateAdded属性。但model的dateAdded属性的数据类型是NSDate，而view model的数据类型是NSString，所以在view model的init方法中进行数据绑定，但需要数据类型转换。示例代码如下：

```
RAC(self,dateAdded) = [RACObserve(self.model,dateAdded) map:^(NSDate*date){ 
    return [[ViewModel dateFormatter] stringFromDate:date];
}];
```

ViewModel调用dateFormatter进行数据转换，且方法dateFormatter可以复用到其他地方。然后view controller监听view model的dateAdded属性且绑定到label的text属性。

```
RAC(self.label,text) = RACObserve(self.viewModel,dateAdded);
```

现在我们抽象出日期转换到字符串的逻辑到view model，使得代码可以**测试**和**复用**，并且帮view controller**瘦身**。

##项目目录结构

##Objective-C 编码规范
关于Objective-C的编码规范，请参考我翻译的[raywenderlich.com Objective-C编码规范](https://github.com/samlaudev/Objective-C-Coding-Style)

##iOS 最佳实践

##iOS 开源库
* [ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa)
* [AFNetworking](https://github.com/AFNetworking/AFNetworking)
* [Mantle](https://github.com/Mantle/Mantle)
* [Masonry](https://github.com/SnapKit/Masonry)
* [Classy](https://github.com/cloudkite/Classy)
* [ClassyLiveLayout](https://github.com/olegam/ClassyLiveLayout)
* [Kiwi](https://github.com/kiwi-bdd/Kiwi)

<b id="development_proces"></b>
#Development Process
![](https://raw.githubusercontent.com/samlaudev/ElemeProject/master/ScreenShots/Scrum-Development-Process.jpg)

##Prodcut Backlog
##Sprint计划
##Sprint Backlog
##1-4 Week Sprint
##Sprint演示

<b id="best_practices"></b>
#Best Practices

##增量设计与重构

##TDD与BDD

##Git版本控制和工作流

##持续集成测试

##代码规范

##Code Review

<b id="join_us"></b>
#Join Us
