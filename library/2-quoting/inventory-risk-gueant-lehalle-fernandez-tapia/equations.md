# Equation index

This is a retrieval-oriented companion to `document.md`. It collects the paper's principal model equations and quote formulas in clean LaTeX.

## Base model

Reference price:

$$
dS_t=\sigma\,dW_t.
$$

Inventory:

$$
q_t=N_t^b-N_t^a.
$$

Quote distances:

$$
\delta_t^b=S_t-S_t^b,
\qquad
\delta_t^a=S_t^a-S_t.
$$

Execution intensities:

$$
\lambda^b(\delta^b)=Ae^{-k\delta^b},
\qquad
\lambda^a(\delta^a)=Ae^{-k\delta^a}.
$$

Cash dynamics:

$$
dX_t=(S_t+\delta_t^a)dN_t^a-(S_t-\delta_t^b)dN_t^b.
$$

Objective:

$$
\sup_{\delta^a,\delta^b}
\mathbb E\left[-e^{-\gamma(X_T+q_TS_T)}\right].
$$

## HJB transform

Parameters:

$$
\alpha=\frac{k}{2}\gamma\sigma^2,
\qquad
\eta=A\left(1+\frac\gamma k\right)^{-\left(1+\frac{k}{\gamma}\right)}.
$$

Interior ODE:

$$
\dot v_q=\alpha q^2v_q-\eta(v_{q-1}+v_{q+1}).
$$

Value function:

$$
u(t,x,q,s)=-e^{-\gamma(x+qs)}v_q(t)^{-\gamma/k}.
$$

Matrix solution:

$$
\mathbf v(t)=e^{-M(T-t)}\mathbf 1,
$$

with $M_{q,q}=\alpha q^2$ and $M_{q,q\pm1}=-\eta$.

## Optimal quotes

$$
\delta^{b*}(t,q)
=\frac1k\ln\frac{v_q(t)}{v_{q+1}(t)}
+\frac1\gamma\ln\left(1+\frac\gamma k\right),
$$

$$
\delta^{a*}(t,q)
=\frac1k\ln\frac{v_q(t)}{v_{q-1}(t)}
+\frac1\gamma\ln\left(1+\frac\gamma k\right),
$$

$$
\psi^*(t,q)
=-\frac1k\ln\frac{v_{q+1}(t)v_{q-1}(t)}{v_q(t)^2}
+\frac2\gamma\ln\left(1+\frac\gamma k\right).
$$

## Asymptotic eigenvector form

If $f^0$ is the eigenvector corresponding to the smallest eigenvalue of $M$,

$$
\delta_\infty^{b*}(q)
=\frac1\gamma\ln\left(1+\frac\gamma k\right)
+\frac1k\ln\frac{f_q^0}{f_{q+1}^0},
$$

$$
\delta_\infty^{a*}(q)
=\frac1\gamma\ln\left(1+\frac\gamma k\right)
+\frac1k\ln\frac{f_q^0}{f_{q-1}^0},
$$

$$
\psi_\infty^*(q)
=-\frac1k\ln\frac{f_{q+1}^0f_{q-1}^0}{(f_q^0)^2}
+\frac2\gamma\ln\left(1+\frac\gamma k\right).
$$

Rayleigh characterization:

$$
\min_{\|f\|_2=1}
\left[
\sum_{q=-Q}^{Q}\alpha q^2f_q^2
+\eta\sum_{q=-Q}^{Q-1}(f_{q+1}-f_q)^2
+\eta f_Q^2+\eta f_{-Q}^2
\right].
$$

Continuous approximation:

$$
\min_{\|\widetilde f\|_2=1}
\int_{\mathbb R}
\left(\alpha x^2\widetilde f(x)^2+\eta\widetilde f'(x)^2\right)dx.
$$

Gaussian minimizer:

$$
\widetilde f^0(x)=\pm\pi^{-1/4}\left(\frac\alpha\eta\right)^{1/8}
\exp\left(-\frac12\sqrt{\frac\alpha\eta}\,x^2\right).
$$

Define

$$
C=\sqrt{
\frac{\sigma^2\gamma}{2kA}
\left(1+\frac\gamma k\right)^{1+k/\gamma}
}.
$$

Closed-form asymptotic quote approximation:

$$
\delta_\infty^{b*}(q)
\simeq \frac1\gamma\ln\left(1+\frac\gamma k\right)+\frac{2q+1}{2}C,
$$

$$
\delta_\infty^{a*}(q)
\simeq \frac1\gamma\ln\left(1+\frac\gamma k\right)-\frac{2q-1}{2}C,
$$

$$
\psi_\infty^*(q)
\simeq \frac2\gamma\ln\left(1+\frac\gamma k\right)+C.
$$

## Drift extension

$$
dS_t=\mu\,dt+\sigma\,dW_t,
\qquad \beta=k\mu.
$$

$$
\dot v_q=(\alpha q^2-\beta q)v_q-\eta(v_{q-1}+v_{q+1}).
$$

$$
\delta_\infty^{b*}(q)
\simeq \frac1\gamma\ln\left(1+\frac\gamma k\right)
+\left[-\frac\mu{\gamma\sigma^2}+\frac{2q+1}{2}\right]C,
$$

$$
\delta_\infty^{a*}(q)
\simeq \frac1\gamma\ln\left(1+\frac\gamma k\right)
+\left[\frac\mu{\gamma\sigma^2}-\frac{2q-1}{2}\right]C.
$$

## Market-impact extension

$$
dS_t=\sigma\,dW_t+\xi\,dN_t^a-\xi\,dN_t^b.
$$

$$
\dot v_q
=\alpha q^2v_q-\eta e^{-k\xi/2}(v_{q-1}+v_{q+1}),
$$

$$
v_q(T)=e^{-k\xi q^2/2}.
$$

$$
u(t,x,q,s)=-\exp\left[-\gamma\left(x+qs+\frac12\xi q^2\right)\right]v_q(t)^{-\gamma/k}.
$$

$$
\delta^{b*}
=\frac1k\ln\frac{v_q}{v_{q+1}}+\frac\xi2+\frac1\gamma\ln\left(1+\frac\gamma k\right),
$$

$$
\delta^{a*}
=\frac1k\ln\frac{v_q}{v_{q-1}}+\frac\xi2+\frac1\gamma\ln\left(1+\frac\gamma k\right),
$$

$$
\psi^*
=-\frac1k\ln\frac{v_{q+1}v_{q-1}}{v_q^2}+\xi+\frac2\gamma\ln\left(1+\frac\gamma k\right).
$$

With $C_\xi=e^{k\xi/4}C$,

$$
\delta_\infty^{b*}\simeq \frac1\gamma\ln\left(1+\frac\gamma k\right)+\frac\xi2+\frac{2q+1}{2}C_\xi,
$$

$$
\delta_\infty^{a*}\simeq \frac1\gamma\ln\left(1+\frac\gamma k\right)+\frac\xi2-\frac{2q-1}{2}C_\xi,
$$

$$
\psi_\infty^*\simeq \frac2\gamma\ln\left(1+\frac\gamma k\right)+\xi+C_\xi.
$$
