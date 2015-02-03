### Cluster Evaluation R package (ClueR) for detecting key signaling events from time-series phosphoproteomics data

##### Description
CLUster Evaluation (or "CLUE") is an R package for identifying optimal number of clusters in a given time-course dataset clustered by cmeans or kmeans algorithms. It relies on a reference annotation set to test for enrichment in
each cluster using Fisher's Exact Test and then test for overall enrichment of the entire clusters using Fisher's
combined probability test.

CLUE is designed for analyzing time-course phosphoproteomics dataset using kinase-substrate annotation as reference. However, it can be applied to time-course microarray dataset as well by replacing the kinase-substrate annotation with gene sets annotation.

Download the latest release [here](https://github.com/PengyiYang/ClueR/releases)

###### Examples

``` r
## install the latest release of ClueR package

# load the package into R session
library(ClueR) 

# load the human ES phosphoprotoemics data (Rigbolt et al. Sci Signal. 4(164):rs3, 2011)
data(hES) 

# load the PhosphoSitePlus annotations (Hornbeck et al. Nucleic Acids Res. 40:D261-70, 2012)
data(PhosphoSite)
# run CLUE with a repeat of 5 times and a range from 2 to 20
set.seed(2)
clueObj <- runClue(Tc=hES, annotation=PhosphoSite.human, rep=5, kRange=20)

# visualize the evaluation outcome
Ms <- apply(clueObj$evlMat, 2, mean, na.rm=TRUE)
Ss <- apply(clueObj$evlMat, 2, sd, na.rm=TRUE)
library(Hmisc)
errbar(1:length(Ms), Ms, Ms+Ss, Ms-Ss, cex=1.2, type="b", xaxt="n", xlab="k", ylab="E score")
axis(1, at=1:19, labels=paste("k=", 2:20, sep=""))

# generate the optimal clustering results
best <- clustOptimal(clueObj, rep=10, mfrow=c(3, 4))

# list enriched clusters
best$enrichList

# obtain the optimal clustering object (not run)
# best$clustObj
```
    
