R卡，不能进，清空R内存
----
cd ~/.local/share/rstudio/sessions/active
## 分隔数据
```
cellcluster=cut(cellsum,quantile(cellsum,seq(0,1,1/5))) ## 按照5等分分隔
cellcluster=cut(cellsum,break=5,label=seq(1,5) ## 按照均值分隔
```
## RCPP函数的调用
- https://cloud.tencent.com/developer/article/1938199
- https://blog.csdn.net/zhouyongsdzh/article/details/16809355
- https://blog.csdn.net/weixin_41929524/article/details/82260929   ###打包方法
```C++
#include <Rcpp.h>
using namespace Rcpp;

// 注意 #include <Rcpp.h> 是调用Rcpp的必要条件
// [[Rcpp::export]]
RcppExport SEXP expfun(SEXP vec){
  Rcpp::NumericVector vec2(vec);
  int prod = 0;
  prod = vec2[1]*5;
  return (wrap(prod));
}

// [[Rcpp::export]]
RcppExport SEXP expfun1(SEXP vec){
  int i= as<int>(vec);
  int prod = 0;
  prod = i*5;
  return (wrap(prod));
}
```
### 保存cpp后，再用sourceCpp调用里面的函数，就可以直接用了

强行安装，repos代表不通过网络安装
------
```
install.packages("../test_1.0.tar.gz",repos  = NULL,dependencies=TRUE, INSTALL_opts = c('--no-lock'))
```

安装软件，设置镜像
----
```
install.packages("metap",repos="http://mirrors.tuna.tsinghua.edu.cn/CRAN/")
## bioconductor
- https://www.bioconductor.org/about/mirrors/
options(BioC_mirror="http://mirrors.ustc.edu.cn/bioc/")     #需要重启
```

并行
----
- https://zhuanlan.zhihu.com/p/70432486
```
library(parallel)
#第一个函数，申请需要使用的逻辑核心数，cl可以理解为代表申请的逻辑核
cl <- makeCluster(14)
#第二个函数，在每个逻辑核（cl）上加载计算需要用到的R包
clusterEvalQ(cl,library(statmod))
#第三个函数，在每个逻辑核（cl）上加载用到的变量，这里写变量的名字
clusterExport(cl,'y1')
#开始运行
result.tweedie=parApply(cl=cl,X=dat.microglia.nor,MARGIN=1,function(x){  
  y=glm(y1~x,family=tweedie(var.power=1.6,link.power=0))
  y2=summary(y)
  return(c(y2$coefficients[2],y2$coefficients[8]))})
#结束
stopCluster(cl)
```
