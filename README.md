## 分隔数据
```
cellcluster=cut(cellsum,quantile(cellsum,seq(0,1,1/5))) ## 按照5等分分隔
cellcluster=cut(cellsum,break=5,label=seq(1,5) ## 按照均值分隔
```
