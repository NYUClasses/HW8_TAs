HW8
================

Directions: Your final github repository should contain 1) the .Rmd file and 2) a HTML file (make sure to commit both!). Also, please make sure that your code chunk for each question is visible in the HTML document, and that all warning messages are removed. Please do not include unnecessary and lengthy output, or points will be taken off. Please check your HTML file to make sure it is complete with all of your answers. The assignment is due on Thursday November 21st, at midnight.

Question 1.
-----------

### Part A:

Load the mouse cortex data. Calculate the fano factor for all of the genes, and then select the genes with a fano factor greater than 35.

### Part B:

Center the cortex data. Perform NMF on the selected genes from the centered data, using a rank of 10. Plot a heatmap of the basis matrix.

Question 2.
-----------

### Part A:

Repeat the steps of Q1 part B above, but now using a rank of 5.

### Part B:

Intepret the heatmap in part A (explain what the basis matrix is and what it means). Compare it to the heatmap in Q1 part B and explain the difference.

Question 3.
-----------

Load the pancreas data and clean. Calculate the fano factor for all of the genes, and then select the genes with a fano factor greater than 20.

Question 4.
-----------

Center the pancreas data. Perform NMF on the selected genes from the centered data, using a rank of 20. Plot a heatmap of the basis matrix.

Question 5.
-----------

Plot a heatmap of the coefficient matrix. Explain how the basis matrix and the coefficient matrix relate to one another.

Question 6.
-----------

Perform PCA on the Pancreas data from Question 3. Plot a biplot using the first two PCs. Which genes contribute most to PC1 and PC2?
