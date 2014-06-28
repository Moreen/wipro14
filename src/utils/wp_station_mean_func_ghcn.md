
**Name**

wp_ghcn_yr_mean

**Description**

Functions for calc station means of GHCN dataset 
or clino means of these stations that have complete data for at least n_clino_yr years of clino timespan


**Usage**

MEAN <- wp_ghcn_yr_mean(data, SD=TRUE/FALSE, clino=TRUE/FALSE, n_clino_yr)

Default: - SD = F
         - clino = F
         - n_clino_yr = 30


call functions:

- output data <- wp_station_mean_func_ghcn(_data_, SD=TRUE/FALSE (optional))

_data_ <- wp_ghcn_yr_mean(data)

call functions:

- output data <- wp_station_mean_func_ghcn(_data_)

**Input**

ghcn monthly
function: readGHCNdata(datapath)

- README Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/README
- Data Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/





**Output**

annual means and their standart deviation or
mean temerature of clino time span (1961 - 1990) with only datasets that have at least complete data of n_clino_yr years of clino time span 


**Example**

T_yr_mean <- wp_ghcn_yr_mean(data)

**Author**

AlK, Moh

**Date**

AlK 25.06.2014: first version

**TODO**

- Selektieren nach Stationseigenschaften z.B. Name 
Idee mean_func(orig_dataset, Name="XYZ") 

```{r}

wp_ghcn_yr_mean <- function(data, SD=FALSE, clino=FALSE, n_clino_yr=30) {

  #achtung: manuell einlesen
  #clino <- T
  #n_clino_yr = 30
  #data <- GHCNdata
  #SD=F
 

if(clino){
  
  data <- subset(data, YEAR >= 1961 & YEAR <= 1990)
  
}

  
  
n_ys = length(data$YEAR)  
T_yr_mean <- matrix(nrow=n_ys)
stdev <- matrix(nrow=n_ys)


if(SD){
  for (n in 1:n_ys) {
    
    T_yr_mean[n] <- mean(c(data$VALUE1[n],data$VALUE2[n],data$VALUE3[n],data$VALUE4[n],data$VALUE5[n],data$VALUE6[n],
                           data$VALUE7[n],data$VALUE8[n],data$VALUE9[n],data$VALUE10[n],data$VALUE11[n],data$VALUE12[n]), na.rm = F)
    # na.rm = F ignoriert alle Mittlungen für Jahre mit fehlenden Monatswertten
  
    stdev[n] <- sd(c(data$VALUE1[n],data$VALUE2[n],data$VALUE3[n],data$VALUE4[n],data$VALUE5[n],data$VALUE6[n],
                           data$VALUE7[n],data$VALUE8[n],data$VALUE9[n],data$VALUE10[n],data$VALUE11[n],data$VALUE12[n]), na.rm = F)
  }
  
  sub <- data.frame(T_yr_mean,stdev)
  } else {
 
    for (n in 1:n_ys) {
    T_yr_mean[n] <- mean(c(data$VALUE1[n],data$VALUE2[n],data$VALUE3[n],data$VALUE4[n],data$VALUE5[n],data$VALUE6[n],
                           data$VALUE7[n],data$VALUE8[n],data$VALUE9[n],data$VALUE10[n],data$VALUE11[n],data$VALUE12[n]), na.rm = F)
    }
  
    
   
    
    
    sub <- data.frame(data$ID,data$YEAR,T_yr_mean)
  }


```

In case option clino is activated -> subset of total matrix and get rid of NAs

```{r}

if(clino){

    ID <- unique(as.numeric(as.character(sub$data.ID)))
    clino_mean <- matrix(nrow = length(ID), ncol=2)
    colnames(clino_mean) <- c("stationID", "T_clino_mean") 

    clino_na_free <- subset(sub, !is.na(T_yr_mean), select= c(data.ID, data.YEAR, T_yr_mean))

```


cutting out the clino data which has complete data for at least n_clino_yr Years. 

```{r}

    for(i in 1:length(ID)){
      
temp <- clino_na_free[which(clino_na_free$data.ID == ID[i],arr.ind = TRUE),]
if (length(temp$data.ID)>=n_clino_yr){ 
  
  clino_mean[i,1] <- ID[i]
  clino_mean[i,2] <- sum(temp$T_yr_mean)/n_clino_yr
  }
}
clino_mean_complete_data<- subset(clino_mean, !is.na(clino_mean[,1]))
      
      }
      
     
return(clino_mean_complete_data)

}

```

