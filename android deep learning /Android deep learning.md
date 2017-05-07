###开发深度学习的Android应用

Google亲爹最近动作很大，我们不也要更上脚步么。上次看到篇文章说Prisma 团队坦言他们公司最大的困扰就是 **增长太快，增长太快，增长太快**

![](sad.jpeg)

我（stormzhang自己）上周写过人人都该学点编程，Android开发很长一段时间依旧是主流，感兴趣算法的同学可以学习深度学习领域，学习下Tensforflow，那么问题来了，怎么学呢？ 当然是做一个深度学习的 Android 应用啦！

说干就干，Google 早就开源了一个 TensorFlow Android Camera Demo 的库 (https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/android), 其中包含了三个样例应用：

- 分类（TF Classify）

  ![](classify.jpg)


- 识别（TF Detect）

  ![](detect.jpg)
  

- 渲染（TF Stylize）
 
  ![](stylize.jpg)

迫不及待就安装玩耍了一番，感觉棒棒哒。当然直接下载构建好了的APK有什么意思，我们可是程序员，于是一阵折腾，自己把库拖下来构建了一番，一样轻松搞定。

有了这三个APP，思路如潮水般涌来，做个名片自动录入的应用？ 做个按照当天天气渲染图片的应用？做个实时翻译彩蛋的应用？做个门禁识别应用？ 立刻开始创业，马上开始融资，从此就要走向人生巅峰了！

![](top.jpeg)

啊，等等。似乎我用的是别人训练好的模型。怎么训练自己的模型？ 似乎tensorflow 的模型都是用python 写的，Android 应用不都是用java 的吗？似乎都适用RESTFUL API进行分类和计算的，离线能不能实现？走向人生巅峰的路上，似乎还有数不清的坑啊！似乎这些demo都好丑啊，我自己都不想用，能不能做得好看一点啊？

看来还是要靠Google，Google一定会教我的！

**to yuhang: 下面开始文末卖课，我编不下去了，要不你接着卖？**