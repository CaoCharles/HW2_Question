---
title: "Question 01"
output: 
  html_document:
    keep_md: true
---

```r
library(ggplot2)
library(dplyr)
library(kableExtra)
library(knitr)
#setwd("/Users/kevinpiger/Desktop/碩一下/統模/Homework02/")
options(scipen = 100)
```

# Uniform (0,1) transformation
For uniform (0,1) random variables $U_1,U_2, ... ,$ define N = min{n :$\sum_{i=1}^{n}{U_i>1}$ }.
That is, N is the number of random numbers that must be summed to exceed 1.

## (a) 
Estimate E(N) with standard errors by generating 1,000, 2,000, 5,000, 10,000,
and 100,000 values of N, and check if there are any patterns in the estimate and its s.e.

```r
# T 欲模擬次數 #
Q1 <- function(T){
N = NULL
S = NULL
for( i in 1:T){
  n = 0; i = 0
  while(n < 1){
    n = sum(n ,runif(1))
    i = i + 1}
    N <- c(N,i)
    }
  return(N)
}
```

Calculation and output

```r
output <- NULL
output2 <- NULL
sim <- c(1000, 2000, 5000, 10000, 100000)
for(i in 1:5){
  output[i] <- mean(Q1(sim[i]));
  output2[i] <- var(Q1(sim[i]))
}
output <- t(output)
output2 <- t(output2)
output <- rbind(output,output2)
rownames(output) <- c("Output","var")
colnames(output) <- sim
kable(output,"html") %>% 
  kable_styling(bootstrap_options = 'striped', full_width = F) %>% 
  add_header_above(c(" " = 1, "# of Simulation" = 5))
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
<tr>
<th style="border-bottom:hidden" colspan="1"></th>
<th style="text-align:center; border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;" colspan="5"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px;"># of Simulation</div></th>
</tr>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> 1000 </th>
   <th style="text-align:right;"> 2000 </th>
   <th style="text-align:right;"> 5000 </th>
   <th style="text-align:right;"> 10000 </th>
   <th style="text-align:right;"> 100000 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Output </td>
   <td style="text-align:right;"> 2.7610000 </td>
   <td style="text-align:right;"> 2.706000 </td>
   <td style="text-align:right;"> 2.7112000 </td>
   <td style="text-align:right;"> 2.7153000 </td>
   <td style="text-align:right;"> 2.7177600 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> var </td>
   <td style="text-align:right;"> 0.7283123 </td>
   <td style="text-align:right;"> 0.736496 </td>
   <td style="text-align:right;"> 0.7714232 </td>
   <td style="text-align:right;"> 0.7737012 </td>
   <td style="text-align:right;"> 0.7694329 </td>
  </tr>
</tbody>
</table>

## (b) 
Compute the density function of N, E(N), and Var(N).

>>E(N) = e

>>Var(N) = 3e-e^2
