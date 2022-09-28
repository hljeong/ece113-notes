# 9.26 1m
- [syllabus](tiny.cc/ucla113)

## ece102: signals & systems
- signals were modeled as functions of time
  - $x(t): t \in \mathbb R$ (continuous time)
  - $x: \mathbb R \to \mathbb R, \mathbb C$
  - sampling $t = n T_s$
    - $T_s$ = sampling interval
    - $n$ = integer
    - $t-x$ plot $\overset{sampling}{\longrightarrow}$ $n-x$ plot
    - $x(t)$ bandlimited ($|X(f)| \leq f_\text{max}$) then if sampling rate is $f_s > 2 f_\text{max}$ (nyquist rate) then it is possible to recover the original signal
    - sampling at lower rate then there will be aliasing
- sytems
  - $x(t) \rightarrow \boxed{S} \rightarrow y(t)$
  - $x[n] \rightarrow \boxed{S} \rightarrow y[n]$

## three ways tor write out signals
- mathematical expression
  - $x[n] = 3 \cos(2 n), n \in \mathbb Z$
- tabular list of significant samples
  - $x[n] = \left \{ -1, 8, 0, 5, -2 \right \}, n \in \mathbb Z$
    - underspecified signal: loss of indices
    - typically put an arrow underneath the 0 index
    - convention: any sample not listed has 0 amplitude
- plotting

## signal operations
- arithmetic
  - $g[n] = x[n] + A$
  - $g[n] = B x[n]$
  - signal addition: $g[n] = x_1[n] + x_2[n]$
  - signal multiplication: $g[n] = x_1[n] \cdot x_2[n]$
- time shifting
  - ece102
    - $x(t) \rightarrow x(t - \tau)$ delays signal by shifting it right
    - $x(t) \rightarrow x(t + \tau)$ advances signal by shifting left
  - ece113
    - $g[n] = x[n - k], k > 0$
- time scaling
  - ece102
    - $x(a t), a > 1$: contraction
    - $x(a t), 0 < a < 1$: dilation
  - ece113
    - $g[n] = x[2 n]$ (downsampling)
    - $g[n] = x\left [ \frac{1}{2} n \right ]$ (upsampling)
    - $g[n] = x[-n]$ (time reversal)

## basic signals
- $\delta(t)$ from ece102 $\rightarrow$ hard concept to grasp
- $\delta[t]$ from ece113 $\rightarrow$ : )
  - $\delta[n] = \begin{cases}
    1 & n = 0 \\ 
    0 & n \neq 0
  \end{cases}$
  - $\delta[n]$ does not have complexities of $\delta(t)$
- sampling property of $\delta$
  - $x[n] * \delta[n] = x[0] \cdot \delta[0] = x[0]$
  - $x[n] * \delta[n - k] = x[k] \cdot \delta[0] = x[k]$
