# Equation reference — *Optimal market making*

This file is the normalized LaTeX equation sheet for Olivier Guéant's *Optimal market making* (arXiv:1605.01862v5). It is intended as the machine-readable mathematical companion to `document.md`.

Notation follows the paper. In particular, `\Delta` is the fixed trade size, `Q` an inventory limit, `\Lambda^b,\Lambda^a` execution-intensity functions, `\gamma` the price-risk parameter, and `\xi` the auxiliary parameter that unifies Models A and B.

## 2. Modeling framework

### Equation (2.1) — reference price

$$
dS_t=\sigma\,dW_t,\qquad S_0\ \text{given}.
$$

### Equation (2.2) — inventory

$$
dq_t=\Delta\,dN_t^b-\Delta\,dN_t^a,\qquad q_0\ \text{given}.
$$

### Equation (2.3) — execution intensities and quote distances

$$
\lambda_t^b=\Lambda^b(\delta_t^b)\mathbf 1_{\{q_{t^-}<Q\}},
\qquad
\lambda_t^a=\Lambda^a(\delta_t^a)\mathbf 1_{\{q_{t^-}>-Q\}},
$$

with

$$
\delta_t^b=S_t-S_t^b,
\qquad
\delta_t^a=S_t^a-S_t.
$$

### Equation (2.4) — cash account

$$
\begin{aligned}
dX_t
&=S_t^a\Delta\,dN_t^a-S_t^b\Delta\,dN_t^b\\
&=(S_t+\delta_t^a)\Delta\,dN_t^a-(S_t-\delta_t^b)\Delta\,dN_t^b.
\end{aligned}
$$

### Model A

$$
\sup_{(\delta_t^b),(\delta_t^a)\in\mathcal A}
\mathbb E\!\left[-\exp\!\left(-\gamma\bigl(X_T+q_TS_T-\ell(|q_T|)\bigr)\right)\right].
$$

### Model B

$$
\sup_{(\delta_t^b),(\delta_t^a)\in\mathcal A}
\mathbb E\!\left[
X_T+q_TS_T-\ell(|q_T|)
-\frac12\gamma\sigma^2\int_0^T q_t^2\,dt
\right].
$$

## 3. Unified ODE characterization

Let

$$
\mathcal Q=\{-Q,-Q+\Delta,\ldots,Q-\Delta,Q\}.
$$

### Equation (3.1) — HJB for Model A

$$
\begin{aligned}
0={}&-\partial_tu(t,x,q,S)-\frac12\sigma^2\partial_{SS}^2u(t,x,q,S)\\
&-\mathbf 1_{\{q<Q\}}\sup_{\delta^b}\Lambda^b(\delta^b)
\Bigl[u(t,x-\Delta S+\Delta\delta^b,q+\Delta,S)-u(t,x,q,S)\Bigr]\\
&-\mathbf 1_{\{q>-Q\}}\sup_{\delta^a}\Lambda^a(\delta^a)
\Bigl[u(t,x+\Delta S+\Delta\delta^a,q-\Delta,S)-u(t,x,q,S)\Bigr].
\end{aligned}
$$

### Equation (3.2) — Model A terminal condition

$$
u(T,x,q,S)=-\exp\!\left(-\gamma(x+qS-\ell(|q|))\right).
$$

### Equation (3.3) — Model A ansatz

$$
u(t,x,q,S)=-\exp\!\left(-\gamma(x+qS+\theta(t,q))\right).
$$

### Equation (3.4) — reduced Model A system

