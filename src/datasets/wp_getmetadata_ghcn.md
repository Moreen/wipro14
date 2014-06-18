
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
 
 get_metadata(10160670000, STLOC)
 

  
  
  


**Author**
  
   MoH

**Date**
  
  MoH 16.06.2014: creation


**TODO**
  
   -vektor mit mehreren IDs übergeben
   - Example verfollständigen
 


### 1. take meta data  from GHCNmeta

```{r}

get_metadata <- function(ID, META){

 


```

define datapath and call functions readGHCNdata() and readGHCNmeta()

```{r}

datapath <- "D:/UNI/SoSe2014/wissProgrammieren/wipro14/rawdata/ghcnm.v3.2.2.20140514/ghcnm.tavg.v3.2.2.20140514.qca.dat"

GHCNdata <- readGHCNdata(datapath)
GHCNmeta <- readGHCNmeta(datapath)

```

finde Reihe zur ID in GHCNmeta

```{r}
#testinputs:
# META <- "GRVEG"
#META <- "NAME"
#META <- "POPCLS"
#IDstation <- 10160670000

IDindex <- which(GHCNmeta[,1] == IDstation, arr.ind = TRUE)

OUT <- "invalid meta name or station ID"

if (META == "ID") {OUT <- GHCNmeta$ID[IDindex]}
if (META == "LATITUDE") {OUT <- GHCNmeta$LATITUDE[IDindex]}
if (META ==  "LONGITUDE") {OUT <- GHCNmeta$LONGITUDE[IDindex]}	
if (META == "STNELEV") {OUT <- GHCNmeta$STNELEV[IDindex]}
if (META == "NAME") {OUT <- GHCNmeta$NAME[IDindex]}
if (META == "GRELEV") {OUT <- GHCNmeta$GRELEV[IDindex]}
if (META == "POPCLS") {OUT <- GHCNmeta$POPCLS[IDindex]}
if (META == "POPSIZ") {OUT <- GHCNmeta$POPSIZ[IDindex]}
if (META == "TOPO") {OUT <- GHCNmeta$TOPO[IDindex]}
if (META == "STVEG") {OUT <- GHCNmeta$STVEG[IDindex]}
if (META == "STLOC") {OUT <- GHCNmeta$STLOC[IDindex]}
if (META == "OCNDIS")	{OUT <- GHCNmeta$OCNDIS[IDindex]}
if (META == "AIRSTN") {OUT <- GHCNmeta$AIRSTN[IDindex]}
if (META == "TOWNDIS"){OUT <- GHCNmeta$TOWNDIS[IDindex]}
if (META == "GRVEG") {OUT <- GHCNmeta$GRVEG[IDindex]}            
if (META == "POPCSS")  {OUT <- GHCNmeta$POPCSS[IDindex]}






}
}

```

