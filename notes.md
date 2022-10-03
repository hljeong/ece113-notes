# 9.26 1m
- [syllabus](tiny.cc/ucla113)

## ece102: signals & systems
- signals were modeled as functions of time
  - $x(t): t \in \mathbb R$ (continuous time)
  - $x: \mathbb R \to \mathbb R, \mathbb C$
  - sampling $t = n T_s$
    - $T_s$ = sampling interval
    - $n$ = integer
    - $t-x$ plot $\overset{\text{sampling}}{\longrightarrow}$ $n-x$ plot
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

# 9.28 1w

## sampling properties hold in discrete domain as well
- $\sum_{n = -\infty}^\infty x[n] \cdot \delta[n - k] = \sum_n x[k] \delta[n - k] = x[k] \sum_n \delta[n - k] = x[k]$

## systems
- unit step system $u[n] = \begin{cases}
  1 & n \geq 0 \\ 
  0 & n < 0
\end{cases}$
  - $u[n] - u[n - 1] = \delta[n]$
  - $\delta[n]$ is the first derivative of $u[n]$
  - ece102: $\delta(t) = \frac{d u(t)}{dt}$
  - $u[n] = \sum_{k = 0}^\infty \delta[n - k]$
- unit ramp signal $r[t] = \begin{cases}
  n & n \geq 0 \\ 
  0 & n < 0
\end{cases}$
  - 102: $r(t) = t u(t)$
  - $r[n] = n \cdot u[n] = \sum_{k = 1}^\infty u[n - k]$

## how wan se express $x[n]$ using basic signals?
- generic signal representation using the "canonical basis" of $\left \{ \delta[n - k] \forall \, k \right \}$
- $x[n] = \left \{ 1, 2, (0), 1, 1 \right \}$
- $x[n] = \delta[n + 2] + 2 \delta[n + 1] + \delta[n - 1] - \delta[n - 2]$

## sinusoidal signals
- $x(t) = A \cos(\omega_0 t + B)$, $\omega_0 = 2 \pi f_0$
- $x[n] = A \cos(\Omega_0 n + \theta)$, $\Omega_0 = 2 \pi F_0 \in [-\pi, \pi)$ where $F_0$ is the normalized frequency
- $x[n] A \cos(2 \pi f_0 n T_0 + \theta) = A \cos \left (2 \pi \frac{f_0}{f_s} n + \theta \right )$
- $F_n := \frac{f_0}{f_s} < 1$

## complex exponential
- $x[n] = A e^{j (2 \pi F_0 n + \theta)}$

## additional signal properties
1. duration of signal
2. real or complex
3. periodicity: a signal is periodic if $\exists \, N \in \mathbb Z: x[n + N] = x[n] \; \forall \, n$
  - $x[n]$ is also periodic with $2 N$, $3 N$, etc.
  - $x[n + k N] = x[n] \; \forall \, k, n$
  - fundamental period: smallestpositive $N$ such that $x[n + N] = x[n]$
  - e.g. $x[n] = \cos(2 \pi F_0 n) \rightarrow \exists \, k \in \mathbb Z: 2 \pi F_0 N = 2 \pi k \rightarrow F_0 N \in \mathbb Z, N = \frac{k}{F_0}$
  - is $x[n] = \cos(0.2 n)$ periodic?
    - no
    - $2 \pi F_0 = 0.2 \rightarrow \frac{k}{F_0} = 10 k \pi \not \in \mathbb Z$
