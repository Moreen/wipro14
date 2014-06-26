
**Name**

wp_ghcn_yr_mean

**Description**

Functions for calc station means of GHCN dataset 

**Usage**

MEAN <- wp_ghcn_yr_mean(data, SD=TRUE/FALSE)

call functions:

- output data <- wp_station_mean_func_ghcn(_data_, SD=TRUE/FALSE (optional))

MEAN <- wp_ghcn_yr_mean(data)

call functions:

- output data <- wp_station_mean_func_ghcn(_data_)

**Input**

ghcn monthly
function: readGHCNdata(datapath)

- README Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/README
- Data Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/





**Output**

annual means and their standart deviation or
annual means for the clino time span (1961 - 1990)


**Example**

T_yr_mean <- wp_ghcn_yr_mean(data)

**Author**

AlK

**Date**

AlK 25.06.2014: first version

**TODO**

- Selektieren nach Stationseigenschaften z.B. Name 
Idee mean_func(orig_dataset, Name="XYZ") 

```{r}

wp_ghcn_yr_mean <- function(data, SD=FALSE, clino=FALSE) {

  #achtung: manuell einlesen
  clino <- T
 data <- GHCNdata
 SD=F
 

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

 ID <- unique(as.numeric(as.character(sub$data.ID)))
clino_mean <- matrix(nrow = length(ID))
    
    for(i in 1:length(ID)){
      if(length(which(sub$data.ID==ID[i]))==30  & length(!is.na(sub$T_yr_mean[which(sub$data.ID==ID[i])]))==30)
      {clino_mean[i] <- 3 }
    }

#T_yr_mean_clino[i] <- cbind(ID[i], mean(subset(which(sub$data.ID==ID[i])


}

```

