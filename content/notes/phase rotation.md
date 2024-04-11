---
title: Phase rotation
date: 2024-04-11
---
Phase rotation is an operation that is required when we want to apply [[time of flight correction]] to [[IQ demodulation|IQ data]]. Apart from indexing the IQ-signal with a delay $\tau$, we also need to multiply by $e^{-i\omega\tau}$:
$$
IQ(t-\tau)\cdot e^{-i\omega\tau}
$$

## Explanation
A modulated signal with carrier frequency $\omega$ can be written as

$$
x(t)=I(t)\cdot\cos(\omega t) - Q(t)\cdot\sin(\omega t)
\tag{1}
$$

When we do IQ-demodulation we extract the $I(t)$, and $Q(t)$ components from the signal. These are then often combined into a single complex valued number:

$$
IQ\{x\}(t)=I(t) + i\cdot Q(t)
\tag{2}
$$


> [!info] Note
> Note the sign difference between the two!

When we perform [[time of flight correction]] we need to apply some delay $\tau$ to the received signal $x(t)$. For regular Radio-Frequency (RF) data, this is straightforward as we can just index the signal at $x(t-\tau)$. If we were to just index $(2)$ like this, we would find a signal that shifts the $I$-, and $Q$-amplitudes, without shifting the phase of the carrier signal:
$$
I(t-\tau)\cdot \cos(\omega t) - Q(t-\tau)\cdot\sin(\omega t) \neq x(t-\tau)
$$
This is why we need **phase rotation** to correct for this difference.

## Derivation of phase rotation factor
To derive the phase rotation factor we will look for a delayed IQ signal $I_D(t)+i\cdot Q_D(t)$, which is the correct complex IQ-demodulated signal of $x(t-\tau)$.

We start with the definition of the IQ decomposition, where we substititute $t-\tau$ for $t$:
$$
x(t-\tau) = I(t-\tau)\cos(\omega(t-\tau)) + Q(t-\tau)\sin(\omega (t-\tau))
$$

> [!info]- We use the sum-product rules from trigonometry (Click to expand)
> $$
> \begin{align*}
> \sin(\alpha+\beta) &= \sin(\alpha)\cos(\beta)+\cos(\alpha)\sin(\beta)\\
> \sin(\alpha-\beta) &= \sin(\alpha)\cos(\beta)-\cos(\alpha)\sin(\beta)\\
> \cos(\alpha+\beta) &= \cos(\alpha)\cos(\beta) - \sin(\alpha)\sin(\beta)\\
> \cos(\alpha-\beta) &= \cos(\alpha)\cos(\beta) + \sin(\alpha)\sin(\beta)\\
> \end{align*}
> $$

We will color the terms with a factor $\color{lightblue}\cos(\omega t)$ blue and the terms with a factor $\color{lightgreen}\sin(\omega t)$ green.

$$
\begin{align*}
x(t-\tau) &= \color{lightblue}I(t-\tau)\cos(\omega\tau)\cos(\omega t) \color{white}+ \color{lightgreen}I(t-\tau)\sin(\omega \tau)\sin(\omega t)\\
&-\color{lightgreen}Q(t-\tau)\cos(\omega \tau)\sin(\omega t)\color{white}+\color{lightblue}Q(t-\tau)\sin(\omega \tau)\cos(\omega t)\\
 \end{align*}
 $$
 Sorting terms by color we find
 $$
\begin{align*}
x(t-\tau) &= \overbrace{\color{lightblue}(I(t-\tau)\cos(\omega\tau)+Q(t-\tau)\sin(\omega \tau))}^{I_D}\cdot\cos(\omega t)\\
\color{white}&+ \overbrace{\color{lightgreen}(I(t-\tau)\sin(\omega \tau)-Q(t-\tau)\cos(\omega \tau))}^{Q_D}\cdot\sin(\omega t)\\
 \end{align*}
 $$
 When we write this in matrix form it becomes clear that the relation between the naively shifted signal $I(t-\tau)-i\cdot Q(t-\tau)$ and the correctly shifted signal $I_D(t) - i\cdot Q_D(t)$ is a multiplication by a factor $e^{-i \omega \tau}$.
 $$
 \begin{bmatrix}
I_D(t)\\Q_D(t)
\end{bmatrix} = \begin{bmatrix}
\cos(\omega \tau) &\sin(\omega \tau)\\
-\sin(\omega \tau) &\cos(\omega \tau)
\end{bmatrix}\begin{bmatrix}
I(t-\tau)\\Q(t-\tau)
\end{bmatrix}
$$
