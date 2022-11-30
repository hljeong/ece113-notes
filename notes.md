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
- systems
  - $x(t) \rightarrow \boxed{S} \rightarrow y(t)$
  - $x[n] \rightarrow \boxed{S} \rightarrow y[n]$

## three ways to write out signals
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
- $x[n] = A \cos(2 \pi f_0 n T_0 + \theta) = A \cos \left (2 \pi \frac{f_0}{f_s} n + \theta \right )$
- $F_n := \frac{f_0}{f_s} < 1$

## complex exponential
- $x[n] = A e^{j (2 \pi F_0 n + \theta)}$

## additional signal properties
1. duration of signal
2. real or complex
3. periodicity: a signal is periodic if $\exists \, N \in \mathbb Z: x[n + N] = x[n] \; \forall \, n$
  - $x[n]$ is also periodic with $2 N$, $3 N$, etc.
  - $x[n + k N] = x[n] \; \forall \, k, n$
  - fundamental period: smallest positive $N$ such that $x[n + N] = x[n]$
  - e.g. $x[n] = \cos(2 \pi F_0 n) \rightarrow \exists \, k \in \mathbb Z: 2 \pi F_0 N = 2 \pi k \rightarrow F_0 N \in \mathbb Z, N = \frac{k}{F_0}$
  - is $x[n] = \cos(0.2 n)$ periodic?
    - no
    - $2 \pi F_0 = 0.2 \rightarrow \frac{k}{F_0} = 10 k \pi \not \in \mathbb Z$

# 10.3 2m

## recap
- recall: a signal is periodic if $x[n + N] = x[n]$ for all $n$ and some $N \in \mathbb Z$
- is $\cos(0.2 n)$ periodic?
  - no due to irrational period
- is the sum of $x_1$ and $x_2$ periodic if they are periodic signals?

## periodicity
- $x_1[n] = 2 \cos(0.4 \pi n), x_2[n] = 1.5 \cos(0.48 \pi n)$
- $F_1 = \frac{0.4 \pi}{2 \pi} = 0.2$
- $F_2 = \frac{0.48 \pi}{2 \pi} = 0.24$
- $N_1 = \frac{K_1}{F_1} = \frac{K_1}{0.2} = 5 K_1 = 5$
- $N_2 = \frac{K_2}{F_2} = \frac{K_2}{24 / 100} = \frac{100}{24} K_2 = \frac{25}{6} K_2 = 25$
- fact: sum of two periodic signals is itself a periodic signal
- $x_3[n] := x_1[n] + x_2[n]$ is periodic with period $N_1 N_2$
  - $x_3[n + N_1 N_2] = x_1[n + N_1 N_2] + x_2[n + N_1 N_2] = x_1[n] + x_2[n] = x_3[n]$
  - e.g. $N_1 = 5, N_2 = 25 \Rightarrow 2 \cos(0.4 \pi n) + 1.5 \cos(0.48 \pi n)$ has a period of $5 \cdot 25 = 125$
  - fundamental period: $\operatorname{lcm}(5, 25) = 25$
- e.g. $x[n]$ is periodic w $N = 12$
- are the following periodic
  - $y[n] = x[-n]$
    - yes: $y[n + 12] = x[-(n + 12)] = x[-n - 12] = y[n]$
  - $y[n] = x[n + 1]$
    - yes: $y[n + 12] = x[(n + 12) + 1] = x[n + 1] = y[n]$
  - $y[n] = x[3 n]$
    - yes: $y[n + 4] = x[3 (n + 4)] = x[3 n + 12] = x[3 n] = y[n]$
  - $y[n] = x^2[n]$
    - yes: $y[n + 12] = (x[n + 12])^2 = (x[n])^2 = y[n]$

## even and odd signals
- even: $x[n] = x[-n]$
- odd: $x[n] = -x[-n]$ or $-x[n] = x[-n]$
- any signal can be decomposed into odd and even components
  - $x[n] = x_\text{even}[n] + x_\text{odd}[n]$
- $x_\text{even}[n] = \frac{x[n] + x[-n]}{2}$
- $x_\text{odd}[n] = \frac{x[n] - x[-n]}{2}$

## complex signals
- $x[n] = x_R[n] + j x_I[n] = \left | x[n] \right | e^{j \angle x[n]}$
- $x^*[n] = x_R[n] - j x_I[n] = \left | x[n] \right | e^{-j \angle x[n]}$
- "even symmetry" for complex
  - $x[-n] = x^*[n]$
  - $x^*[-n] = x[n]$
- "odd antisymmetry" for complex
  - $x[-n] = -x^*[n]$
  - $x^*[-n] = -x[n]$

## decompose of even / odd for complex signals
- $x[n] = x_e[n] + x_o[n]$
- $x_e[n] = \frac{x[n] + x^*[-n]}{2}$
- $x_o[n] = \frac{x[n] - x^*[-n]}{2}$

## energy + power of a signal
- energy: $E_x = \sum_{n = -\infty}^\infty \left | x[n] \right |^2$
  - if $E_x < +\infty$: **finite energy signal**
  - e.g. $x[n] = \cos(2 \pi 0.1 n + 0.3 \pi)$ is not finite energy
- power
  - consider a periodic signal with period $N$
  - its power is expressed as $P_x = \frac{1}{N} \sum_{n = 0}^{N - 1} \left | x[n] \right |^2$
  - consider a non-periodic signal
  - its power is expressed as $P_x = \lim_{M \to \infty} \frac{1}{2 M + 1} \sum_{n = -M}^M \left | x[n] \right |^2$
- e.g. calculate the energy of $x[n] = (0.5)^n u[n]$
  - $E_x = \sum_{n = -\infty}^\infty \left | (0.5)^n u[n] \right |^2 = \sum_{n = -\infty}^\infty (0.5)^{2 n} u^2[n] = \sum_{n = 0}^\infty (0.5)^{2 n} = \frac{1}{1 - 0.25} = \frac{4}{3}$

## systems
- $x[n] \to \boxed{S} \to y[n]$
- properties
  - linearity
    - $y_1[n] = S\{x_1[n]\}$
    - $y_2[n] = S\{x_2[n]\}$
    - $x_3[n] = a x_1[n] + b x_2[n]$
    - $y_3[n] = S\{x_3[n]\}$
    - linear $\Rightarrow y_3[n] = a y_1[n] + b y_2[n]$
    - $S\left \{ \sum_{k = 1}^N a_k x_k[n] \right \} = \sum_{k = 1}^N a_k S\{x_k[n]\}$
  - time-invariance
    - $y[n] = S\{x[n]\}$
    - time invariance $\Rightarrow y[n - k] = S\{x[n - k]\}$
  - causality
    - if current output $y[n]$ depends only on the current and past input samples, the system is causal
    - e.g. $y[n] = x[n] - n x[n - 2]$: causal
    - e.g. $y[n] = (n + 1) x[n]$: causal (also memory-less)  
    - e.g. $y[n] = x[n] + x[n + 2]$: not causal
  - bounded input, bounded output (bibo) stability
    - if $\left | x[n] \right | < B$ for all $n$, then $\left | y[n] \right | < C$ for all $n$, $B, C$ are constants
    - e.g. $y[n] = 3 x[n] + 2 x[n - 1]$
      - suppose $\left | x[n] \right | < B$
      - stable: $\left | y[n] \right | = \left | 3 x[n] + 2 x[n - 1] \right | \leq 3 \left | x[n] \right | + 2 \left | x[n - 1] \right | < 5 B$
    - e.g. $y[n] = x^2[n]$
      - suppose $\left | x[n] \right | < B$
      - stable: $\left | y[n] \right | = \left | x^2[n] \right | = \left | x[n] \right |^2 < B^2$
    - e.g. $y[n] = n x[n - 1]$
      - not stable: as $n \to \infty$, $y \to \infty$
- e.g. $y[n] = 3 x[n] + 2 x[n - 1]$
  - time invariant: $x_1[n] = x[n - k] \Rightarrow y_1[n] = 3 x[n - k] + 2 x[n - k - 1] = y[n - k]$
- e.g. $y[n] = x^2[n]$
  - not linear
  - time invariant: $x_1[n] = x[n - k] \Rightarrow y_1[n] = x_1^2[n] = x^2[n - k] = y[n - k]$
- e.g. $y[n] = n x[n - 1]$
  - not time invariant: $x_1[n] = x[n - k] \Rightarrow y_1[n] = n x_1[n - 1] = n x[n - 1 - k] \neq (n - k) x[n - 1 - k] = y[n - k]$
- e.g. $y[n] = x[n / 4]$
  - linear
    - $y_1[n] = x_1[n / 4]$
    - $y_2[n] = x_2[n / 4]$
    - $x_3[n] = a x_1[n] + b x_2[n]$
    - $y_3[n / 4] = x_3[n / 4] = a x_1[n / 4] + b x_3[n / 4] = a y_1[n] + b y_2[n]$
  - not time invariant
  - not causal
    - $n = -4 \Rightarrow y[-4] = x[-1]$
  - stable
    - suppose $\left | x[n] \right | < B$
    - $\left | y[n] \right | = \left | x[n / 4] \right | < B$

# 10.5 2w

## hw q4
- suppose $x[n]$ periodic with period $N$, is the following periodic
- $y[n] = x[1 - 2 n]$
  - yes, $y[n + N] = x [1 - 2 n - 2 N] = x[1 - 2 n] = y[n]$
