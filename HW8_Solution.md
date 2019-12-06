HW8
================

``` r
knitr::opts_chunk$set(echo = FALSE,
                      warning = FALSE, 
                      message = FALSE, 
                      echo = TRUE,
                      eval = FALSE
                      )
```

Directions: Your final github repository should contain 1) the .Rmd file
and 2) a HTML file (make sure to commit both\!). Also, please make sure
that your code chunk for each question is visible in the HTML document,
and that all warning messages are removed. Please do not include
unnecessary and lengthy output, or points will be taken off. Please
check your HTML file to make sure it is complete with all of your
answers. The assignment is due on Thursday November 21st, at midnight.

## Question 1.

### Part A:

Load the mouse cortex data. Calculate the fano factor for all of the
genes, and then select the genes with a fano factor greater than
35.

``` r
load(file="C:/Users/Nina/Documents/1-NYU/TA Materials/Intro to Biostats & EDA 2019/Datasets/cortex_data.RData")
fano = apply(cortex_data,1,var)/apply(cortex_data,1,mean)
fano_genes = names(which(fano>35))
```

### Part B:

Perform NMF on the selected genes, using a rank of 10. Plot a heatmap of
the basis matrix.

``` r
library(NMF, quietly=TRUE)
library(fastICA, quietly=TRUE)
library(ComplexHeatmap, quietly=TRUE)
NMF_rank = 10
results = nmf(cortex_data[fano_genes,], rank = NMF_rank, seed = 'ica', method = 'nsNMF')
Basis_matrix= basis(results)
Heatmap(Basis_matrix, row_names_gp = gpar(cex=0.3))
```

## Question 2.

### Part A:

Repeat the steps of Q1 part B above, but now using a rank of 5.

``` r
NMF_rank = 5
results2 = nmf(cortex_data[fano_genes,], rank = NMF_rank, seed = 'ica', method = 'nsNMF')
Basis_matrix2= basis(results2)
Heatmap(Basis_matrix2, row_names_gp = gpar(cex=0.3))
```

### Part B:

Intepret the heatmap in part A (explain what the basis matrix is and
what it means). Compare it to the heatmap in Q1 part B and explain the
difference.

The basis matrix has rows that are composed of each of the selected
genes, and columns that are composed of the basis elements, or features.
In the case of Q1 Part B, the number of columns is 10 because we chose a
rank of 10, whereas in Q2 part A, the number of columns is 5. The basis
elements are features of the data that are summarized into 5. We can
think of the columns of the basis matrix, often denoted as W, as signals
that sum to make our data. We see that in each column, different
clusters of genes are differentially expressed. As we reduce the rank
from 10 to 5, we lose some level of detail in the data as we see that
each of the columns contains a larger cluster of expressed genes.
However, in our case, with a rank of 10, some of the columns are fully
zero across all of the genes indicating that 10 is likely too high of a
choice of rank.

## Question 3.

Load the pancreas data and clean. Calculate the fano factor for all of
the genes, and then select the genes with a fano factor greater than
20.

``` r
P = read.csv("C:/Users/Nina/Documents/1-NYU/TA Materials/Intro to Biostats & EDA 2019/Datasets/Pancreas_dataset_gene_expression1.csv", header=FALSE)
P = P[!duplicated(P[,1]),]
rownames(P) = P[,1]
P = P[, -1]

fano = apply(P,1,var)/rowMeans(P)
fano_genes = names(which(fano>20))
```

## Question 4.

Perform NMF on the selected genes, using a rank of 20. Plot a heatmap of
the basis matrix.

## Question 5.

Plot a heatmap of the coefficient matrix. Explain how the basis matrix
and the coefficient matrix relate to one another.

``` r
Coef_matrixq4 = coef(res_q4)
Heatmap(Coef_matrixq4, row_names_gp = gpar(cex=0.3))
names(which(Basis_matrixq4[,1]>.05))
```

Explanation: NMF is an algorithm that factorizes the given matrix into
two matrices. All three matrices must have no negative values.

\[V_{mxn} = W_{mxp}H_{pxn}\] Where p is specified to the algorithm. p
can be thought of as the number of features to search for. W can be
thought of as the features, and H can be thought of as the weights of
these features.

## Question 6.

Perform PCA on the Pancreas data from Question 3. Plot a biplot using
the first two PCs. Which genes contribute most to PC1 and PC2?

``` r
out <- prcomp(t(P[fano_genes,]))
biplot(out)
```

Genes contributing most: INS, SST, IAPP
