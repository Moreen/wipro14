1.read data
```{r}

setwd ("D:\\UNI\\SoSe2014\\wissProgrammieren\\wipro14\\rawdata\\ghcnm.v3.2.2.20140514")
filepath <- "./ghcnm.tavg.v3.2.2.20140514.qca.dat"
GHCNmeta <- readGHCNmeta(filepath)
GHCNdata <- readGHCNdata(filepath)



```

2. compute mean temp

```{r}
mean_temp_clino <- wp_ghcn_yr_mean(GHCNdata, clino=T)
meta <- matrix(ncol=1,nrow=length(mean_temp_clino[,1]))



for(i in 1:length(mean_temp_clino[,1])){
    meta[i] <-get_metadata_ghcn(mean_temp_clino[i,1],GHCNmeta,"LATITUDE")
}

merge_mean_meta <- data.frame(mean_temp_clino, meta)


```

```{r}
qplot(merge_mean_meta$meta, merge_mean_meta$T_clino_mean)

```

