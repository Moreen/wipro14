
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

annual means and their standart deviation


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

wp_ghcn_yr_mean <- function(data, SD=FALSE) {

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
  
  return(data.frame(T_yr_mean,stdev))
  }
else
  {
    for (n in 1:n_ys) {
    T_yr_mean[n] <- mean(c(data$VALUE1[n],data$VALUE2[n],data$VALUE3[n],data$VALUE4[n],data$VALUE5[n],data$VALUE6[n],
                           data$VALUE7[n],data$VALUE8[n],data$VALUE9[n],data$VALUE10[n],data$VALUE11[n],data$VALUE12[n]), na.rm = F)
    }
    return(data.frame(data$ID,data$YEAR,T_yr_mean))
  }
}

```