$$
\begin{aligned}
0={}&-\partial_t\theta(t,q)+\frac12\gamma\sigma^2q^2\\
&-\mathbf 1_{\{q<Q\}}\sup_{\delta^b}
\frac{\Lambda^b(\delta^b)}{\gamma}
\left[1-\exp\!\left(-\gamma\bigl(\Delta\delta^b+\theta(t,q+\Delta)-\theta(t,q)\bigr)\right)\right]\\
&-\mathbf 1_{\{q>-Q\}}\sup_{\delta^a}
\frac{\Lambda^a(\delta^a)}{\gamma}
\left[1-\exp\!\left(-\gamma\bigl(\Delta\delta^a+\theta(t,q-\Delta)-\theta(t,q)\bigr)\right)\right].
\end{aligned}
$$

with `\theta(T,q)=-\ell(|q|)`.

### Equation (3.5) — HJB for Model B

$$
\begin{aligned}
0={}&-\partial_tu(t,x,q,S)+\frac12\gamma\sigma^2q^2
-\frac12\sigma^2\partial_{SS}^2u(t,x,q,S)\\
&-\mathbf 1_{\{q<Q\}}\sup_{\delta^b}\Lambda^b(\delta^b)
\Bigl[u(t,x-\Delta S+\Delta\delta^b,q+\Delta,S)-u(t,x,q,S)\Bigr]\\
&-\mathbf 1_{\{q>-Q\}}\sup_{\delta^a}\Lambda^a(\delta^a)
\Bigl[u(t,x+\Delta S+\Delta\delta^a,q-\Delta,S)-u(t,x,q,S)\Bigr].
\end{aligned}
$$

### Equation (3.6) — Model B terminal condition

$$
u(T,x,q,S)=x+qS-\ell(|q|).
$$

### Equation (3.7) — Model B ansatz

$$
u(t,x,q,S)=x+qS+\theta(t,q).
$$

### Equation (3.8) — reduced Model B system

$$
\begin{aligned}
0={}&-\partial_t\theta(t,q)+\frac12\gamma\sigma^2q^2\\
&-\mathbf 1_{\{q<Q\}}\sup_{\delta^b}\Lambda^b(\delta^b)
\Bigl(\Delta\delta^b+\theta(t,q+\Delta)-\theta(t,q)\Bigr)\\
&-\mathbf 1_{\{q>-Q\}}\sup_{\delta^a}\Lambda^a(\delta^a)
\Bigl(\Delta\delta^a+\theta(t,q-\Delta)-\theta(t,q)\Bigr).
\end{aligned}
$$

### Hamiltonians `H_\xi^b,H_\xi^a`

For `\xi>0`,

$$
H_\xi^b(p)=\sup_\delta\frac{\Lambda^b(\delta)}{\xi}
\left(1-e^{-\xi\Delta(\delta-p)}\right),
\qquad
H_\xi^a(p)=\sup_\delta\frac{\Lambda^a(\delta)}{\xi}
\left(1-e^{-\xi\Delta(\delta-p)}\right).
$$

For `\xi=0`,

$$
H_0^b(p)=\Delta\sup_\delta\Lambda^b(\delta)(\delta-p),
\qquad
H_0^a(p)=\Delta\sup_\delta\Lambda^a(\delta)(\delta-p).
$$

### Equation (3.9) — unified system

$$
\begin{aligned}
0={}&-\partial_t\theta(t,q)+\frac12\gamma\sigma^2q^2\\
&-\mathbf 1_{\{q<Q\}}H_\xi^b\!\left(\frac{\theta(t,q)-\theta(t,q+\Delta)}{\Delta}\right)\\
&-\mathbf 1_{\{q>-Q\}}H_\xi^a\!\left(\frac{\theta(t,q)-\theta(t,q-\Delta)}{\Delta}\right).
\end{aligned}
$$

### Equation (3.10) — unified terminal condition

$$
\theta(T,q)=-\ell(|q|).
$$

### Equations (3.11) and (3.12) — optimal one-step offsets

The maximizing bid offset `\tilde\delta_\xi^{b*}(p)` is characterized for `\xi>0` by