- $y[n] = x[n] + (-1)^n x[0]$
  - yes, $y[n + 2 N] = x[n + 2 N] + (-1)^{n + 2 N} x[0] = x[n] + (-1)^n x[0] = y[n]$
  - fundamental period: $\begin{cases}
    \operatorname{lcm}(N, 2) & x[0] \neq 0 \\ 
    N
  \end{cases}$

## constant coefficient difference equation
- $x[n] \to \boxed{S} \to y[n] = S\left \{ x[n] \right \}$
- $\sum_{k = 0}^M a_k y[n - k] = \sum_{k = 0}^N b_k x[n - k]$
- $a_0, \dots, a_M, b_0, \dots, b_N$: constant coefficients
- $M, N$: order of the equation
  - often, $\max\left \{ M, N \right \}$ to get the system order
- e.g. $y[n] = \frac{1}{N} \sum_{k = 0}^{N - 1} x[k]$
  - $a_0 = 1$
  - $b_0, \dots, b_{N - 1} = \frac{1}{N}$
  - order: $N - 1$
  - length $N$ moving average
- e.g. exponential smoother
  - $y[n] = (1 - \alpha) y[n - 1] + \alpha x[n]$
  - $0 < \alpha < 1$
  - $a_0 = 1, a_1 = \alpha - 1$
  - $M = 1$
  - $b_0 = \alpha$
  - $N = 0$
  - because $\left \{ a_1, \dots, a_M \right \} \neq \left \{ 0 \right \}$, this system is recursive, or, equivalently, has feedback
- if a system has feedback, then we need to know the *initial condition* of the system
  - initial condition is the time when input is applied
- e.g. $y[n] = y[n - 1] + x[n]$
  - suppose $x[n] = u[n] = \begin{cases}
    1 & n \geq 0 \\ 
    0 & n < 0
  \end{cases}$
  - $y[0] = y[-1] + x[0], y[-1] = y[-2] + x[-1], \dots$
  - initial condition: $y[-1] = 2$
  - $y[-1] = 2, y[0] = y[-1] + x[0] = 2 + 1 = 3, y[1] = y[0] + x[1] = 3 + 1 = 4, \dots$
  - $y[-1] = 3 \Rightarrow y[0] = 4, y[1] = 5, \dots$
- "relaxed system": a system is relaxed if $y[n] = 0$ for $n \to \infty$
- are relaxed systems described by a constant coefficient difference equation lti?

## visual method to look at ccds
- $\sum_{k = 0}^M a_k y[n - k] = \sum_{k = 0}^N b_k x[n - k]$
- e.g. delay element
  - "unit delay"

  ![](img/10.5.0.png)

- e.g. multiplier
  - constant multiplier

  ![](img/10.5.1.png)

- e.g. adder
  
  ![](img/10.5.2.png)

- e.g. branch

  ![](img/10.5.3.png)

- block diagram for $y[n] = 2 x[n] + 3 x[n - 1]$

  ![](img/10.5.4.png)

## impulse response
- $\delta[n] \to \boxed{S} \to h[n] := S\left \{ \delta[n] \right \}$
- recall: when a system is lti, then we have an expression for the output with respect to an arbitrary $x[n]$
- $x[n] = \sum_{k = -\infty}^\infty x[k] \delta[n - k]$
- $y[n] = S\left \{ x[n] \right \} = S\left \{ \sum_{-\infty}^\infty x[k] \delta[n - k] \right \} = \sum_{k = -\infty}^\infty S\left \{ \delta[n - k] \right \} = \sum_{-\infty}^\infty x[k] h[n - k] = x[n] * h[n]$

## convolution properties
- commutative: $x_1[n] * x_2[n] = x_2[n] * x_1[n]$
- distributive: $x[n] * (h_1[n] + h_2[n]) = x[n] * h_1[n] + x[n] * h_2[n]$
- associative: $x_1[n] * (x_2[n] * x_3[n]) = (x_1[n] * x_2[n]) * x_3[n]$
- identity: $x[n] * \delta[n] = x[n]$
  - $x[n] * \delta[n - m] = x[n - m]$
  
# 10.10 3m

## simple discrete-time convolution
- $h[n] = \left \{ (4)_{N_2 = 7}, 3, 2, 1 \right \}$
- $x[n] = \left \{ (-3)_{N_1 = 5}, 7, 4 \right \}$
- $y[n] = \sum_{k = -\infty}^\infty x[k] h[n - k]$
- what length will the output $y[n]$ be? where is the support?
  - $N_1 \leq k \leq N_1 + 2$
  - $N_2 \leq n - k \leq N_2 + 3$
  - $n - N_2 - 3 \leq k \leq n - N_2$
  - $y[n] = \sum_{k = K_1}^{K_2} x[k] h[n - k]$
  - $K_1 = \max \left \{ N_1, n - N_2 - 3 \right \} = \max \left \{ 5, n - 10 \right \}$
  - $K_2 = \min \left \{ N_1 + 2, n - N_2 \right \} = \min \left \{ 7, n - 7 \right \}$
  - $n - 10 \leq 7 \Rightarrow n \leq 17$
  - $n - 7 \geq 5 \Rightarrow n \geq 12$
  - support: $\left \{ 12, 13, 14, 15, 16, 17 \right \}$
- generalization
  - $x[n]$ starts at $N_1$ with length $L_x$
  - $h[n]$ starts at $N_2$ with length $L_h$
  - $K_1 = \max \left \{ N_1, n - N_2 - L_h \right \}$
  - $K_2 = \min \left \{ N_1 + L_x, n - N_2 \right \}$
  - $n - N_2 - L_h \leq N_1 + L_x \Rightarrow n \leq N_1 + N_2 + L_x + L_h$
  - $n - N_2 \geq N_1 \Rightarrow n \geq N_1 + N_2$
  - nonzero samples of convolution: $N_1 + N_2 \leq n \leq N_1 + N_2 + L_h + L_x$
  - number of nonzeros: $L_h + L_x + 1$

## graphical way of computing convolution
- $y[n] = \sum_{k = -\infty}^\infty x[k] h[n - k]$
- sketch $x[k]$
- sketch $h[-k]$
- sketch $h[n - k]$
- sample by sample multiplication of $x[k] \cdot h[n - k]$ for every $n$ that overlaps
- e.g.
  - $x[n] = u[n] - u[n - 7]$
  - $h[n] = (0.9)^n u[n]$
  - $y = x * h$
  - $y = 0$ when $n < N_1 + N_2 = 0$
  - $0 \leq n \leq 6$
    - $y[n] = \sum_{k = 0}^n x[k] \cdot h[n - k] = \sum_{k = 0}^n 1 \cdot (0.9)^{n - k} = (0.9)^n \sum_{k = 0}^n (0.9)^{-k} = (0.9)^n \frac{1 - (0.9)^{-(n + 1)}}{1 - (0.9)^{-1}}$
  - $n > 6$

## discrete time fourier series
- consider a discrete-time periodic signal
  - $x[n] = x[n + N]$
- infinite duration signal, which we represent as a vector of $N$ samples
- $x = \begin{bmatrix} x[0] \\ \vdots \\ x[N - 1] \end{bmatrix} \in \mathbb R^n, \mathbb C^n$
- key learning aims for 113
  - decompose a signal $x[n]$ into a set of "basis" signals
- $x[n] = \sum c_k \underbrace{y_k[n]}_\text{"basis"}$
  - $c_k \in \mathbb R, \mathbb C$ are scalar coefficients

## review: inner product
- $\left \langle x, y \right \rangle = \sum_{k = 0}^{N - 1} x[k] y[k]$ for $x, y \in \mathbb R^N$
  - "dot product"
- $\left \langle x, x \right \rangle = \sum_{k = 0}^{N - 1} x[k] \cdot x[k] = \sum_{k = 0}^{N - 1} x[k]^2 = \left | x \right |_2^2$
  - "squared norm"
- $\left | x \right |_2 = \sqrt{\left \langle x, x \right \rangle}$
  - "norm" of a vector

# 10.12 3w

## discrete time fourier series
- $x[n] = \sum_k c_k y_k[n]$
- $x = \sum_k c_k y_k$
- inner product: $\left \langle x, y \right \rangle = \sum_{k = 0}^{N - 1} x_k \cdot y_k$
- $\left \langle x, x \right \rangle = \sum_{k = 0}^{N - 1} x_k^2 = \left | x \right |_2^2$
- $\left | x \right |_2 = \sqrt{\left \langle x, x \right \rangle}$
- $\left \langle x, y \right \rangle = \left | x \right |_2 \left | y \right |_2 \cos \alpha$
- $\cos \alpha = \frac{\left \langle x, y \right \rangle}{\left | x \right |_2 \left | y \right |_2} = \frac{\left \langle x, y \right \rangle}{\left | x \right | \left | y \right |}$
- $\left \langle x, y \right \rangle = 0$ when $x$ and $y$ are orthogonal
- find a set $\left \{ y_k \right \}_k$ of basis vectors that are *orthonormal*
  - $\left \langle y_k, y_m \right \rangle = \begin{cases}
     0 & k \neq m \\ 
     1 & k = m
  \end{cases}$
  - e.g. $y_0 = \frac{1}{\sqrt 2} \begin{bmatrix} 1 \\ 1 \end{bmatrix}$ and $y_1 ql \frac{1}{\sqrt 2} \begin{bmatrix} 1 & -1 \end{bmatrix}$ are orthonormal
