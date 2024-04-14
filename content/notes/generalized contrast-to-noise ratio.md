---
title: The generalized contrast-to-noise ratio
aliases:
  - gCNR
---
The generalized contrast-to-noise ratio (gCNR) [1] is measure of contrast between two regions in an image that cannot be artificially improved by dynamic range transformations.

It is computed from the probability density function of pixel intensities in two regions $A$, and $B$ as 
$$
\text{gCNR} = 1-\int_{-\infty}^{\infty} \min(p_A(x), p_B(x)) dx,
$$
where $x$ is the pixel intensity. In practice the probability density functions are approximated by normalized histograms.

The figure below shows the how the gCNR measures the overlap between $p_A(x)$ and $p_B(x)$.
![[gcnr-overlap.png]]

## The problem with the regular contrast-to-noise ratio
The regular contrast-to-noise ratio is computed as
$$
\text{CNR} = \frac{|\mu_A-\mu_B|}{\sqrt{\sigma_A^2+\sigma_B^2}}.
$$
The problem with this metric is that it can be manipulated by a non-linear dynamic range transformation to artificially increase contrast. The figure below shows an image with two regions and the CNR value computed between the two before and after applying the S-curve in the middle.

We see that the CNR is significantly higher after the S-curve transformation, while the gCNR is unaffected.
![[gcnr-cnr-comparison.png]]

If we look at the probability density functions for the two regions after applying the S-curve we see that although $p_A(x)$, and $p_B(x)$ have changed a lot, the overlapping area has remained the same.
![[gcnr-scurve-overlap.png]]

The code used to generate these plots is available via this link:
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/vincentvdschaft/quartz-website/blob/v4/figure-generation/gcnr.ipynb)

[1] A. Rodriguez-Molares _et al._, “The Generalized Contrast-to-Noise Ratio: A Formal Definition for Lesion Detectability,” _IEEE Trans. Ultrason., Ferroelect., Freq. Contr._, vol. 67, no. 4, pp. 745–759, Apr. 2020, doi: [10.1109/TUFFC.2019.2956855](https://doi.org/10.1109/TUFFC.2019.2956855).