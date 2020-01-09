# Demand Models With Random Partitions

# Author Contributions Checklist Form

## Data

### Abstract

There is one data set attached corresponding to the empirical application in the paper. The data set contains store-level price and sales data for 40 products in the salty snack category over a five-year period.

### Availability

The data set was purchased from Information Resources, Inc. (IRI) and is part of the IRI Academic Data Set. We have included the data for review purposes only. In place of the actual data set, we have included code to simulate data and repeat the analysis done in the empirical section of the paper.

## Code

### Abstract 

The code includes functions to sample from and evaluate the probability mass function of the DP and LSP distributions, conduct simulation studies to compare LSP proposals to other posterior sampling routines, and estimate the store-level demand model proposed in the paper using both the empirical data and a simulated data set. The code is written in R and C++ and is integrated using the Rcpp package.

Description

How delivered: R code
Licensing information: MIT License
Link to code/repository: https://github.com/adam-n-smith (to be made available)
Optional Information (complete as necessary)

Supporting software requirements:
* Software: R (>= 3.5.1)
* Required Libraries: bayesm (>= 3.1-0.1), clues (>= 0.5.9), doParallel (>= 1.0.14), ggplot2
(>= 3.0.0), Matrix (>= 1.2-14), Rcpp (>= 0.12.18), RcppArmadillo (>= 0.8.600.0.0), reshape2 (>= 1.4.3), shallot (>= 0.4.5)

## Instructions for Use

### Reproducibility

What is to be reproduced (e.g., "All tables and figure from paper", "Tables 1-4”, etc.)

All tables and figures 1, 2, 3, 6, 7, 8, and 9.

How to reproduce analyses (e.g., workflow information, makefile, wrapper scripts)

Figures 1-3 can be replicated by running the “LSPproperties.R” file. Table 1 can be replicated by running the “compareproposals.R” file. Figures 6-9 and table 2 can be replicated by running the “simulationstudy.R” file.


## List of Files 

- `dmrpfunctions.cpp`

  This is an Rcpp file containing four sections of code. A description of each section along with its exported functions is provided below.

  **Section 1** contains core functions used in other parts of the file. 
  - `compsm`: compute pairwise similarity matrix given draws from a partition distribution

  **Section 2** contains functions to sample from and evaluate PMFs for the DP, LSP, LSPx, and block LSP models.
  - `rdp`: sample from the DP partition distribution
  - `rlsp`: sample from the LSP distribution
  - `rlspx`: sample from the LSPx distribution
  - `rblocklsp`: sample from the LSP distribution at given starting/ending point
  - `ddp`: evaluate PMF of the DP partition distribution
  - `dlsp`: evaluate PMF of the LSP distribution
  - `dlspx`: evaluate PMF of the LSPx distribution
  - `dblocklspx`: evaluate PMF of the LSP distribution at given starting/ending point

  **Section 3** contains functions to carry out a simulation study to compare LSP proposals with alternative proposal mechanisms.
  - `regll`: evaluates the log likelihood of a univariate regression model with a nonlinear mean function
  - `drawblocks`: draws block structure used for block LSP proposals
  - `reglsp`: MCMC sampler for regression model using LSP proposals
  - `regblocklsp`: MCMC sampler for regression model using block LSP proposals

  **Section 4** contains the MCMC samplers for an isolated demand model with a random partition and various partitioning priors.
  - `mvregll`: evaluates the log likelihood of a multivariate regression model
  - `mvregmcmc`: MCMC sampler for an unrestricted multivariate regression model
  - `isomvregdpmcmc`: MCMC sampler for an isolated demand model with a random partition and DP prior
  - `isomvreglspmcmc`: MCMC sampler for an isolated demand model with a random partition and LSP prior
  - `isomvreglspxmcmc`: MCMC sampler for an isolated demand model with a random partition and LSPx prior

- `LSPproperties.R`

  This is an R file that illustrates the properties of the LSP and LSPx models (figures 1 and 2). There is also code to compare the LSP distribution to the DP, ddCRP, and EPA partition distributions (figure 3).

- `compareproposals.R`
 
  This is an R file that compares the performance of MCMC algorithms using LSP and block LSP proposals with split-merge proposals and Gibbs proposals. Simulation studies are conducted for both small n (figure 6) and large n (figure 7).

- `simulationstudy.R`

  This is an R file that creates a simulated data set and then fits an unrestricted demand model and an isolated demand model (with both DP and LSP priors) to the data. There is code to check the recovery of all model parameters, plot posterior pairwise similarity matrices, and compute model fit statistics.

  Note: To get an idea of computation time, if a data set is generated with n=20, K=5, and T=100, then the isomvreglspmcmc sampler generates roughly 1,000 posterior draws per second. Computation time will increase as n increases, K decreases, or T increases. 