- synthesis: given a basis and coefficients, synthesize vectors
  - $c_0 = \sqrt 2, c_1 = \sqrt 2 \cdot 5$
  - $x = \sum c_k y_k = \begin{bmatrix} 6 \\ -4 \end{bmatrix}$
- analysis: given a basis and a signal $x$, what is the representation of $x$ in this basis?
  - find $c_0, c_1$ given $x, y_0, y_1$
  - $c_0 = \left \langle x, y_0 \right \rangle = \sum x[k] y_0[k]$
  - $c_1 = \left \langle x, y_1 \right \rangle = \sum x[k] y_1[k]$

## periodic signals
- suppose $\tilde x[n]$ is a periodic signal
- goal is to represent $\tilde x[n] = \sum_k \tilde c_k \phi_k[n]$
- $\phi_k[n] = e^{j \Omega_k n}$ fourier basis
- $\Omega_k$ is the angular frequency of the $k$-th basis vector
- $\tilde x[n] = \sum_k \tilde c_k e^{j \Omega_k n}$
- three open questions
  - what is $\Omega_k$?
  - how many basis signals / vectors are needed?
  - what are the coefficients $\tilde c_k$?

## what is $\Omega_k$
- suppose $\tilde x$ is periodic with period $N$
- what is the periodicity of $\phi_k$?
- $\phi_k$ has period $N$
- therefore $\phi_k[n] = \phi_k[n + N] \Rightarrow e^{j \Omega_k n} = e^{j \Omega_k (n + N)} = e^{j \Omega_k n} e^{j \Omega_k N}$
- $e^{j \Omega_k N} = 1$
- $\Omega_k N = 2 \pi k \Rightarrow \Omega_k = \frac{2 \pi}{N} \cdot k$
- $\phi_k(n) = e^{j \frac{2 \pi}{N} k n}$

## how many $\phi_k[n]$ are there
- suppose we have a finite set of $N$ basis vectors $\left \{ \phi_0, \dots, \phi_{N - 1} \right \}$
- is this sufficient?
- $\phi_{k + N}[n] = e^{j \frac{2 \pi}{N} (k + N) n} = e^{j \frac{2 \pi}{N} k n} e^{j 2 \pi n} = e^{j \frac{2 \pi}{N} k n} = \phi_k[n]$
- $\tilde x[n] = \sum_{k = 0}^{N - 1} \tilde c_k \phi_k[n]$
- find the basis vectors for $\tilde x[n] = \cos(0.2 \pi n)$
  - $\Omega_0 = 0.2 \pi$
  - $F_0 = \frac{0.2 \pi}{2 \pi} = 0.1$
  - $N = 10 \Rightarrow \left \{ \phi_0, \dots, \phi_9 \right \}$
  - $\tilde x[n] = \sum_{k = 0}^9 \tilde c_k e^{j 0.2 \pi k n}$
- how to compute $\tilde c_k$
$$
  \begin{aligned}
    \left \langle \tilde x[n], e^{j \frac{2 \pi}{N} k n} \right \rangle &= \sum_{n = 0}^{N - 1} \tilde x[n] e^{-j \frac{2 \pi}{N} k n} & \\ 
    &= \sum_{n = 0}^{N - 1} \sum_{m = 0}^{N - 1} \tilde c_m e^{j \frac{2 \pi}{N} m n} e^{-j \frac{2 \pi}{N} k n} & \\ 
    &= \sum_{n = 0}^{N - 1} \sum_{m = 0}^{N - 1} \tilde c_m e^{j \frac{2 \pi}{N} (m - k) n} & \\ 
    &= \tilde c_k N &
  \end{aligned}
$$
$$
  \tilde c_k = \frac{1}{N} \sum_{n = 0}^{N - 1} \tilde x[n] e^{-j \frac{2 \pi}{N} k n}
$$

## discrete time fourier series (dtfs) summary
- synthesis equation: $\tilde x[n] = \sum_{k = 0}^{N - 1} \tilde c_k e^{j \frac{2 \pi}{N} k n}$
- analysis equation: 
$\tilde c_k = \frac{1}{N} \sum_{n = 0}^{N - 1} \tilde x[n] e^{-j \frac{2 \pi}{N} k n}$

# 10.19 4w

## discrete time fourier series (dtfs)
- $\tilde x[n] = \tilde x[n + N] = \tilde x[n + k N]$
- $\tilde x[n] = \sum_{k = 0}^{N - 1} \tilde c_k e^{j \frac{2 \pi}{N} k n}$
- $\tilde c_k = \left \langle \tilde x[n], \frac{1}{N} e^{j \frac{2 \pi}{N} k n} \right \rangle$
- $\left \langle x[n], y[n] \right \rangle := \sum_{n = 0}^{N - 1} x[n] y^*[n]$
- $\tilde c_k = \frac{1}{N} \sum_{n = 0}^{N - 1} \tilde x[n] e^{-j \frac{2 \pi}{N} k n}$
- side note: pulse train signal
  - $\tilde x[n] = \begin{cases}
    1 & -L \leq n \leq L \\ 
    0 & L < n < N - L
  \end{cases}$
  - periodic with $N$
  - homework or exam: calculate dtfs $\tilde x[n] = \sum_{n = 0}^{N - 1} \tilde c_k e^{j \frac{2 \pi}{N} k n}$

## properties of dtfs
- periodicity: coefficients are perioddic with $N$
  - $\tilde c_k = \tilde c_{k + r N}, r \in \mathbb Z$
- linearity
  - $\tilde x_1[n]$, $\tilde x_2[n]$ periodic with same period $N$
  - $\tilde x_1[n] \overset{\text{dtfs}}{\longrightarrow} \tilde c_k$
  - $\tilde x_2[n] \overset{\text{dtfs}}{\longrightarrow} \tilde d_k$
  - $\alpha \tilde x_1[n] + \beta \tilde x_2[n] \overset{\text{dtfs}}{\longrightarrow} \alpha \tilde c_k + \beta \tilde d_k$
  - proof
    - $\tilde x_1[n] = \sum_{n = 0}^{N - 1} \tilde c_k e^{j \frac{2 \pi}{N} k n}$
    - $\tilde x_2[n] = \sum_{n = 0}^{N - 1} \tilde c_k e^{j \frac{2 \pi}{N} k n}$
    - $\alpha \tilde x_1[n] + \beta \tilde x_2[n] = \sum_{n = 0}^{N - 1} (\alpha \tilde c_k + \beta \tilde d_k) e^{j \frac{2 \pi}{N} k n}$
- if $x[n]$ is real-valued, then the dtfs $\tilde c_k$ for a signal is a conjugate symmetric sequence
  - $\tilde c_k^* = \tilde c_{-k}$
  - $\left | \tilde c_k \right | = \left | \tilde c_{-k} \right |$
  - proof
    - $\tilde x[n] = \tilde x^*[n]$
    - $\tilde c_k^* = \left ( \frac{1}{N} \sum_{n = 0}^{N - 1} \tilde x[n] e^{-j \frac{2 \pi}{N} k n} \right )^* = \frac{1}{N} \sum_{k = 0}^{N - 1} \tilde x[n] e^{j \frac{2 \pi}{N} k n} = \tilde c_{-k}$
  - $\tilde c_k = \left | \tilde c_k \right | e^{j \angle \tilde c_k}$
- dtfs of even and odd signals
  - $\tilde x[n]$ is real and even $\Rightarrow$ then $\tilde x^*[n] = \tilde x[n]$ and $\tilde x[n] = \tilde x[-n]$
  - $\tilde c_{-k} = \frac{1}{N} \sum_{n = 0}^{N - 1} \tilde x[n] e^{-j \frac{2 \pi}{N} k n} = \frac{1}{N} \sum_{n' = 0}^{-(N - 1)} \tilde x[-n'] e^{-j \frac{2 \pi}{N} k n'} = \frac{1}{N} \sum_{n' = 0}^{-(N - 1)} \tilde x[n'] e^{-j \frac{2 \pi}{N} k n'} = \tilde c_k$
  - $\tilde c_k^* = \tilde c_{-k}$ real signal
  - $\tilde c_k = \tilde c_{-k}$ even signal
  - real even signal $\rightarrow$ real dtfs
