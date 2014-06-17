
**Name**
  
  wp_get_metadata_ghcn

**Description**
  
  get metadata from certain station of ghcn. e.g. ground vegetation arround station xyz

**Usage**
  
  
- README Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/README
- Data Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/




**Input**
  
  ID of station
  
   - source: wp_read_function_ghcn.md
 datapath
 function: readGHCNmeta(datapath) and readGHCNmeta(datapath)
 
 GHCNmeta<- readGHCNmeta(datapath)
 GHCNdata<- readGHCNdata(datapath)


   

**Output**
  
 - ground vegetation of Station


**Example**
  
  
  
  


**Author**
  
   MoH

**Date**
  
  MoH 16.06.2014: creation


**TODO**
  
   -spaltename als übergabevariable schreiben
   - Example
 


### 1. take meta data  from GHCNmeta

```{r}

rausziehen <- function(IDstation){

 


```

define datapath and call functions readGHCNdata() and readGHCNmeta()

```{r}

datapath <- "D:/UNI/SoSe2014/wissProgrammieren/wipro14/rawdata/ghcnm.v3.2.2.20140514/ghcnm.tavg.v3.2.2.20140514.qca.dat"

GHCNdata <- readGHCNdata(datapath)
GHCNmeta <- readGHCNmeta(datapath)

```

finde Reihe zur ID in GHCNmeta

```{r}



IDstation <- 10764911000
META <- as.factor(GRVEG)

IDindex <- which(GHCNmeta[,1] == IDstation, arr.ind = TRUE)

OUT <- GHCNmeta$META[IDindex]




}
}

```

