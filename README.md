# How to implement the *MOXIE* algorithm to find toxicological mimicking interactions 
## Vishal Midya and Chris Gennings

This article presents a step-by-step guide and intuitions to implement the MOXIE algorithm, an amalgamation of the Weighted Quantile Sum regression (WQS) and Extreme Gradient Boosting (XGBoost). MOXIE is conducted in two stages to discover interactions associated with the outcome of interest. The first part of this algorithm uses an exposure mixture model (which, in this case, is the Weighted Quantile Sum regression (WQS) model). The WQS mixture model was used because of the apriori hypothesized directionality of the mixture association. Note that other exposure mixture analytical models, such as the Bayesian Kernel Machine Regression (BKMR) or Quantile g-computation method, can also be used when the directionality of the association between exposures and the outcome is not hypothesized beforehand, and interest lies in the overall mixture effect. See more technical details in Midya et al. <sup>1</sup>.

Assuming the main chemical mixture effect and the interactions are additive; we extracted the residuals (Pearson residuals in case of binary outcome) from this model. We treated the residual as the new outcome and used a machine learning-based prediction framework to discover non-linear combinations predictive of the outcome. The interactions are searched using the XGBoost algorithm by extracting its branches. A similar algorithm with WQS and a repeated hold-out signed-iterated Random Forest (rh-SiRF), has been explored in <sup>2,3</sup>.

As noted in Midya et al.<sup>1</sup>, this combination of exposure mixture algorithms can search for multi-ordered and non-linear interactions even when the number of chemical exposures is large. Further, since these interactions are based on thresholds, i.e., these interactions mimic the classical toxicological paradigm in which an interaction occurs only if the concentrations of certain chemicals are above some threshold. We will illustrate the use of this algorithm through simulated data. 

For detailed illustration, we included a CSV file containing the simulated data for 25 chemical exposures for 500 participants. It also contains four covariates and a continuous outcome. This fictitious dataset demonstrates how to use the WQS-SiRF algorithm. Please read the `WQS-SiRF-vignette.md` tab for further discussion. 


## Reference

1. Midya, V., & Gennings, C. (2023). Detecting Shape-based Interactions among Environmental Chemicals using an Ensemble of Exposure-Mixture Regression and Interpretable Machine Learning Tools.
2. Midya, V., Alcala, C. S., Rechtman, E., Gregory, J. K., Kannan, K., Hertz-Picciotto, I., ... & Valvi, D. (2023). Machine Learning Assisted Discovery of Interactions between Pesticides, Phthalates, Phenols, and Trace Elements in Child Neurodevelopment. Environmental Science & Technology.
3. Basu, S.; Kumbier, K.; Brown, J. B.; Yu, B. Iterative Random Forests to Discover Predictive and Stable High-Order Interactions. Proc. Natl. Acad. Sci. 2018, 115 (8), 1943–1948.


