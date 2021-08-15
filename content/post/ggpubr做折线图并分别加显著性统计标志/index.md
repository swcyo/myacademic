---
title: ggpubr做折线图并分别加显著性统计标志
date: 2021-08-15T16:39:02.244Z
draft: false
featured: false
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
* `ggpubr`作图简单，不需要特别公式就可以计算均数和标准差，相比`ggplot2`简单很多，但是框架比较限制，但是比较而言，个人觉得`ggpubr`就够用，`ggplot2`经典，但是需要大量代码，具体用哪个，见仁见智
2.首先是`ggplot2`做折线图，需要另外计算均数和标准差，应该需要现定义一个函数,本文介绍ggpubr
```
p<-ggline(data, "x",  "y", color = "group",shape='group', add = "mean_se", palette = 'aaas',ggtheme = theme_bw())
#多个样本比较(非参数检验)
p+stat_compare_means(method = "kruskal.test")+ 
  stat_compare_means(label = "p.signif", method = "wilcox.test",
                     ref.group = ".all.", hide.ns = TRUE)
#多个样本比较(参数检验，anova，t检验)
p+stat_compare_means(method = "anova")+                      stat_compare_means(label = "p.signif", method = "t.test",
                     ref.group = ".all.", hide.ns = TRUE)
+theme(legend.position=c(0.9,0.2))
  ```