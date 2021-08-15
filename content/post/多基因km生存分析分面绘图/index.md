---
title: 多基因KM生存分析分面绘图
date: 2021-08-15T16:59:55.475Z
draft: false
featured: false
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
 🇨🇳 

#宽数据转为长数据，先加载包
library(tidyr)
library(reshape2)

#数据转换
data33_survival2<-melt(data33_survival,
id.vars = c("Status","Time"),
variable.name='gene',
value.name='value')

#作图定义fit
fit<-survfit(Surv(Time,Status)~value,
data=data33_survival2)

#分面作图
ggsurvplot(fit,
pval = T,#显示p值
pval.method =T,#显示logrank
short.panel.labs=T,#去掉分组名
facet.by = "gene",#分面
scale="free",#可不使用
ggtheme = theme_bw())#背景主题
```

```