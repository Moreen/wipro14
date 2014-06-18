
**Name**
  
 get_metadata_ghcn

**Description**
  
  get metadata from certain station of ghcn. e.g. ground vegetation arround station xyz

**Usage**
  
  
- README Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/README
- Data Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/




**Input**
  
  - ID of station and  valid meta variable
  - e.g.: ID  LATITUDE	LONGITUDE	STNELEV	NAME	GRELEV	POPCLS	POPSIZ	TOPO	           STVEG	STLOC	OCNDIS	AIRSTN	TOWNDIS	GRVEG	POPCSS
  
   - source: wp_read_function_ghcn.md
 datapath
 function: readGHCNmeta(datapath) and readGHCNmeta(datapath)
 
 GHCNmeta<- readGHCNmeta(datapath)
 GHCNdata<- readGHCNdata(datapath)


   

**Output**
  
 - ground vegetation of Station


**Example**
 
 get_metadata_ghcn(10160670000, STLOC)
 

  
  
  


**Author**
  
   MoH

**Date**
  
  MoH 16.06.2014: creation


**TODO**
  
   -vektor mit mehreren IDs übergeben
   - Example verfollständigen
   - übergabe der inputvariablen an funktion


### 1. take meta data  from GHCNmeta

```{r}

get_metadata_ghcn <- function(ID, META){

 


```

### 2. define datapath and call function readGHCNmeta()

```{r}

datapath <- "D:/UNI/SoSe2014/wissProgrammieren/wipro14/rawdata/ghcnm.v3.2.2.20140514/ghcnm.tavg.v3.2.2.20140514.qca.dat"

#GHCNdata <- readGHCNdata(datapath)
GHCNmeta <- readGHCNmeta(datapath)

```

### 3. find index of station ID

```{r}
#testinputs:
# META <- "GRVEG"
#META <- "NAME"
#META <- "POPCLS"
#IDstation <- 10160670000


IDindex <- which(GHCNmeta[,1] == IDstation, arr.ind = TRUE)
```

### 4. set up invalid message as default output

```{r}
OUT <- "invalid meta name or station ID"
```
### 5. set up wanted output value if variable was put in correctly

```{r}
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

```

### 6. create output structure with values



```{r}
ERGEBNIS<- c(IDstation,OUT)
```


}
}

```