- shifting in time
  - $\tilde x[n] \to \tilde c_k$
  - $\tilde x[n - m] \to e^{-j \frac{2 \pi}{N} k m} \tilde c_k$
  - proof
    - $\tilde y[n] = \tilde x[n - m]$
    - $\tilde y[n] = \sum_{k = 0}^{N - 1} \tilde d_k e^{j \frac{2 \pi}{N} k n}$
    - $\tilde d_k = \frac{1}{N} \sum_{n = 0}^{N - 1} \tilde y[n] e^{-j \frac{2 \pi}{N} k n} = \frac{1}{N} \sum_{n = 0}^{N - 1} \tilde x[n - m] e^{-j \frac{2 \pi}{N} k n} = \frac{1}{N} \sum_{n' = -m}^{N - 1 - m} \tilde x[n'] e^{-j \frac{2 \pi}{N} k (n' + m)}$
      - $= e^{-j \frac{2 \pi}{N} k m} \frac{1}{N} \sum_{n' = -m}^{N - 1 - m} \tilde x[n] e^{-j \frac{2 \pi}{N} k n'} = e^{-j \frac{2 \pi}{N} k m} \tilde c_k$

# 10.24 5m

## periodic convolution
- $\tilde x[n]$ with period $N$
- $\tilde h[n]$ with period $N$
- $\tilde x[n] \otimes \tilde h[n] = \sum_{k = 0}^{N - 1} \tilde x[k] \tilde h[n - k]$
- "linear convolution"
  - $\tilde x[n] * \tilde h[n] = \sum_{k = -\infty}^\infty \tilde x[k] \tilde h[n - k] \neq \tilde x[n] \otimes \tilde h[n]$
- finding $\tilde y[n] = \tilde x[n] \otimes \tilde h[n]$
  - $\tilde x[n] = \left \{ \dots, 0, 1, 2, 3, 4, \dots \right \}, 0 \leq n \leq 4$
  - $\tilde h[n] = \left \{ \dots, 3, 3, -3, 2, -1, \dots \right \}, 0 \leq n \leq 4$
  - $\tilde y[n] = \tilde x[n] \otimes \tilde h[n] = \sum_{k = 0}^4 \tilde x[k] \tilde h[n - k]$
  - $\tilde y[0] = \sum_{k = 0}^4 \tilde x[k] \tilde h[0 - k] = \tilde x[0] \tilde y[0] + \tilde x[1] \tilde y[-1] + \cdots$
    - $\tilde h[k] = \tilde h[N + k]$
- $\tilde y \overset{\text{dtfs}}{\longrightarrow} \tilde e_k$
- $\tilde x \overset{\text{dtfs}}{\longrightarrow} \tilde c_k$
- $\tilde h \overset{\text{dtfs}}{\longrightarrow} \tilde d_k$
- proposition: $\tilde e_k = N \cdot \tilde c_k \cdot \tilde d_k$
  - proof
    - $\tilde y[n] = \sum_{k = 0}^{N - 1} \tilde x[k] \tilde h[n - k] = \sum_{k = 0}^{N - 1} \tilde e_k e^{j \frac{2 \pi}{N} k n}$
    - $\tilde e_k = \frac{1}{N} \sum_{n = 0}^{N - 1} \left ( \sum_{m = 0}^{N - 1} \tilde x[m] \tilde h[n - m] \right ) e^{-j \frac{2 \pi}{N} k n} = \frac{1}{N} \sum_{m = 0}^{N - 1} \tilde x[m] \sum_{n = 0}^{N - 1} \tilde h[n - m] e^{-j \frac{2 \pi}{N} k n}$
    - $= \frac{1}{N} \sum_{m = 0}^{N - 1} \tilde x[m] \tilde d_k \cdot N \cdot e^{-j \frac{2 \pi}{N} k m} = \sum_{m = 0}^{N - 1} \tilde x[m] \tilde d_k e^{-j \frac{2 \pi}{N} k m} = \tilde d_k \sum_{m = 0}^{N - 1} \tilde x[m] e^{-j \frac{2 \pi}{N} k m} = \tilde d_k \tilde c_k N$

## discrete time fourier transform (dtft)
- consider a non-periodic signal $x[n]$ with finite length
  - $x[n] \neq 0$ for $\left | n \right | \leq M$ 
  - there exists $2 M + 1$ non-zero samples
- create a periodic extension of $x$
  - $\tilde x[n] = \sum_{k = -\infty}^\infty x[n + k(2 M + 1)]$
- $\tilde x[n]$ is periodic so can be analyzed using dtfs
  - $\tilde x[n] = \sum_{k = -M}^M \tilde c_k e^{j \frac{2 \pi}{2 M + 1} k n}$(synthesis)
- since $\tilde x[n]$ is periodic there exists an analysis component as well
  - $\tilde c_k = \frac{1}{2 M + 1} \sum_{n = -M}^M \tilde x[n] e^{-j \frac{2 \pi}{2 M + 1} k n}$
  - $\Omega_0 = \frac{2 \pi}{2 M + 1}$
  - $\Omega_k = k \Omega_0$
  - $k \in [-M, M]$
  - $\Omega_k \in [-\pi, \pi]$
  - $\tilde c_k = \frac{1}{2 M + 1} \sum_{n = -M}^M x[n] e^{-j \frac{2 \pi}{2 M + 1} k n}$
  - $(2 M + 1) \tilde c_k = \sum_{n = -M}^M x[n] e^{-j \frac{2 \pi}{2 M + 1} k n}$
- as $M \to \infty$
  - $\Omega_0 \to \Delta \Omega$
  - $k \Omega = k \frac{2 \pi}{2 M + 1} := \Omega \in \mathbb R$
  - $\Omega \in [-\pi, \pi]$
  - $\lim_{M \to \infty} (2 M + 1) \tilde c_k := X(\Omega) = \sum_{n = -\infty}^\infty x[n] e^{-j \Omega n}$ (dtft)
- $X(\Omega)$ is complex
- $X(\Omega) = \Re\left \{ X(\Omega) \right \} + j \Im\left \{ X(\Omega) \right \}$
- $X(\Omega) = \left | X(\Omega) \right | e^{j \angle X(\Omega)}$
- visualizing $X(\Omega)$ requires two plots
- ece102: 
  - $x(t) \overset{\mathcal F}{\longrightarrow} X(j \omega) = \frac{1}{2 \pi} \int_{-\infty}^\infty x(t) e^{-j \omega t}\ dt$, $\omega \in (-\infty, \infty)$
- ece113: 
  - $x[n] \overset{\mathcal F}{\longrightarrow} X(\Omega) := \sum_{n = -\infty}^\infty x[n] e^{-j \Omega n}$, $\Omega \in [-\pi, \pi]$
$X(\Omega)$ is periodic with $2 \pi$
- $\begin{aligned}[t]
    X(\Omega + 2 \pi) &= \sum_{n = -\infty}^\infty x[n] e^{-j (\Omega + 2 \pi) n} \\ 
    &= \sum_{n = -\infty}^\infty x[n] e^{-j \Omega n} e^{-j 2 \pi n} \\ 
    &= \sum_{n = -\infty}^\infty x[n] e^{-j \Omega n} = X(\Omega)
  \end{aligned}$
- $X(\Omega) \overset{\mathcal F^{-1}}{\longrightarrow} x[n]$
  - $x[n] = \lim_{M \to \infty} \tilde x[n] = \lim_{M \to \infty} \sum_{k = -M}^M \tilde c_k e^{j \frac{2 \pi}{2 M + 1} k n}$
  - $\lim_{M \to \infty} \sum_{k = -M}^M c_k \frac{2 M + 1}{2 \pi} \Delta \Omega e^{j \Omega n}$
  - $x[n] = \frac{1}{2 \pi} \int_{-\pi}^\pi X(\Omega) e^{j \Omega n}\ d\Omega$ (idtft)
- $\delta[n] \overset{\mathcal F}{\longrightarrow} \sum_{n = -\infty}^\infty d[n] e^{-j \Omega n} = e^{-j \Omega 0} = 1$
- $x[n] = \delta[n - n_0]$
  - $X(\Omega) = \sum_{n = -\infty}^\infty = \sum_{n = -\infty}^\infty \delta[n - n_0] e^{-j \Omega n} = e^{-j \Omega n_0}$
- $x[n] = a^n u[n]$, $\left | a \right | < 1$
  - existence of dtft
    - $x[n]$ has to be absolutely summable
      - $\sum_{n = -\infty}^\infty \left | x[n] \right | < +\infty$
    - or square summable
      - $\sum_{n = -\infty}^\infty \left | x[n] \right |^2$
  - $\begin{aligned}[t]
      X(\Omega) &= \sum_{n = -\infty}^\infty a^n u[n] e^{-j \Omega n} \\ 
      &= \sum_{n = 0}^\infty a^n e^{-j \Omega n} \\ 
      &= \sum_{n = 0}^\infty (a e^{-j \Omega})^n \\ 
      &= \frac{1}{1 - a e^{-j \Omega}}
    \end{aligned}$

# 10.26 5w

## dtft
- analysis equation: $X(\Omega) = \sum_{n = -\infty}^\infty x[n] e^{-j \Omega n}$ (continuous)
  - $\Omega \in [-\pi, \pi]$
- synthesis equation (idtft): $x[n] = \frac{1}{2 \pi} \int_{-\pi}^\pi X(\Omega) e^{j \Omega n}\ d\Omega$
- $x[n] = \begin{cases}
    1 & -L \leq n \leq L \\
    0 & \text{otherwise}
  \end{cases}$
  - $\begin{aligned}[t]
      X(\Omega) &= \sum_{n = -\infty}^\infty x[n] e^{-j \Omega n} \\ 
      &= \sum_{n = -L}^L e^{-j \Omega n} \\ 
      &= \frac{e^{j \Omega L} - e^{-j \Omega (L + 1)}}{1 - e^{-j \Omega}} \\ 
      &= \frac{e^{-j \Omega / 2} (e^{j \Omega (L + 1 / 2)} - e^{-j \Omega (L + 1 / 2)})}{e^{-j \Omega / 2} (e^{j \Omega / 2} - e^{-j \Omega / 2})} \\ 
      &= \frac{\sin(\Omega (L + 1 / 2))}{\sin(\Omega / 2)}
    \end{aligned}$
- $X(\Omega) = \begin{cases}
    1 & -\Omega_c < \Omega < \Omega_c \\ 
    0 & \text{otherwise}
  \end{cases}$
  - $\begin{aligned}[t]
      x[n] &= \frac{1}{2 \pi} \int_{-\Omega_c}^{\Omega_c} 1 \cdot e^{j \Omega n}\ d\Omega \\ 
      &= \frac{1}{2 \pi} \left ( \frac{1}{j \Omega} e^{j \Omega n} \right ) \Big |_{-\Omega_c}^{\Omega_c} \\ 
      &= \frac{1}{\pi} \cdot \frac{1}{n} \left ( \frac{e^{j \Omega_c n} - e^{-j \Omega_c n}}{2 j} \right ) \\ 
      &= \frac{1}{\pi n} \sin(\Omega_c n) \\ 
      &= \frac{\Omega_c}{\pi} \operatorname{sinc}(\Omega_c n)
    \end{aligned}$

# 11.7 7m

## dtft $\to$ dft
- periodic signal: dtfs, coefficients are discrete
- non-periodic signal: dtftc, continuous transform domain
- discrete-time signal $x[n] \overset{\text{dtft}}{\longrightarrow} X(\Omega) = \sum_{n = -\infty}^\infty x[n] e^{-j \Omega n}$
  - $\Omega \in \mathbb R$
  - $X(\Omega) = X(\Omega + 2 \pi)$
  - problem: $\Omega$ is continuous
- non-periodic signal with finite duration (length $N$)
  - $x[n]$ given for $n = 0, \dots, N - 1$
  - $x[n] = 0$ for $n < 0$ and $n \geq N$
- first goal: find the periodic extension of $x[m]$
  - $\tilde x[n] = \sum_{m = -\infty}^\infty x[n - m N]$
  - $\tilde x[n] \overset{\text{dtfs}}{\longrightarrow} \tilde c_k$
  - $\tilde c_k := \frac{1}{N} \sum_{n = 0}^{N - 1} \tilde x[n] e^{-j \frac{2 \pi}{N} k n}$
- second goal: extract one period of $\tilde c_k$; in particular, $c_k$ is periodic with $N$
  - $\tilde x[n] = \sum_{k = 0}^{N - 1} \tilde c_k e^{j \frac{2 \pi}{N} k n}$
- define $x[n] = \sum_{k = 0}^{N - 1} c_k e^{j \frac{2 \pi}{N} k n}$ where $c_k = \begin{cases}
    \tilde c_k & k = 0, \dots, N - 1 \\ 
    0 & \text{otherwise}
  \end{cases}$
- rename $c_k N := X[k]$ for $k = 0, \dots, N - 1$
  - dft: $x[n] = \frac{1}{N} \sum_{k = 0}^{N - 1} X[k] e^{j \frac{2 \pi}{N} k n}$
  - inverse dft: $X[k] = \sum_{n = 0}^{N - 1} x[n] e^{-j \frac{2 \pi}{N} k n}$
- $N$ samples map to $N$ coefficients

## dft as a sampling of the dtft
- dtft: $X(\Omega) = \sum_{n = -\infty}^\infty x[n] e^{-j \Omega n} = \sum_{n = 0}^{N - 1} x[n] e^{-j \Omega n}$
- dft: $X[k] = X(\Omega) \Big |_{\Omega = \frac{2 \pi}{N} k}$

## dft in linear algebraic view
- $\mathbf x = \left [ x[0], x[1], \dots, x[N - 1] \right ]$
- $\mathbf X = \left [ X[0], X[1], \dots, X[N - 1] \right ]$
- $\mathbf X = W \mathbf x$
  - $X[k] = \sum_{n = 0}^{N - 1} x[n] e^{-j \frac{2 \pi}{N} k n}$
  - $\omega_N := e^{-j \frac{2 \pi}{N}}$
  - dft: $X[k] = \sum_{n = 0}^{N - 1} x[n] \omega_N^{k n}$
  - idft: $x[n] = \frac{1}{N} \sum_{k = 0}^{N - 1} X[k] \omega_N^{-k n}$
- $W = \begin{bmatrix}
    1 & 1 & \cdots & 1 \\ 
    1 & \omega_N^1 & \cdots & \omega_N^{N - 1} \\ 
    \vdots & \vdots & \ddots & \vdots \\ 
    1 & \omega_N^{N - 1} & \cdots & \omega_N^{(N - 1)^2}
  \end{bmatrix}$
- $\mathbf x = W^{-1} \mathbf x$ 
- $W^{-1} = \frac{1}{N} \overline{W}$

## from a basis perspective
- $\mathbf x = W^{-1} \mathbf X = \frac{1}{N} \sum X[i] W^{-1}[:, i]$

## example
- $x[n] = u[n] - u[n - 10]$
- $X[k] = \sum_{n = 0}^9 e^{-j \frac{2 \pi}{10} k n} = \frac{1 - e^{-j \frac{2 \pi}{10} k \cdot 10}}{1 - e^{-j \frac{2 \pi}{10} k}} = \frac{1 - e^{-j 2 \pi k}}{1 - e^{-j \frac{2 \pi}{10} k}}$
- $X[0] = \lim_{k \to 0} \frac{1 - e^{-j 2 \pi k}}{1 - e^{-j \frac{2 \pi}{10} k}} = 10$
- $X[\geq 1] = 0$
- dtft has waves: $\frac{\sin(5 \Omega)}{\sin(0.5 \Omega)} e^{-j 4.5 \Omega}$

# 11.9 7w

## dft review
- $x[n]$ length $N$ signal
- $x[n] = 0$ for $n < 0, n \geq N$
- $x[n] \overset{\text{dft}}{\longrightarrow} X[k]$
- we arrived at the dft through the following steps
  - $x[\text{$N$ samples}] \to \text{periodic extension} \to$
  - $\tilde x[n] \to dtfs \to$
  - $\tilde c_k \to X[k] := N \cdot c_k, k = 0, 1, \dots, N - 1$
  - dft: $X[k] = \sum_{n = 0}^{N - 1} x[n] e^{-j \frac{2 \pi}{N} k n}$
  - idft: $x[n] = \frac{1}{N} \sum_{k = 0}^{n - 1} X[k] e^{j \frac{2 \pi}{N} k n}$
- dft is practical, dtft is idealized
- recall dtft $x[n] \overset{\text{dtft}}{\longrightarrow} X(\Omega), \Omega \in \mathbb R$
- relationship between dft and dtft: $X[k] = X(\Omega) \Big |_{\Omega = \frac{2 \pi}{N} k}$
- e.g.:
  - $u[n] - u[n - 10]$
  - dtft looks like $\operatorname{sinc}$
  - dft has 10 at $n = 0$ and 0 everywhere else = lossy

## sample spacing puzzle
- zero padding
- $x[n] \to g[n] = \begin{cases}
    x[n] & n \in [0, N - 1] \\ 
    0 & n \in [N, N + M - 1]
  \end{cases}$
- $G[k] = X(\Omega) \Big |_{\Omega = \frac{2 \pi}{N + M} k}$

## dft properties
- $x[n] \to X[k]$
- time shifting property
  - $x[n - m] \to e^{-j \omega k m} X[k]$
    - wrong because sampling window doesnt change
    - solution: cyclic shift, periodic extension
  - $g[n] = x[(n - m)\ \mathrm{mod}\ N]$
  - $x[(n - m)\ \mathrm{mod}\ N] \to e^{-j \omega k m} X[k]$
    - where $\omega = \frac{2 \pi}{N}$
- linearity
  - $x_1[n] \to X_1[k]$
  - $x_2[n] \to X_2[k]$
  - $\alpha x_1[n] + \beta x_2[n] \to \alpha X_1[k] + \beta X_2[k]$

## determine the dtft
- $x[n] = (0.7)^n \cos(0.2 \pi n) u[n]$
  - $x_1[n] = (0.7)^n u[n] \to X_1(\Omega) = \frac{1}{1 - 0.7 e^{-j \Omega}}$
  - $\begin{aligned}[t]
      X(\Omega) &= \operatorname{DTFT}(\cos(0.2 \pi n) x_1[n]) \\ 
      &= \left ( \frac{1}{2} e^{j 0.2 \pi n} + \frac{1}{2} e^{-j 0.2 \pi n} \right ) x_1[n] \\ 
      &= \frac{1}{2} e^{j 0.2 \pi n} x_1[n] + \frac{1}{2} e^{-j 0.2 \pi n} x_1[n] \\ 
      &= \frac{1}{2} X_1(\Omega - 0.2 \pi) + \frac{1}{2} X_1(\Omega + 0.2 \pi) \\ 
      &= \frac{1}{2} \cdot \frac{1}{1 - 0.7 e^{-j (\Omega - 0.2 \pi)}} + \frac{1}{2} \cdot \frac{1}{1 - 0.7 e^{-j (\Omega + 0.2 \pi)}}
    \end{aligned}$
- $x[n] = n x[n - 1]$
  - time shift: $x[n - 1] \to e^{-j \Omega \cdot 1} X(\Omega)$
  - differentiation in freq: $n x[n - 1] \to j \frac{d}{d\Omega} \left [ e^{-j \Omega} X(\Omega) \right ]$
- $x_2[n] = e^{j \frac{\pi \Omega}{2}} \left ( x[n] * x[n] \right )$

# 11.14 8m

## dft conv thm
- conv thm for dtft
  - $x[n] \to h[n] \to y[n] = x[n] * h[n]$
  - $\overset{\text{dtft}}{\leftrightarrow} X(\Omega) \to H(\Omega) \to Y(\Omega) = X(\Omega) H(\Omega), \Omega \in \mathbb R$
- in practice, we compute dft, so does the property hold?
  - $X[k] = \operatorname{DFT}(x[n]), k = 0, 1, \dots, N_x - 1$
  - $H[k] = \operatorname{DFT}(h[n]), k = 0, 1, \dots, N_h - 1$
  - $Y[k] = \operatorname{DFT}(y[n]), k = 0, 1, \dots, N_{y - 1}$
- $X[k] \cdot H[k] \overset{\text{?}}{=} Y[k]$
  - $N_y = N_x + N_h - 1$
  - no
- try to derive an analog of conv thm
  - recall that we got dft from "periodic" extension of a finite signal
  - assumption: $x[n], h[n]$ both have length $N$
  - $x[n] \to \tilde x[n] \overset{\text{dtfs}}{\longrightarrow} \tilde c_k \to c_k \mid X(k) := c_k \cdot N$
  - $h[n] \to \tilde h[n] \overset{\text{dtfs}}{\longrightarrow} \tilde d_k \to d_k \mid H(k) := d_k \cdot N$
- periodic convolution
  - $\tilde y[n] = \tilde x[n] \otimes \tilde h[n] = \sum_{k = 0}^{N - 1} \tilde x[k] \tilde h[n - k]$
  - $\tilde y[n] \overset{\text{dtfs}}{\longrightarrow} \tilde e_k$
  - recall $\tilde e_k = N \tilde c_k \tilde d_k$ proven in an earlier lecture
  - taking $N$ samples of $\tilde y[n]$ such that $y[n] = \tilde y[n], n = 0, 1, \dots, N - 1$
  - $y[n] = \tilde y[n] = \sum_{n = 0}^{N - 1} \tilde x[k] \tilde h[n - k], n = 0, 1, \dots, N - 1$
  - $y[n] = \sum_{n = 0}^{N - 1} x[k] \tilde h[n - k], n = 0, 1, \dots, N - 1$
  - $y[n] = \sum_{k = 0}^{N - 1} x[k] h[(n - k)\ \mathrm{mod}\ N]$
  - circular convolution: applies to two finite duration signals of length $N$
  - $y[n] = x[n] \circ h[n]$
- example
  - $x[n] = \left \{ 1, 2, 3, -4, 6 \right \}$
  - $h[n] = \left \{ 5, 4, 3, 2, 1 \right \}$
  - $y[0] = \sum_{k = 0}^{N - 1} x[k] h[(-k)\ \mathrm{mod}\ N] = 5 \cdot 1 + 2 \cdot 1 + 3 \cdot 2 + (-4) \cdot 3 + 6 \cdot 4 = 25$
- $y[n] = \sum_{k = 0}^{N - 1} x[k] h[(n - k)\ \mathrm{mod}\ N]$
- $\overset{\text{$N$-point DFT}}{\longrightarrow} Y[k] = X[k] H[k]$
- $y[n] = \operatorname{IDFT}(Y[k]) = \operatorname{IDFT}(X[k] \cdot H[k])$
- recall: $\tilde e_k = N \tilde d_k \tilde c_k$
  - $y[n] = \tilde y[n] \to \tilde e_k, n = 0, \dots, N - 1$
  - $x[n] = \tilde x[n] \to \tilde c_k, n = 0, \dots, N - 1$
  - $h[n] = \tilde h[n] \to \tilde d_k, n = 0, \dots, N - 1$
  - $\tilde e_k = N \tilde c_k \tilde d_k \forall \, k$
  - dft relationship: 
    - $X[k] = N c_k$
    - $H[k] = N d_k$
    - $Y[k] = N e_k$
    - $c_k = \frac{X[k]}{N}$
    - $d_k = \frac{H[k]}{N}$
    - $e_k = \frac{Y[k]}{N}$
- generalize this insight to not same length sequences
  - $y_l[n] = x[n] * h[n]$
  - $x[n]$ length $N_x$
  - $h[n]$ length $N_h$
  - $y_l[n]$ length $N_y = N_x + N_h - 1$
  - trick: zero pad $x$ and $h$ to have the same length
  - $x_p[n] = \begin{cases}
      x[n] & n = 0, \dots, N_x - 1 \\ 
      0 & n = N_x, \dots, N_y - 1
    \end{cases}$
  - $h_p[n] = \begin{cases}
      h[n] & n = 0, \dots, N_h - 1 \\ 
      0 & n = N_h, \dots, N_y - 1
    \end{cases}$
  - $y^c[n] = x_p[n] \circ h_p[n] = \sum_{k = 0}^{N_y - 1} x_p[k] h_p[(n - k)\ \mathrm{mod}\ N_y]$
  - $y_l[n] = \sum_{k = 0}^{N_y - 1} x[k] \cdot h[n - k]$
  - $X[k] = \operatorname{DFT}(x_p[n])$
  - $H[k] = \operatorname{DFT}(h_p[n])$
  - $Y[k] = H[k] \cdot X[k] = \operatorname{DFT}(x_p(n) \circ h_p(n)) = \operatorname{DFT}(x[n] * h[n])$
- summary
  - $y[n] = x[n] * h[n] = \operatorname{IDFT}(X[k] \cdot H[k])$ assuming $X[k]$ is DFT of zero padded $x$: $X(\Omega) \Big |_{\Omega = \frac{2 \pi}{N_y} k}$


## fast fourier theorem (fft) + algo analysis
- what is the runtime of a dft?
  - $x[n] \to N$ values
  - $X[k] = \sum_{n = 0}^{N - 1} x[n] e^{-j \frac{2 \pi}{N} k n}, k = 0, 1, \dots, N - 1$
  - for 1 coeffieicnt: $N$ complex multiplications, $N - 1$ complex additions
  - repeating for $N$ coefficients
  - $N \cdot (N + (N - 1))$ operations $= \mathcal O(N^2)$
- radix-2 fft
  - preliminaries
    - $N$-dft has $\Theta(N^2)$ complexity
    - $\omega_N = e^{-j \frac{2 \pi}{N}}, X[k] = \sum_{n = 0}^{N - 1} x[n] \omega_N^{k n}$
    - properties of $\omega_N$: 
      - $\omega_N^2 = \omega_{N / 2}$
        - $e^{-j \frac{2 \pi}{N} \cdot 2} = e^{-j \frac{2 \pi}{N / 2}}$
      - $\omega_N^{2 + N / 2} = -\omega_N^2$
        - $e^{-j \frac{2 \pi}{N} (2 + N / 2)} = e^{-j \frac{2 \pi}{N} \cdot 2} \cdot e^{-j \pi} = -\omega_N^2$
      - $\omega_N^{2 (N / 2)} = (-1)^2$
        - $e^{-j \frac{2 \pi}{N} \cdot 2 (N / 2)} = (e^{-j \pi})^2 = (-1)^2$
  - assumption: $N = 2^p$
  - $\text{even samples} = \left \{ x[0], x[2], x[4], \dots, x[N - 2] \right \}$
  - $\text{odd samples} = \left \{ x[1], x[3], [5], \dots, x[N - 1] \right \}$
  - $\begin{aligned}[t]
      X[k] &= \sum_{n = \text{even}} x[n] \omega_N^{k n} + \sum_{n = \text{odd}} x[n] \omega_N^{k n} \\ 
      &= \sum_{m = 0}^{N / 2 - 1} x[2 m] \omega_N^{k \cdot 2 m} + \sum_{m = 0}^{N / 2 - 1} x[2 m + 1] \omega_N^{k (2 m + 1)} \\ 
      &= \sum_{m = 0}^{N / 2 - 1} x[2 m] \omega_{N / 2}^{k m} + \omega_N^k \sum_{m = 0}^{N / 2 - 1} x[2 m + 1] \omega_{N / 2}^{k m} \\ 
      &= X_e[k] + \omega_N^k X_o[k]
    \end{aligned}$
  - $X_e[k]$ has length $N / 2$
  - observe that $X_e[k] = X_e[k + N / 2], X_o[k] = X_o[k + N / 2]$
  - now: 
    - $X[k] = X_e[k] + \omega_N^k X_o[k]$
    - $X[k + N / 2] = X_e[k + N / 2] + \omega_N^{k + N / 2} X_o[k + N / 2]$
    - $= X_e[k] - \omega_N^k X_o[k]$
  - complexity: $\Theta((N / 2)^2) \to 2 \Theta(N^2 / 4) + \Theta(N / 2) + \Theta(N)$

# 11.16 8w

## warm up problem
- suppose we have $\left \{ y[0], y[1] \right \}$, compute the 2-point dft
  - $Y[k] = y[0] e^0 + y[1] e^{-j \frac{2 \pi}{N} k}$
  - $Y[0] = y[0] + y[1]$
  - $Y[1] = y[0] - y[1]$

## radix-2 fft
- $X[k] = \sum_{m = 0}^{N / 2 - 1} x[2 m] \omega_N^{k \cdot 2 m} + \sum_{m = 0}^{N / 2 - 1} x[2 m + 1] \omega_N^{k (2 m + 1)}$
- $X[k] = X_e[k] - \omega_N^k X_o[k]$
- $X_e[k] \to \Theta((N / 2)^2) = \Theta(N^2 / 4)$
- $X_o[k] \to \Theta((N / 2)^2) = \Theta(N^2 / 4)$
- $X[k + N / 2] = X_e[k + N / 2] - \omega_N^{k + N / 2} X_o[k + N / 2]$
- complexity: $2 \cdot N^2 / 4 + N / 2 \text{ multiplications} + N \text{ additions} = \Theta(N^2 + N) = \Theta(N^2)$
- continue splitting
  - $X_e[k] = X_{ee}[k] + \omega_{N / 2}^k X_{eo}[k]$
  - $X_e[k + N / 4] = X_{ee}[k] - \omega_{n / 2}^k X_{eo}[k]$
  - $X_o[k] = X_{oe}[k] + \omega_{N / 2}^k X_{oo}[k]$
  - $X_o[k + N / 4] = X_{oe}[k] - \omega_{N / 2}^k X_{oo}[k]$
- can continue splitting $p$ times
- $\Theta(N)$ complexity in each state
- total complexity: $\Theta(N \log N)$
- $N \log N \ll N^2$

## application of fft (compression)
- 1 hour song at 44kHz
  - humans can only hear 20 - 20000 Hz
  - very few sounds are above 10000 Hz
  - song is usually on a major scale, few dominant notes
    - just look at fft and keep top 100 frequencies by magnitude
  - $\to$ 100 floating points
- 2d fft to compress image
  - $x[n_1, n_2] \to X[k_1, k_2]$
  - bright disc in the center and everything else is dark 
  - lossy compression

## z-transform
- motivation
  - dtft of a step function $u[n]$
  - doesnt exist
  - recall that a signal must be absolutely summable to have a dtft
  - intuition (102)
  - fourier transform of an exponential function (e.g. $e^3$): kill / damp it by multiplying by $e^{-3}$ $\to$ laplace transform
  - z-transform helps with analysis of exploding signals
  - z-transform helps solve diff eqs
- next phase of sig + sys
  - $y[n] = a x[n - 1] + x[n - 2] \to H(\Omega)$
  - reverse the idea
    - given what $H(\Omega)$ looks like
    - design the system engineering accordingly

# 11.21 9m

## z-transform
- $x[n] \overset{\mathbb Z}{\longrightarrow} X(z) = \sum_{n = -\infty}^\infty x[n] z^{-n}, z = r e^{j \Omega} \in \mathbb C$
- $X(z) = \mathbb Z \left \{ x[n] \right \}$
- observe: z-transform is a superset of dtft
- $X(z) \big |_{z = r e^{j \Omega}} = \sum_{n = -\infty}^\infty x[n] r^{-n} e^{-j \Omega n}$
  - $r = 1 \Rightarrow X(\Omega)$ (dtft)
- dtft is obtained from z-transform for setting $z = e^{j \Omega}$ if $X(z)$ exists for $e^{j \Omega}$
- example
  - $x[n] = \left \{ \dot 1, 5, 7, 9, 13 \right \}$: finite duration, causal
  - $\begin{aligned}[t]
      X(z) &= \sum_{n = -\infty}^\infty x[n] z^{-n} \\ 
      &= 1 z^0 + 5 z^{-1} + 7 z^{-2} + 9 z^{-3} + 13 z^{-4} \\ 
    \end{aligned}$
  - $X(z)$ exists for $z \neq 0 + j \cdot 0$ or $\left | z \right | \neq 0$
  - concept: region of convergence: values of $z$ for which $X(z)$ "exists"
    - "exists" means it is not infinity
- example
  - $x[n] = \left \{ 3, 1, \dot 2, 4, 5 \right \}$: non-causal, finite duration
  - $\mathbb Z \left \{ x[n] \right \} = X(z) = 3 z^2 + z + 2 + 4 z^{-1} + 5 z^{-2}$
  - region of convergence: $\left | z \right | \neq 0$ and $\left | z \right | \nrightarrow \infty$
- example
  - try to compute $\mathbb Z \left \{ \delta[n] \right \}$
  - $\delta[n] \overset{\mathbb Z}{\longrightarrow} \delta[0] z^{-0} = 1$
  - roc: entire $z$-plane
- example
  - $\mathbb Z \left \{ \delta[n - k] \right \} = z^{-k}$
  - roc: $\left | z \right | \neq 0$ if $k > 0$, $\left | z \right | \nrightarrow \infty$ if $k < 0$, entire $z$-plane if $k = 0$
- example
  - $u[n] = \begin{cases}
      1 & n \geq 0 \\ 
      0 & n < 0
    \end{cases}$
  - $\mathbb Z \left \{ u[n] \right \} = \sum_{n = 0}^\infty z^{-n} = \frac{1}{1 - z^{-1}} = \frac{z}{z - 1}$
  - roc: $\left | z \right | > 1$
  - summary: dtft, which is $X(z) \big |_{z = e^{j \Omega}}$ is not in the roc; this is consistent with our understanding that dtft of $u[n]$ does not exist
- example
  - compute the z-transform of $x[n] = a^n u[n]$: infinite duration, causal
  - $X(z) = \sum_{n = -\infty}^\infty a^n u[n] z^{-n} = \sum_{n = 0}^\infty a^n z^{-n} = \frac{1}{1 - a z^{-1}} = \frac{z}{z - a}$
  - roc: $\left | a z^{-1} \right | < 1$ or $\left | z \right | > \left | a \right |$
  - dtft exists if $\left | a \right | < 1$
- observation: z-transform are fractional polynomials
  - $X(z)$ is defined by $z_1, z_2, \dots, z_M$ zeroes and $p_1, p_2, \dots, p_N$ poles (roc does not contain poles)
- examples
  - $x[n] = \begin{cases}
      1 & 0 \leq n \leq N - 1 \\ 
      0 & n < 0 \vee n > N
    \end{cases}$
  - $X(z) = \sum_{n = 0}^{N - 1} z^{-n} = \frac{1 - z^{-N}}{1 - z^{-1}} = \frac{z^N - 1}{z^{N - 1} (z - 1)}$
  - roc: $\left | z \right | \neq 0$
    - note: $z = 1$ works
- example
  - $x[n] = -a^n u[-n - 1] = \begin{cases}
      -a^n & n < 0 \\ 
      0 & n \geq 0
    \end{cases}$
  - $X(z) = \sum_{n = -\infty}^\infty -a^n u[-n - 1] z^{-n} = \sum_{n = -\infty}^{-1} -a^n z^{-n} = -\sum_{m = 1}^\infty a^{-m} z^m = -\frac{a^{-1} z}{1 - a^{-1} z} = \frac{z}{z - a}$
  - roc: $\left | a^{-1} z \right | < 1$ or $\left | z \right | < \left | a \right |$
  - z-transform is uniquely defined by $X(z)$ *and* roc
- example
  - $x[n] = 3^{-n} u[n] - 2^{-n} u[-n - 1]$
  - $x_1[n] = 3^{-n} u[n]$
  - $x_2[n] = 2^{-n} u[-n - 1]$
  - $X(z) = X_1(z) - X_2(z) = \frac{z}{z - 3^{-1}} - \frac{z}{z - 2^{-1}}$
  - roc: $\left | z \right | \in (3^{-1}, \infty) \cap [0, 2^{-1}) = (3^{-1}, 2^{-1})$
- summary
  - roc is circularly shaped in z-transform
  - roc cannot have any poles
  - causal signals are outside the circle
  - anticausal signals are inside the circle
  - signals that decompose into causal and anticausal signals have a ring shaped roc

# 11.23 9w

## z-transform properties
- recall: $x[n] \overset{\mathbb Z}{\longrightarrow} X(z) = \sum_{n = -\infty}^\infty x[n] z^{-n}$ where $z \in \mathbb C$
  - $z = e^{j \Omega} \to$ dtft
- linearity
  - if $x_1[n] \overset{\mathbb Z}{\longrightarrow} X_1(z)$ and $x_2[n] \overset{\mathbb Z}{\longrightarrow} X_2(z)$
  - then $\alpha x_1[n] + \beta x_2[n] \overset{\mathbb Z}{\longrightarrow} \alpha X_1(z) + \beta X_2(z)$
  - roc: recalculate poles
- time shifting
  - if $x[n] \overset{\mathbb Z}{\longrightarrow} X(z)$
  - then $x[n - k] \overset{\mathbb Z}{\longrightarrow} X(z) z^{-k}$
  - proof
    - $\mathbb Z \left \{ x[n - k] \right \} = \sum_{n = -\infty}^\infty x[n - k] z^{-n} = \sum_{m = -\infty}^\infty x[m] z^{-(m + k)} = z^{-k} \sum_{m = -\infty}^\infty x[m] z^{-m} = z^{-k} X(z)$
  - new roc $\neq$ roc
  - $k > 0$: roc excludes $\left | z \right | = 0$
  - $k < 0$: roc excludes $\left | z \right | \to \infty$
- convolution property
  - if $x_1[n] \overset{\mathbb Z}{\longrightarrow} X_1(z)$ and $x_2[n] \overset{\mathbb Z}{\longrightarrow} X_2(z)$
  - then $x_1[n] * x_2[n] \overset{\mathbb Z}{\longrightarrow} X_1(z) X_2(z)$
  - proof
    - $x_1[n] * x_2[n] = \sum_{k = -\infty}^\infty x_1[k] x_2[n - k]$
    - $\begin{aligned}[t]
        \mathbb Z \left \{ \sum_{k = -\infty}^\infty x_1[k] x_2[n - k] \right \} &= \sum_{n = -\infty}^\infty \left ( \sum_{k = -\infty}^\infty x_1[k] x_2[n - k] \right ) z^{-n} \\ 
        &= \sum_{k = -\infty}^\infty x_1[k] \sum_{n = -\infty}^\infty x_2[n - k] z^{-n} \\ 
        &= x_1[k] \sum_{k = -\infty}^\infty X_2(z) z^{-k} \\ 
        &= X_2(z) \sum_{k = -\infty}^\infty x_1[k] z^{-k} \\ 
        &= X_1(z) X_2(z)
      \end{aligned}$
    - combined roc depends on the poles (pay attention to zero-pole cancellations)

## inverse z-transform
- $X(z) = \frac{B(z)}{(z - p_1) (z - p_2) \cdots (z - p_N)}$
- recall
  - $a^n u[n] \overset{\mathbb Z}{\longrightarrow} \frac{z}{z - a}, \left | z \right | > \left | a \right |$
  - $-a^n u[-n - 1] \overset{\mathbb Z}{\longrightarrow} \frac{z}{z - a}, \left | z \right | < \left | a \right |$
- $X(z) = \frac{k_1 z}{z - p_1} + \frac{k_2 z}{z - p_2} + \cdots + \frac{k_N z}{p - p_N}$
- example
  - $X(z) = \frac{(z - 1) (z + 2)}{(z - 1 / 2) (z - 2)}$
  - $\frac{X(z)}{z} = \frac{(z - 1) (z + 2)}{z (z - 1 / 2) (z - 2)} = \frac{k_1}{z} + \frac{k_2}{z - 1 / 2} + \frac{k_3}{z - 2}$
  - $k_1 = \left ( \frac{k_1}{z} + \frac{k_2}{z - 1 / 2} + \frac{k_3}{z - 2} \right ) \cdot (z - 0) \Big |_{z = 0} = (z - 0) \frac{X(z)}{z} = X(z) \Big |_{z = 0} = \frac{(0 - 1) (0 + 2)}{(0 - 1 / 2) (0 - 2)} = -2$
  - $k_2 = \frac{(1 / 2 - 1) (1 / 2 + 2)}{(1 / 2) (1 / 2 - 2)} = \frac{5}{3}$
  - $k_3 = \frac{(2 - 1) (2 + 2)}{2 (2 - 1 / 2)} = \frac{4}{3}$
  - $X(z) = -2 + \frac{(5 / 3) z}{z - 1 / 2} + \frac{(4 / 3) z}{z - 2}$
  - $X(z) \overset{\mathbb Z^{-1}}{\longrightarrow} x[n] = -2 \delta[n] + \frac{5}{3} x_1[n] + \frac{4}{3} x_2[n]$
  - roc $\left | z \right | > 2$: $x_1[n] = 2^{-n} u[n], x_2[n] = 2^n u[n]$
  - roc $\left | z \right | < 2^{-1}$: $x_1[n] = -2^n u[-n - 1], x_2[n] = -2^{-n} u[-n - 1]$
  - roc $2^{-1} < \left | z \right | < 2$: $x_1[n] = 2^{-n} u[n], x_2[n] = -2^{-n} u[-n - 1]$
- summary
  - find poles $\left \{ p_i \right \}, i = 1, \dots, N$
  - find coefficients for partial fraction $k_i = X(z) (z - p_i) \Big |_{z = p_i}$
  - based on roc, digure out which causality of canonical z-transform pairs to use

## using z-transform to analyze / design dtlti systems
- $H(z) = \mathbb Z \left \{ h[n] \right \}$
- $H(z) = \frac{Y(z)}{X(z)}$: easier to obtain
- recall: dtlti is defined by a constant coefficient difference equation w suitable initial conditions
- $\sum_{k = 0}^N a_k y[n - k] = \sum_{k = 0}^M b_k x[n - k]$
  - z-tranfrom on both sides: $\sum_{k = 0}^N a_k z^{-k} Y(z) = \sum_{k = 0}^M b_k X(z) z^{-k}$
  - $\frac{Y(z)}{X(z)} = \frac{\sum_{k = 0}^M b_k z^{-k}}{\sum_{k = 0}^N a_k Z^{-k}} = H(z)$
- given $H(z)$, say smth abt the system
  - causal? $h[n]$ only defined for $n \geq 0$
    - check that $\left | z \right | \to \infty$ is defined on the $z$-plane
    - $\lim_{z \to \infty} H(z) = \lim_{z \to \infty} \frac{\sum_{k = 0}^M b_k z^{-k}}{\sum_{k = 0}^N a_k z^{-k}} < \infty$
    - for causality: $N \geq M$
  - stable? $h[n]$ bounded or dtft bounded / exists
    - check that unit circle is in roc

## design of dtlti
- $H(z) = \frac{b_0 + b_1 z^{-1} + \cdots + b_M z^{-M}}{1 + a_1 1^{-1} + \cdots + a_N z^{-N}}$
- $y[n] = b_0 x[n] + b_1 x[n - 1] + \cdots + b_M x[n - M] - a_1 y[n - 1] - \cdots - a_N y[n - N]$

  ![](img/11.23.0.png)

- steps
  - given $H(z)$ in pole / zero notation
  - given $H(z)$ in polynomial
  - constant coefficient diff eq
  - system circuit / design
- gap: how to go from high level idea, e.g. "filter out frequencies from 30 - 50Hz", to $H(z)$

# 11.28 10m

## review
- recall: $H(z) = \frac{(z - z_1) \cdots (z - z_N)}{(z - p_1) \cdots (z - p_M)}$ (poles and zeroes)
- $H(z) = \frac{\sum_{k = 0}^M b_k z^{-k}}{\sum_{k = 0}^N a_k z^{-k}}$ (polynomial coefficients / constant coefficient difference equation $\to$ block diagram)

## design question
- low pass filter with pas_and of 20000 Hz
- stable system: dtft exists $\to$ roc includes unit circle
- $H(z) = \frac{\prod_{i = 0}^M (z - z_i)}{\prod_{i = 0}^N (z - p_i)}$
- $H(e^{j \Omega}) = \frac{\prod_{i = 0}^M (e^{j \Omega} - z_i)}{\prod_{i = 0}^N (e^{j \Omega} - p_i)}$
- $\left | H(e^{j \Omega}) \right | = \frac{\prod_{i = 0}^M (e^{j \Omega} - z_i)}{\prod_{i = 0}^N (e^{j \Omega} - p_i)}$
  - $\Omega$ can express in Hz if we want to
- key insight
  - a frequency in Hz that is near a zero is attenuated
  - a frequency near a pole is amplified

## fir filter
- "finite impulse response"
- $H(e^{j \omega}) = \sum_{k = 0}^M b_k z^{-n}$
- $y[n] = x[n] + b_1 x[n - 1] + b_2 x[n - 2]$: ~convolution
- easy to do optimization to find $b_k$'s
- find frequency / phase response
- with enough $b_k$'s, we can make pretty much any filter
- problem: requires large $M$

## iir filter
- $H(z) = \frac{\sum_{k = 0}^M b_k z^{-k}}{\sum_{k = 0}^N a_k z^{-k}}$
- add feedback
- complex designs with fewer coefficients
- nonlinear effects (phase unpredictable)

## practice

  ![](img/11.28.0.png)

- "detective / sleuth" question
  - evaluate $H(z)$
  - $S_1$: has a pole at 0.5, a zero at 0, and $H_1(1) = -3$
  - $S_2$: $y[n] - 0.7 y[n - 1] = 2.5 x[n] - 1.6 x[n - 1]$
  - $S_3$: $h_3[n] = \frac{5}{4} (0.8)^n u[n - 1]$
  - $H(z) = (H_1(z) + H_2(z)) \cdot H_3(z)$
  - $H_1(z) = A \cdot \frac{z}{z - 0.5} = -\frac{3 z}{2 (z - 0.5)}$
    - roc: $\left | z \right | > 0.5$ (check if $H$ goes to infinity as $z \to \infty$)
  - $H_2(z) = \frac{2.5 - 1.6 z^{-1}}{1 - 0.7 z^{-1}} = \frac{2.5 z - 1.6}{z - 0.7}$
    - roc: $\left | z \right | > 0.7$
  - $H_3(z) = \mathbb Z \left \{ h_3[n] \right \} = \mathbb Z \left \{ (0.8)^{n - 1} u[n - 1] \right \} = z^{-1} \left ( \frac{z}{z - 0.8} \right ) = \frac{1}{z - 0.8}$
    - roc: $\left | z \right | > 0.8$
  - $H(z) = \frac{(z - 1) (z - 0.8)}{(z - 0.5) (z - 0.7) (z - 0.8)} = \frac{z - 1}{(z - 0.5) (z - 0.7)}$
    - roc: $\left | z \right | > 0.7$ because of zero-pole cancellation
