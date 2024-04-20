---
title: IQ demodulation
date: 2024-04-11
---
IQ demodulation is a method to decompose a signal that is modulated with a carrier frequency $\omega$ into a signal $I(t)$, that is in phase with the carrier $\cos(\omega t)$, and a signal $Q(t)$, that has a $90^\circ$ phase shift:
$$
x(t)=I(t)\cdot\cos(\omega t) - Q(t)\cdot\sin(\omega t)
\tag{1}
$$
## Complex representation
The in-phase, and quadrature components are often represented as a single complex number:
$$
IQ(t) = I(t) + i\cdot Q(t)
$$

> [!info] Note
> Note the sign difference between the two!

## Performing I/Q demodulation
The most common way to perform I/Q demodulation on sampled data with carrier frequency $\omega_c=2\pi f_c$ is as follows:
1. Compute the analytic signal using the Hilbert transform. The analytic signal is just the signal without the negative frequency components. This means that the analytic signal is complex-valued.
2. Shift the one-sided spectrum to baseband by multiplying with a signal $e^{-i2\pi f_c t}$.
3. Low-pass filter to remove noise from outside the bandwidth of the signal.
4. If we then want to perform envelope detection this is as simple as taking the magnitude of the complex valued I/Q signal.

The figure below shows the different stages of the process. The code used to generate this image can be viewed in Google Colab:
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/vincentvdschaft/quartz-website/blob/v4/figure-generation/demodulation.ipynb)

![[demodulation.png]]