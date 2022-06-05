---
title: "Goodman Kruskal Association Plots"
author: "semanticnoodles"
output: 
---
 # About Goodman-Kruskal Tau
The Goodman-Kruskal Tau is an asymmetric association measure between two categorical variables, based on the extent to which variation in one variable can be explained by the other. This function returns an S3 object of class 'GKtauMatrix' that gives the number of levels for each variable on the diagonal of the matrix and the association between variables in the off-diagonal elements. Note that this matrix is generally NOT symmetric, in contrast to standard correlation matrices.

# Workflow
## Load required libaries and dataset
```r
# Load libraries
library(dplyr)
library(RColorBrewer)
library(GoodmanKruskal)

# Load data
eventdata <- read.table(file="~/eventcodes.csv", header = T, sep=",")
head(eventdata)
```
## Dataset adjustments
```r
# Label columns
colnames(eventdata) <- c("case.study","event.type","event.code", "sample.code", "sex", "age", "edu.level", "work", "returning", "visiting", "local")

# Filter the dataset - Vignale
data_V <- filter(eventdata, case.study == "V")
sum(is.na(data_V))

# Filter the dataset - Massaciuccoli Romana
data_MR <- filter(eventdata, case.study == "MR")
sum(is.na(data_MR))

# Filter the dataset - Poggio del Molino
data_PdM <- filter(eventdata, case.study == "PdM")
sum(is.na(data_PdM))

# Select the palette to be used in the plots
pal <- brewer.pal(11,"RdBu")
```
## Outputs 
### Vignale (V)
```r
# Obtain the association matrix
assmat_V <- GKtauDataframe(data_V[,c(2,5:11)], includeNA = "no")

# Plot  
plot(assmat_V, backgroundColor = pal, corrColors = "black" )
```
### Massaciuccoli Romana (MR)
```r
# Obtain the association matrix
assmat_MR <- GKtauDataframe(data_MR[,c(2,5:11)], includeNA = "no")

# Plot the association heatmap
plot(assmat_MR, backgroundColor = pal, corrColors = "black" )
```
### Poggio del Molino
```r
# Obtain the association matrix
assmat_PdM <- GKtauDataframe(data_PdM[,c(2,5:11)], includeNA = "no")

# Plot the association heatmap
plot(assmat_PdM, backgroundColor = pal, corrColors = "black" )
```