$$
p=\tilde\delta_\xi^{b*}(p)
-\frac{1}{\xi\Delta}
\log\!\left(
1-\xi\Delta
\frac{\Lambda^b(\tilde\delta_\xi^{b*}(p))}
{{\Lambda^b}'(\tilde\delta_\xi^{b*}(p))}
\right),
$$

and for `\xi=0` by

$$
p=\tilde\delta_0^{b*}(p)+
\frac{\Lambda^b(\tilde\delta_0^{b*}(p))}
{{\Lambda^b}'(\tilde\delta_0^{b*}(p))}.
$$

Equivalently,

$$
\boxed{
\tilde\delta_\xi^{b*}(p)=
(\Lambda^b)^{-1}\!\left(\xi H_\xi^b(p)-\frac{{H_\xi^b}'(p)}{\Delta}\right)
}
\tag{3.11}
$$

and

$$
\boxed{
\tilde\delta_\xi^{a*}(p)=
(\Lambda^a)^{-1}\!\left(\xi H_\xi^a(p)-\frac{{H_\xi^a}'(p)}{\Delta}\right)
}
\tag{3.12}
$$

with the analogous first-order conditions on the ask side.

### Equation (3.13) — exponential-intensity linear system

If

$$
\Lambda^b(\delta)=\Lambda^a(\delta)=Ae^{-k\delta}=:\Lambda(\delta),
$$

then

$$
H_\xi(p)=\frac{A\Delta}{k}C_\xi e^{-kp},
$$

where

$$
C_\xi=
\begin{cases}
\left(1+\dfrac{\xi\Delta}{k}\right)^{-\frac{k}{\xi\Delta}-1}, & \xi>0,\\[6pt]
e^{-1}, & \xi=0.
\end{cases}
$$

With

$$
v_q(t)=\exp\!\left(\frac{k}{\Delta}\theta(t,q)\right),
$$

we obtain

$$
-\partial_t v_q(t)
+\frac{k\gamma\sigma^2}{2\Delta}q^2v_q(t)
-A C_\xi\left(
\mathbf1_{\{q<Q\}}v_{q+\Delta}(t)
+\mathbf1_{\{q>-Q\}}v_{q-\Delta}(t)
\right)=0.
\tag{3.13}
$$

The terminal condition is

$$
v_q(T)=\exp\!\left(-\frac{k}{\Delta}\ell(|q|)\right).
$$

### Equation (3.14) — Model A optimal quotes

$$
\boxed{
\delta_t^{b*}=\tilde\delta_\gamma^{b*}\!\left(
\frac{\theta(t,q_{t^-})-\theta(t,q_{t^-}+\Delta)}{\Delta}
\right),
\qquad
\delta_t^{a*}=\tilde\delta_\gamma^{a*}\!\left(
\frac{\theta(t,q_{t^-})-\theta(t,q_{t^-}-\Delta)}{\Delta}
\right)
}
\tag{3.14}
$$

The long Itô verification identity numbered (3.15) is preserved visually in `source_pages/page-13.png` through `source_pages/page-15.png` rather than re-keyed here.

### Equation (3.16) — Model B optimal quotes

$$
\boxed{
\delta_t^{b*}=\tilde\delta_0^{b*}\!\left(
\frac{\theta(t,q_{t^-})-\theta(t,q_{t^-}+\Delta)}{\Delta}
\right),
\qquad
\delta_t^{a*}=\tilde\delta_0^{a*}\!\left(
\frac{\theta(t,q_{t^-})-\theta(t,q_{t^-}-\Delta)}{\Delta}
\right)
}
\tag{3.16}
$$

The long Itô verification identity numbered (3.17) is preserved visually in `source_pages/page-16.png` and `source_pages/page-17.png`.

## 4. Closed-form and almost-closed-form approximations

Assume symmetric intensities `\Lambda^b=\Lambda^a=:\Lambda` and write `H_\xi:=H_\xi^b=H_\xi^a`.

### Equation (4.1) — continuous-inventory PDE approximation

$$
0=-\partial_t\tilde\theta(t,q)
+\frac12\gamma\sigma^2q^2
-2H_\xi(0)
-H_\xi''(0)\bigl(\partial_q\tilde\theta(t,q)\bigr)^2
+\Delta H_\xi'(0)\partial_{qq}^2\tilde\theta(t,q).
\tag{4.1}
$$

### Hopf-Cole-type transform and Equation (4.2)

Define

$$
\tilde v(t,q)=\exp\!\left(
-\frac{H_\xi''(0)}{\Delta H_\xi'(0)}\tilde\theta(t,q)
\right).
$$

Then

$$
0=\partial_t\tilde v(t,q)
-\frac{H_\xi''(0)}{\Delta H_\xi'(0)}
\left(2H_\xi(0)-\frac12\gamma\sigma^2q^2\right)\tilde v(t,q)
-\Delta H_\xi'(0)\partial_{qq}^2\tilde v(t,q).
\tag{4.2}
$$

### Asymptotic finite differences of `\theta`

$$
\frac{\theta(t,q)-\theta(t,q+\Delta)}{\Delta}
\simeq
\frac{2q+\Delta}{2}\sqrt{\frac{\gamma\sigma^2}{2H_\xi''(0)}},
$$

$$
\frac{\theta(t,q)-\theta(t,q-\Delta)}{\Delta}
\simeq
-\frac{2q-\Delta}{2}\sqrt{\frac{\gamma\sigma^2}{2H_\xi''(0)}}.
$$

### Equations (4.3)–(4.5) — general quote approximations

$$
\boxed{
\delta_t^{b*}\simeq\delta_{\mathrm{approx}}^{b*}(q_{t^-})
:=\tilde\delta_\xi^*\!\left(
\frac{2q_{t^-}+\Delta}{2}\sqrt{\frac{\gamma\sigma^2}{2H_\xi''(0)}}
\right)
}
\tag{4.3}
$$

$$
\boxed{
\delta_t^{a*}\simeq\delta_{\mathrm{approx}}^{a*}(q_{t^-})
:=\tilde\delta_\xi^*\!\left(
-\frac{2q_{t^-}-\Delta}{2}\sqrt{\frac{\gamma\sigma^2}{2H_\xi''(0)}}
\right)
}
\tag{4.4}
$$

where

$$
\boxed{
\tilde\delta_\xi^*(p)=\Lambda^{-1}\!\left(
\xi H_\xi(p)-\frac{H_\xi'(p)}{\Delta}
\right)
}
\tag{4.5}
$$

### Equations (4.6) and (4.7) — exponential intensities

For `\Lambda(\delta)=Ae^{-k\delta}`,

$$
\delta_{\mathrm{approx}}^{b*}(q)=
\begin{cases}
\dfrac{1}{\xi\Delta}\log\!\left(1+\dfrac{\xi\Delta}{k}\right)
+\dfrac{2q+\Delta}{2}
\sqrt{\dfrac{\gamma\sigma^2}{2A\Delta k}
\left(1+\dfrac{\xi\Delta}{k}\right)^{\frac{k}{\xi\Delta}+1}}, & \xi>0,\\[10pt]
\dfrac1k+\dfrac{2q+\Delta}{2}\sqrt{\dfrac{\gamma\sigma^2e}{2A\Delta k}}, & \xi=0.
\end{cases}
\tag{4.6}
$$

$$
\delta_{\mathrm{approx}}^{a*}(q)=
\begin{cases}
\dfrac{1}{\xi\Delta}\log\!\left(1+\dfrac{\xi\Delta}{k}\right)
-\dfrac{2q-\Delta}{2}
\sqrt{\dfrac{\gamma\sigma^2}{2A\Delta k}
\left(1+\dfrac{\xi\Delta}{k}\right)^{\frac{k}{\xi\Delta}+1}}, & \xi>0,\\[10pt]
\dfrac1k-\dfrac{2q-\Delta}{2}\sqrt{\dfrac{\gamma\sigma^2e}{2A\Delta k}}, & \xi=0.
\end{cases}
\tag{4.7}
$$

### Equations (4.8) and (4.9) — approximate spread and skew

$$
\delta_{\mathrm{approx}}^{b*}(q)+\delta_{\mathrm{approx}}^{a*}(q)=
\begin{cases}
\dfrac{2}{\xi\Delta}\log\!\left(1+\dfrac{\xi\Delta}{k}\right)
+\Delta\sqrt{\dfrac{\gamma\sigma^2}{2A\Delta k}
\left(1+\dfrac{\xi\Delta}{k}\right)^{\frac{k}{\xi\Delta}+1}}, & \xi>0,\\[10pt]
\dfrac{2}{k}+\Delta\sqrt{\dfrac{\gamma\sigma^2e}{2A\Delta k}}, & \xi=0,
\end{cases}
\tag{4.8}
$$

$$
\delta_{\mathrm{approx}}^{b*}(q)-\delta_{\mathrm{approx}}^{a*}(q)=
\begin{cases}
2q\sqrt{\dfrac{\gamma\sigma^2}{2A\Delta k}
\left(1+\dfrac{\xi\Delta}{k}\right)^{\frac{k}{\xi\Delta}+1}}, & \xi>0,\\[10pt]
2q\sqrt{\dfrac{\gamma\sigma^2e}{2A\Delta k}}, & \xi=0.
\end{cases}
\tag{4.9}
$$

## 5. Multi-asset market making

For `i\in\{1,\ldots,d\}`, let `S_t^i` be the reference price and `\Delta_i` the trade size. Let `\Sigma=(\rho^{i,j}\sigma^i\sigma^j)_{i,j}`.

### Equation (5.1)

$$
dS_t^i=\sigma^i\,dW_t^i,\qquad S_0^i\ \text{given}.
\tag{5.1}
$$

### Equation (5.2)

$$
dq_t^i=\Delta_i\,dN_t^{i,b}-\Delta_i\,dN_t^{i,a},
\qquad q_0^i\ \text{given}.
\tag{5.2}
$$

### Equation (5.3)

$$
\lambda_t^{i,b}=\Lambda^{i,b}(\delta_t^{i,b})\mathbf1_{\{q_{t^-}^i<Q_i\}},
\qquad
\lambda_t^{i,a}=\Lambda^{i,a}(\delta_t^{i,a})\mathbf1_{\{q_{t^-}^i>-Q_i\}},
\tag{5.3}
$$

with

$$
\delta_t^{i,b}=S_t^i-S_t^{i,b},
\qquad
\delta_t^{i,a}=S_t^{i,a}-S_t^i.
$$

### Equation (5.4)

$$
\begin{aligned}
dX_t
&=\sum_{i=1}^d\left(S_t^{i,a}\Delta_i\,dN_t^{i,a}-S_t^{i,b}\Delta_i\,dN_t^{i,b}\right)\\
&=\sum_{i=1}^d\left((S_t^i+\delta_t^{i,a})\Delta_i\,dN_t^{i,a}-(S_t^i-\delta_t^{i,b})\Delta_i\,dN_t^{i,b}\right).
\end{aligned}
\tag{5.4}
$$

### Equation (5.5) — multi-asset Model A HJB

Let `e_i` be the canonical basis of `\mathbb R^d`. Then

$$
\begin{aligned}
0={}&-\partial_tu(t,x,q,S)
-\frac12\sum_{i=1}^d\sum_{j=1}^d\rho^{i,j}\sigma^i\sigma^j\partial_{S^iS^j}^2u(t,x,q,S)\\
&-\sum_{i=1}^d\mathbf1_{\{q^i<Q_i\}}\sup_{\delta^{i,b}}\Lambda^{i,b}(\delta^{i,b})
\Bigl[u(t,x-\Delta_iS^i+\Delta_i\delta^{i,b},q+\Delta_ie_i,S)-u(t,x,q,S)\Bigr]\\
&-\sum_{i=1}^d\mathbf1_{\{q^i>-Q_i\}}\sup_{\delta^{i,a}}\Lambda^{i,a}(\delta^{i,a})
\Bigl[u(t,x+\Delta_iS^i+\Delta_i\delta^{i,a},q-\Delta_ie_i,S)-u(t,x,q,S)\Bigr].
\end{aligned}
\tag{5.5}
$$

### Equation (5.6)

$$
u(T,x,q,S)=-\exp\!\left[-\gamma\left(x+\sum_{i=1}^dq^iS^i-\ell_d(q^1,\ldots,q^d)\right)\right].
\tag{5.6}
$$

### Equation (5.7)

$$
u(t,x,q,S)=-\exp\!\left[-\gamma\left(x+\sum_{i=1}^dq^iS^i+\theta(t,q)\right)\right].
\tag{5.7}
$$

### Equation (5.8) — reduced multi-asset Model A

$$
\begin{aligned}
0={}&-\partial_t\theta(t,q)
+\frac12\gamma\sum_{i=1}^d\sum_{j=1}^d\rho^{i,j}\sigma^i\sigma^j q^iq^j\\
&-\sum_{i=1}^d\mathbf1_{\{q^i<Q_i\}}\sup_{\delta^{i,b}}
\frac{\Lambda^{i,b}(\delta^{i,b})}{\gamma}
\left[1-e^{-\gamma(\Delta_i\delta^{i,b}+\theta(t,q+\Delta_ie_i)-\theta(t,q))}\right]\\
&-\sum_{i=1}^d\mathbf1_{\{q^i>-Q_i\}}\sup_{\delta^{i,a}}
\frac{\Lambda^{i,a}(\delta^{i,a})}{\gamma}
\left[1-e^{-\gamma(\Delta_i\delta^{i,a}+\theta(t,q-\Delta_ie_i)-\theta(t,q))}\right].
\end{aligned}
\tag{5.8}
$$

### Equation (5.9) — multi-asset Model B HJB

$$
\begin{aligned}
0={}&-\partial_tu(t,x,q,S)
+\frac12\gamma\sum_{i,j=1}^d\rho^{i,j}\sigma^i\sigma^j q^iq^j
-\frac12\sum_{i,j=1}^d\rho^{i,j}\sigma^i\sigma^j\partial_{S^iS^j}^2u(t,x,q,S)\\
&-\sum_{i=1}^d\mathbf1_{\{q^i<Q_i\}}\sup_{\delta^{i,b}}\Lambda^{i,b}(\delta^{i,b})
\Bigl[u(t,x-\Delta_iS^i+\Delta_i\delta^{i,b},q+\Delta_ie_i,S)-u(t,x,q,S)\Bigr]\\
&-\sum_{i=1}^d\mathbf1_{\{q^i>-Q_i\}}\sup_{\delta^{i,a}}\Lambda^{i,a}(\delta^{i,a})
\Bigl[u(t,x+\Delta_iS^i+\Delta_i\delta^{i,a},q-\Delta_ie_i,S)-u(t,x,q,S)\Bigr].
\end{aligned}
\tag{5.9}
$$

### Equation (5.10)

$$
u(T,x,q,S)=x+\sum_{i=1}^dq^iS^i-\ell_d(q^1,\ldots,q^d).
\tag{5.10}
$$

### Equation (5.11)

$$
u(t,x,q,S)=x+\sum_{i=1}^dq^iS^i+\theta(t,q).
\tag{5.11}
$$

### Equation (5.12) — reduced multi-asset Model B

$$
\begin{aligned}
0={}&-\partial_t\theta(t,q)
+\frac12\gamma\sum_{i,j=1}^d\rho^{i,j}\sigma^i\sigma^j q^iq^j\\
&-\sum_{i=1}^d\mathbf1_{\{q^i<Q_i\}}\sup_{\delta^{i,b}}\Lambda^{i,b}(\delta^{i,b})
\Bigl(\Delta_i\delta^{i,b}+\theta(t,q+\Delta_ie_i)-\theta(t,q)\Bigr)\\
&-\sum_{i=1}^d\mathbf1_{\{q^i>-Q_i\}}\sup_{\delta^{i,a}}\Lambda^{i,a}(\delta^{i,a})
\Bigl(\Delta_i\delta^{i,a}+\theta(t,q-\Delta_ie_i)-\theta(t,q)\Bigr).
\end{aligned}
\tag{5.12}
$$

### Multi-asset Hamiltonians

For `\xi>0`,

$$
H_\xi^{i,b}(p)=\sup_\delta\frac{\Lambda^{i,b}(\delta)}{\xi}
\left(1-e^{-\xi\Delta_i(\delta-p)}\right),
\qquad
H_\xi^{i,a}(p)=\sup_\delta\frac{\Lambda^{i,a}(\delta)}{\xi}
\left(1-e^{-\xi\Delta_i(\delta-p)}\right),
$$

and for `\xi=0`,

$$
H_0^{i,b}(p)=\Delta_i\sup_\delta\Lambda^{i,b}(\delta)(\delta-p),
\qquad
H_0^{i,a}(p)=\Delta_i\sup_\delta\Lambda^{i,a}(\delta)(\delta-p).
$$

### Equation (5.13) — unified multi-asset system

$$
\begin{aligned}
0={}&-\partial_t\theta(t,q)
+\frac12\gamma\sum_{i,j=1}^d\rho^{i,j}\sigma^i\sigma^j q^iq^j\\
&-\sum_{i=1}^d\mathbf1_{\{q^i<Q_i\}}H_\xi^{i,b}\!\left(
\frac{\theta(t,q)-\theta(t,q+\Delta_ie_i)}{\Delta_i}
\right)\\
&-\sum_{i=1}^d\mathbf1_{\{q^i>-Q_i\}}H_\xi^{i,a}\!\left(
\frac{\theta(t,q)-\theta(t,q-\Delta_ie_i)}{\Delta_i}
\right).
\end{aligned}
\tag{5.13}
$$

### Equation (5.14)

$$
\theta(T,q)=-\ell_d(q^1,\ldots,q^d).
\tag{5.14}
$$

### Equations (5.15) and (5.16) — multi-asset optimal quotes

Model A (`\xi=\gamma`):

$$
\delta_t^{i,b*}=\tilde\delta_\gamma^{i,b*}\!\left(
\frac{\theta(t,q_{t^-})-\theta(t,q_{t^-}+\Delta_ie_i)}{\Delta_i}
\right),
\qquad
\delta_t^{i,a*}=\tilde\delta_\gamma^{i,a*}\!\left(
\frac{\theta(t,q_{t^-})-\theta(t,q_{t^-}-\Delta_ie_i)}{\Delta_i}
\right),
\tag{5.15}
$$

with

$$
\tilde\delta_\gamma^{i,b*}(p)=(\Lambda^{i,b})^{-1}\!\left(
\gamma H_\gamma^{i,b}(p)-\frac{{H_\gamma^{i,b}}'(p)}{\Delta_i}
\right),
$$

and analogously on the ask side.

Model B (`\xi=0`):

$$
\delta_t^{i,b*}=\tilde\delta_0^{i,b*}\!\left(
\frac{\theta(t,q_{t^-})-\theta(t,q_{t^-}+\Delta_ie_i)}{\Delta_i}
\right),
\qquad
\delta_t^{i,a*}=\tilde\delta_0^{i,a*}\!\left(
\frac{\theta(t,q_{t^-})-\theta(t,q_{t^-}-\Delta_ie_i)}{\Delta_i}
\right).
\tag{5.16}
$$

### Equation (5.17) — multidimensional PDE approximation

Assume symmetric sides `\Lambda^{i,b}=\Lambda^{i,a}=:\Lambda^i`, and write `H_\xi^i` for the corresponding Hamiltonian. Then

$$
\begin{aligned}
0={}&-\partial_t\tilde\theta(t,q)
+\frac12\gamma\sum_{i,j=1}^d\rho^{i,j}\sigma^i\sigma^j q^iq^j
-2\sum_{i=1}^dH_\xi^i(0)\\
&-\sum_{i=1}^d {H_\xi^i}''(0)(\partial_{q^i}\tilde\theta(t,q))^2
+\sum_{i=1}^d \Delta_i{H_\xi^i}'(0)\partial_{q^iq^i}^2\tilde\theta(t,q).
\end{aligned}
\tag{5.17}
$$

> Source-layout note: the paper writes the last term as `+ \Delta_i {H_\xi^i}'(0)\partial_{q_iq_i}^2\tilde\theta` inside the sum preceded by an overall minus on the quadratic-gradient term. Since `{H_\xi^i}'(0)<0`, signs should be interpreted exactly as in the displayed paper. See `source_pages/page-29.png` for visual ground truth.

Define

$$
D=\operatorname{diag}\bigl({H_\xi^1}''(0),\ldots,{H_\xi^d}''(0)\bigr),
$$

$$
\Gamma=D^{-1/2}\left(D^{1/2}\Sigma D^{1/2}\right)^{1/2}D^{-1/2}.
$$

Then, asymptotically,

$$
\frac{\theta(t,q)-\theta(t,q+\Delta_ie_i)}{\Delta_i}
\simeq
\sqrt{\frac\gamma2}\left[
\Gamma_{ii}\frac{2q^i+\Delta_i}{2}
+\sum_{j\ne i}\Gamma_{ij}q^j
\right],
$$

$$
\frac{\theta(t,q)-\theta(t,q-\Delta_ie_i)}{\Delta_i}
\simeq
-\sqrt{\frac\gamma2}\left[
\Gamma_{ii}\frac{2q^i-\Delta_i}{2}
+\sum_{j\ne i}\Gamma_{ij}q^j
\right].
$$

### Equations (5.18)–(5.20) — multi-asset quote approximations

$$
\boxed{
\delta_t^{i,b*}\simeq\delta_{\mathrm{approx}}^{i,b*}(q_{t^-})
:=\tilde\delta_\xi^{i*}\!\left(
\sqrt{\frac\gamma2}\left[
\Gamma_{ii}\frac{2q_{t^-}^i+\Delta_i}{2}
+\sum_{j\ne i}\Gamma_{ij}q_{t^-}^j
\right]
\right)
}
\tag{5.18}
$$

$$
\boxed{
\delta_t^{i,a*}\simeq\delta_{\mathrm{approx}}^{i,a*}(q_{t^-})
:=\tilde\delta_\xi^{i*}\!\left(
-\sqrt{\frac\gamma2}\left[
\Gamma_{ii}\frac{2q_{t^-}^i-\Delta_i}{2}
+\sum_{j\ne i}\Gamma_{ij}q_{t^-}^j
\right]
\right)
}
\tag{5.19}
$$

where

$$
\boxed{
\tilde\delta_\xi^{i*}(p)=(\Lambda^i)^{-1}\!\left(
\xi H_\xi^i(p)-\frac{{H_\xi^i}'(p)}{\Delta_i}
\right)
}
\tag{5.20}
$$

## Practical calibration in Section 6

The paper's numerical application uses two credit indices with parameters listed in `tables.md`. The main risk-management point is that the cross terms `\Gamma_{ij}` make the quote for asset `i` depend on inventories in correlated assets `j`, not only on `q^i`.
