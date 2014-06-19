
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
if(sum(checkID,checkNAMES) != 2){stop("invalid meta name or station ID")}


```



### 2. find index of station ID

```{r}


IDindex <- which(GHCNmeta[,1] == IDstation, arr.ind = TRUE)
```

### 3. set up wanted output value if variable was put in correctly

```{r}
if (METAname == "ID") {OUT <- GHCNmeta$ID[IDindex]}
if (METAname == "LATITUDE") {OUT <- GHCNmeta$LATITUDE[IDindex]}
if (METAname ==  "LONGITUDE") {OUT <- GHCNmeta$LONGITUDE[IDindex]}	
if (METAname == "STNELEV") {OUT <- GHCNmeta$STNELEV[IDindex]}
if (METAname == "NAME") {OUT <- GHCNmeta$NAME[IDindex]}
if (METAname == "GRELEV") {OUT <- GHCNmeta$GRELEV[IDindex]}
if (METAname == "POPCLS") {OUT <- GHCNmeta$POPCLS[IDindex]}
if (METAname == "POPSIZ") {OUT <- GHCNmeta$POPSIZ[IDindex]}
if (METAname == "TOPO") {OUT <- GHCNmeta$TOPO[IDindex]}
if (METAname == "STVEG") {OUT <- GHCNmeta$STVEG[IDindex]}
if (METAname == "STLOC") {OUT <- GHCNmeta$STLOC[IDindex]}
if (METAname == "OCNDIS")	{OUT <- GHCNmeta$OCNDIS[IDindex]}
if (METAname == "AIRSTN") {OUT <- GHCNmeta$AIRSTN[IDindex]}
if (METAname == "TOWNDIS"){OUT <- GHCNmeta$TOWNDIS[IDindex]}
if (METAname == "GRVEG") {OUT <- GHCNmeta$GRVEG[IDindex]}            
if (METAname == "POPCSS")  {OUT <- GHCNmeta$POPCSS[IDindex]}

```

### 4. create output structure with values



```{r}
ERGEBNIS<- c(OUT)

}
```




