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