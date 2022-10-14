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
- todo

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
- suppoer $\tilde x[n]$ is a periodic signal
- goal is to represent $\tilde x[n] = \sum_k \tilde c_k \phi_k[n]$
- $\phi_k[n] = e^{j \Omega_k n}$ fourier basis
- $\Omega_k$ si the angular frequency of the $k$-th basis vector
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
