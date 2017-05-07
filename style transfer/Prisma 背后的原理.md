# Prisma 背后的原理

之前看到一篇文章说，困扰Prisma团队最大问题就是 --- 

>我们没有在marketing投入过一分钱，但还是火得太快，我们的服务器承载能力完全跟不上用户的增长。

火得太快，火得太快，火得太快，不得不说，这个装逼我必须给满分！

Prisma 背后的原理其实起源于论文 [Gatys et al, “Image Style Transfer using Convolutional Neural Networks”, CVPR 2016](http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf)。这篇惊世之作一出，在学术界和工业界刮起来两股热潮。学术界陆续提出融合多种风格的算法，转换视频的算法，一次输出多种风格的算法，等等。工业界则做出网站，应用，小工具让人们给自己的照片加上梵高的风格。可以称得上是所有人的狂欢了。 那就尽这篇论文是做什么的呢？ 一张图说明白！

![](explain.jpg)

