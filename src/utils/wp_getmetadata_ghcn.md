
**Name**
  
 get_metadata_ghcn

**Description**
  
  get metadata from certain station of ghcn. e.g. ground vegetation arround station xyz

**Usage**
  

#GHCNdata <- readGHCNdata(datapath)
GHCNmeta <- readGHCNmeta(datapath)
  
  
- README Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/README
- Data Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/




**Input**
  
  - ID of station and  valid meta variable
  - e.g.: ID  LATITUDE	LONGITUDE	STNELEV	NAME	GRELEV	POPCLS	POPSIZ	TOPO	           STVEG	STLOC	OCNDIS	AIRSTN	TOWNDIS	GRVEG	POPCSS
  
   - source: wp_read_function_ghcn.md

  datapath <- "D:/UNI/SoSe2014/wissProgrammieren/wipro14/rawdata/ghcnm.v3.2.2.20140514/ghcnm.tavg.v3.2.2.20140514.qca.dat"

 function: readGHCNmeta(datapath) and readGHCNmeta(datapath)
 
 GHCNmeta<- readGHCNmeta(datapath)
 GHCNdata<- readGHCNdata(datapath)


   

**Output**
  
 - searched meta data of Station


**Example**
 
 get_metadata_ghcn(10160670000, GHCNmeta ,STLOC)
 

  
  
  


**Author**
  
   MoH

**Date**
  
  MoH 16.06.2014: creation


**TODO**
  
   
   - Example verfollständigen
   - evtl. optimieren der if-abfragen


### 1.  check arguments

```{r}

get_metadata_ghcn <- function(ID, GHCNmeta, METAname){

 
checkID <- sum(ID == GHCNmeta$ID)
name <- names(GHCNmeta)
checkNAMES <- sum(METAname == name)
if(sum(checkID,checkNAMES) != 2){


if (checkNAMES != 1){message(c("Meta data", METAname ," does not exsist in data frame"))}
if ( checkID != 1){message(c("Wrong Station ID:", ID))}
stop()
}

```




### 2. find index of station ID

```{r}


IDindex <- which(GHCNmeta[,1] == ID, arr.ind = TRUE)
```

### 3. find index of Meta data column

```{r}


METAindex<-which(name == METAname)


```

### 4. create output structure with values



```{r}
out <- GHCNmeta[IDindex,METAindex]



return(out)

}
```


