
**Name**
  
  explorData

**Description**
  
  explor data from GHCN (version 3) data and meta data
  make plot of data for first impression
**Usage**
  
  
- README Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/README
- Data Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/


    
  call functions:
  


**Input**
  
 - source: wp_read_function_ghcn.md
  - T_avg_meta <- readGHCNmeta(datapath)
  - T_avg_data <- readGHCNdata(datapath)

   

**Output**
  
 - Firt impression plots of vectors


**Example**
  
  
  
  


**Author**
  
   MoH

**Date**
  
  MoH 22.05.2014: creation


**TODO**
  
   - call functions
   - Example
   - xlim = c(0,49) für diagram otimieren (stichwort: max-funktion)
- Ansatz: hist(table(T_avg_meta$GRVEG),xlim = c(0,49), ylim = c(0,1500),nclass = 46)


### 1. take meta data vector from GHCNmeta

```{r}

make_histGHCNmeta <- function(T_avg_meta_var){

 
histometa <- as.numeric(as.factor(T_avg_meta_var))

```

blabla

```{r}


hist(histometa, xlim = c(0,49), ylim = c(0,1500),nclass = 46)
num_levels <- levels(as.factor(T_avg_meta_var))
num_levels

}

```


