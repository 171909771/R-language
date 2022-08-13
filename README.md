## 分隔数据
```
cellcluster=cut(cellsum,quantile(cellsum,seq(0,1,1/5))) ## 按照5等分分隔
cellcluster=cut(cellsum,break=5,label=seq(1,5) ## 按照均值分隔
```
## RCPP函数的调用
- https://helixcn.github.io/2013/10/27/2013-10-27-rcpp2/
- https://blog.csdn.net/weixin_41929524/article/details/82260929   ###打包方法
#### 强行安装
```
install.packages("../test_1.0.tar.gz",repos = NULL,dependencies=TRUE, INSTALL_opts = c('--no-lock'))
```
