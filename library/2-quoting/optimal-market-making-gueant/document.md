---
title: "Optimal market making"
author: "Olivier Guéant"
arxiv: "1605.01862v5"
version_date: "2017-05-06"
format: "agent-optimized Markdown"
---

# Optimal market making

**Olivier Guéant**  
**arXiv:1605.01862v5, 6 May 2017**
**Tags: EXEC,MARKET-MAKING,RISK**

> **Agent edition.** This file is a clean, source-faithful reading version of the paper. The complete normalized mathematical reference is in [`equations.md`](equations.md); the calibrated parameters of the numerical application are in [`tables.md`](tables.md). The proof pages that `equations.md` deliberately does not re-key are kept as rendered images under `source_pages/`.

## Abstract

Market makers provide liquidity to other market participants by proposing prices at which they stand ready to buy and sell assets. Their optimization problem has both static and dynamic components. They seek to earn the bid-ask spread while controlling the risk created by long and short inventories. The paper develops a general framework that extends and reconciles models proposed after Avellaneda and Stoikov; proves existence and characterization results for optimal strategies; derives new closed-form approximations; extends the model to multi-asset market making; and applies the framework to two credit indices.

**Key words:** Market making; stochastic optimal control; closed-form approximations; Guéant-Lehalle-Fernandez-Tapia formulas; CDX indices.

# 1. Introduction

A market maker is a liquidity provider. In modern electronic markets, the exact institutional meaning varies. Some market makers have formal obligations to exchanges, while others - including high-frequency firms - provide liquidity voluntarily because the strategy is profitable. In quote-driven markets, such as corporate bonds, dealers provide bid and offer prices to clients, with the exact quotation protocol depending on the market.

The problem studied here is the determination of bid and ask quotes for an agent or algorithm that is ready to buy or sell one or several assets. The model abstracts from contractual quoting constraints and treats quoted prices as firm for a fixed trade size.

The optimization problem combines two effects. First is a **static margin-volume trade-off**: a wide spread produces a high profit per trade but a low execution rate, whereas a narrow spread produces a lower profit per trade but more executions. Second is a **dynamic inventory-risk problem**: a long market maker should quote conservatively on the bid and aggressively on the ask to encourage inventory reduction; a short market maker should do the opposite.

The model follows the Avellaneda-Stoikov tradition: the reference price is exogenous, and execution probabilities depend on the distance between a market maker's quote and that reference price. Unlike the earliest versions of the model, this paper allows general intensity functions instead of restricting attention to exponential intensities.

Two classical objective functions are brought into a single mathematical framework. The first uses CARA expected utility of terminal mark-to-market wealth (Model A). The second maximizes expected mark-to-market wealth minus a running inventory penalty (Model B). A key contribution is to show that the apparently different HJB equations reduce to the same family of ODE systems, with a parameter `\xi` controlling aversion to non-execution risk.

The paper then derives almost-closed-form and closed-form approximations, extends the model to multiple correlated assets, and demonstrates the practical effect of correlations using CDX.NA.IG and CDX.NA.HY.

# 2. Modeling framework and notations

## 2.1 Single-asset state variables

The reference price follows an arithmetic Brownian motion:

$$
dS_t=\sigma\,dW_t.
$$

The market maker posts a bid `S_t^b` and an ask `S_t^a`. Trades occur in fixed size `\Delta`. Bid-side and ask-side transaction counters are `N_t^b` and `N_t^a`, so inventory evolves as

$$
dq_t=\Delta\,dN_t^b-\Delta\,dN_t^a.
$$

Quote distances from the reference price are

$$
\delta_t^b=S_t-S_t^b,
\qquad
\delta_t^a=S_t^a-S_t.
$$

The market maker is subject to an inventory limit `Q`. Execution intensities are

$$
\lambda_t^b=\Lambda^b(\delta_t^b)\mathbf 1_{\{q_{t^-}<Q\}},
\qquad
\lambda_t^a=\Lambda^a(\delta_t^a)\mathbf 1_{\{q_{t^-}>-Q\}}.
$$

The paper assumes `\Lambda^b` and `\Lambda^a` are decreasing, twice continuously differentiable, vanish as `\delta\to+\infty`, and satisfy a curvature condition ensuring a unique optimal quote for the instantaneous quoting problem.

Cash evolves according to

$$
\begin{aligned}
dX_t
&=S_t^a\Delta\,dN_t^a-S_t^b\Delta\,dN_t^b\\
&=(S_t+\delta_t^a)\Delta\,dN_t^a-(S_t-\delta_t^b)\Delta\,dN_t^b.
\end{aligned}
$$

For the complete normalized equations and the technical condition on `\Lambda`, see [Equations (2.1)-(2.4)](equations.md#2-modeling-framework).

## 2.2 The two classical optimization problems

### Model A - CARA utility

The first objective is

$$
\sup_{\delta^b,\delta^a}
\mathbb E\left[-\exp\left(-\gamma\left(X_T+q_TS_T-\ell(|q_T|)\right)\right)\right],
$$

where `\ell` is a nondecreasing convex terminal inventory/liquidity penalty.

### Model B - expected PnL with running inventory penalty

The second objective is

$$
\sup_{\delta^b,\delta^a}
\mathbb E\left[
X_T+q_TS_T-\ell(|q_T|)
-\frac12\gamma\sigma^2\int_0^T q_t^2\,dt
\right].
$$

Model A applies CARA risk aversion to both price risk and execution uncertainty. Model B penalizes inventory exposure directly and does not apply risk aversion to execution uncertainty in the same way.

# 3. A single ODE framework for optimal quotes

## 3.1 Reduction from four state variables to two

The original control problem uses time `t`, cash `x`, inventory `q`, and reference price `S`. The paper shows that the HJB dimensionality can be reduced by factoring out the mark-to-market component.

For Model A, use

$$
u(t,x,q,S)=-\exp\bigl(-\gamma(x+qS+\theta(t,q))\bigr).
$$

For Model B, use

$$
u(t,x,q,S)=x+qS+\theta(t,q).
$$

Both models then reduce to the unified system

$$
\begin{aligned}
0={}&-\partial_t\theta(t,q)+\frac12\gamma\sigma^2q^2\\
&-\mathbf 1_{\{q<Q\}}H_\xi^b\left(\frac{\theta(t,q)-\theta(t,q+\Delta)}{\Delta}\right)\\
&-\mathbf 1_{\{q>-Q\}}H_\xi^a\left(\frac{\theta(t,q)-\theta(t,q-\Delta)}{\Delta}\right),
\end{aligned}
$$

with terminal condition

$$
\theta(T,q)=-\ell(|q|).
$$

Model A is recovered with `\xi=\gamma`; Model B with `\xi=0`.

For `\xi>0`, the Hamiltonians are

$$
H_\xi^b(p)=\sup_\delta\frac{\Lambda^b(\delta)}{\xi}
\left(1-e^{-\xi\Delta(\delta-p)}\right),
\qquad
H_\xi^a(p)=\sup_\delta\frac{\Lambda^a(\delta)}{\xi}
\left(1-e^{-\xi\Delta(\delta-p)}\right),
$$

and at `\xi=0` they become the linear limits

$$
H_0^b(p)=\Delta\sup_\delta\Lambda^b(\delta)(\delta-p),
\qquad
H_0^a(p)=\Delta\sup_\delta\Lambda^a(\delta)(\delta-p).
$$

This is Equation (3.9) in the paper. The full HJBs for both models are transcribed in [`equations.md`](equations.md#3-unified-ode-characterization).

## 3.2 Existence, uniqueness, and optimal single-period offsets

**Lemma 3.1** shows that, for all `\xi\ge0`, the Hamiltonians `H_\xi^b` and `H_\xi^a` are decreasing `C^2` functions and the maximizers are unique. On the bid side, the optimal one-step offset can be written as

$$
\tilde\delta_\xi^{b*}(p)
=(\Lambda^b)^{-1}\left(\xi H_\xi^b(p)-\frac{{H_\xi^b}'(p)}{\Delta}\right),
$$

and similarly on the ask side.

**Lemma 3.2** establishes a comparison principle for the unified ODE system. This provides a priori bounds.

**Theorem 3.1** then proves existence and uniqueness of a `C^1`-in-time solution `\theta` on `[0,T]\times\mathcal Q`.

The paper pays special attention to the classical exponential-intensity case

$$
\Lambda^b(\delta)=\Lambda^a(\delta)=Ae^{-k\delta}.
$$

In that case, the nonlinear ODE system can be transformed into a **linear tridiagonal system** by defining

$$
v_q(t)=\exp\left(\frac{k}{\Delta}\theta(t,q)\right).
$$

The exact linear system is Equation (3.13) in [`equations.md`](equations.md#equation-313--exponential-intensity-linear-system).

## 3.3 Verification and optimal feedback controls

For Model A, **Theorem 3.2** proves that the HJB solution is the value function and that the optimal quote distances are

$$
\delta_t^{b*}=\tilde\delta_\gamma^{b*}\left(
\frac{\theta(t,q_{t^-})-\theta(t,q_{t^-}+\Delta)}{\Delta}
\right),
$$

$$
\delta_t^{a*}=\tilde\delta_\gamma^{a*}\left(
\frac{\theta(t,q_{t^-})-\theta(t,q_{t^-}-\Delta)}{\Delta}
\right).
$$

For Model B, **Theorem 3.3** gives the same feedback form but with `\xi=0`.

The verification proofs apply Itô's formula to jump-diffusion wealth/inventory dynamics, establish the needed integrability, and show that equality holds under the Hamiltonian maximizers. Because these proof displays are long and the PDF text layer is easy to corrupt, their original page images are retained under `source_pages/` rather than re-keyed.

## 3.4 Interpretation of `\xi`

The common ODE structure makes the difference between the two objective functions explicit. The term

$$
\frac12\gamma\sigma^2q^2
$$

captures price-risk aversion in both models. Model A also applies risk aversion to uncertainty about whether trades occur. The auxiliary parameter `\xi` can therefore be interpreted as a parameter governing **non-execution risk**: `\xi=\gamma` in Model A and `\xi=0` in Model B.

# 4. Closed-form and almost-closed-form approximations

## 4.1 Continuous-inventory PDE approximation

Assume symmetric execution intensities `\Lambda^b=\Lambda^a=:\Lambda` and write `H_\xi` for the common Hamiltonian. The discrete inventory variable is heuristically replaced by a continuous variable, producing the PDE

$$
0=-\partial_t\tilde\theta
+\frac12\gamma\sigma^2q^2
-2H_\xi(0)
-H_\xi''(0)(\partial_q\tilde\theta)^2
+\Delta H_\xi'(0)\partial_{qq}^2\tilde\theta.
$$

The exponential transform

$$
\tilde v(t,q)=\exp\left(
-\frac{H_\xi''(0)}{\Delta H_\xi'(0)}\tilde\theta(t,q)
\right)
$$

turns this nonlinear equation into a linear PDE. Spectral arguments then identify the large-horizon behavior.

## 4.2 Generalized Guéant-Lehalle-Fernandez-Tapia formulas

The asymptotic finite differences of `\theta` are approximated by

$$
\frac{\theta(t,q)-\theta(t,q+\Delta)}{\Delta}
\simeq
\frac{2q+\Delta}{2}\sqrt{\frac{\gamma\sigma^2}{2H_\xi''(0)}},
$$

and

$$
\frac{\theta(t,q)-\theta(t,q-\Delta)}{\Delta}
\simeq
-\frac{2q-\Delta}{2}\sqrt{\frac{\gamma\sigma^2}{2H_\xi''(0)}}.
$$

These approximations are then passed through the one-step optimizer `\tilde\delta_\xi^*` to obtain the approximate optimal bid and ask quotes. In the exponential-intensity case, they become explicit formulas. The full expressions are Equations (4.3)-(4.9) in [`equations.md`](equations.md#equations-43-45--general-quote-approximations).

A particularly useful consequence is that, under exponential intensities, the approximation has an inventory-independent spread and a skew linear in inventory. The numerical section later shows that this is only approximate: the true spread is not exactly constant in inventory, and the true skew is not exactly linear.

## 4.3 Comparative statics and economic interpretation

The approximations make several effects transparent:

- Increasing inventory shifts both quotes in the direction that encourages reversion toward a flat inventory.
- For zero inventory, increasing volatility widens the spread symmetrically.
- For a positive inventory, increasing volatility lowers both bid and ask quotes, increasing the inventory-reducing skew in absolute value; the opposite occurs for a negative inventory.
- Multiplying execution intensities by a liquidity factor `\beta>0` is equivalent, in these approximations, to dividing `\sigma^2` by `\beta`. More liquidity acts like less volatility.
- In Model B, increasing `\gamma` acts like increasing volatility because `\gamma` only penalizes inventory exposure.
- In Model A, risk aversion has two competing effects: a static execution-uncertainty effect that can encourage narrower spreads, and a dynamic inventory-risk effect that encourages wider spreads when adverse price moves cannot be unwound quickly enough.

# 5. Multi-asset market making strategies

## 5.1 Multi-asset dynamics

The model is extended to `d` assets. Asset `i` follows

$$
dS_t^i=\sigma^i\,dW_t^i,
$$

where the Brownian vector has covariance matrix

$$
\Sigma=(\rho^{i,j}\sigma^i\sigma^j)_{1\le i,j\le d}.
$$

Inventory in each asset evolves as

$$
dq_t^i=\Delta_i\,dN_t^{i,b}-\Delta_i\,dN_t^{i,a}.
$$

Each asset has its own bid and ask intensity functions and inventory bounds. Cash is the sum of cashflows across all assets.

The multi-asset versions of Models A and B replace the one-dimensional inventory-risk term by the portfolio quadratic form

$$
\sum_{i=1}^d\sum_{j=1}^d\rho^{i,j}\sigma^i\sigma^j q_t^iq_t^j.
$$

## 5.2 Unified multi-asset ODE system

After the same change of variables as in the single-asset case, both objective functions are again reduced to a common ODE system:

$$
\begin{aligned}
0={}&-\partial_t\theta(t,q)
+\frac12\gamma\sum_{i,j=1}^d\rho^{i,j}\sigma^i\sigma^j q^iq^j\\
&-\sum_{i=1}^d\mathbf1_{\{q^i<Q_i\}}H_\xi^{i,b}\left(
\frac{\theta(t,q)-\theta(t,q+\Delta_ie_i)}{\Delta_i}
\right)\\
&-\sum_{i=1}^d\mathbf1_{\{q^i>-Q_i\}}H_\xi^{i,a}\left(
\frac{\theta(t,q)-\theta(t,q-\Delta_ie_i)}{\Delta_i}
\right).
\end{aligned}
$$

The terminal condition is `\theta(T,q)=-\ell_d(q)`.

**Theorem 5.1** proves existence and uniqueness. **Theorem 5.2** characterizes the optimal quotes for Model A (`\xi=\gamma`) and **Theorem 5.3** does the same for Model B (`\xi=0`).

For asset `i`, the optimal bid and ask offsets depend on the finite difference of `\theta` in the `i`-th inventory direction. This already shows why optimal quoting in one asset depends on the entire portfolio when prices are correlated.

## 5.3 Multi-asset closed-form approximation

Assuming symmetric bid/ask intensity functions per asset, the paper introduces a multidimensional PDE approximation. For a quadratic terminal penalty, the approximate solution is quadratic in the inventory vector.

Define

$$
D=\operatorname{diag}\bigl({H_\xi^1}''(0),\ldots,{H_\xi^d}''(0)\bigr)
$$

and

$$
\Gamma=D^{-1/2}\left(D^{1/2}\Sigma D^{1/2}\right)^{1/2}D^{-1/2}.
$$

The approximate finite differences become

$$
\frac{\theta(t,q)-\theta(t,q+\Delta_ie_i)}{\Delta_i}
\simeq
\sqrt{\frac\gamma2}
\left[
\Gamma_{ii}\frac{2q^i+\Delta_i}{2}
+\sum_{j\ne i}\Gamma_{ij}q^j
\right],
$$

and similarly with the opposite sign for the ask side.

The off-diagonal elements `\Gamma_{ij}` are the key multi-asset terms: the quote in asset `i` reacts to inventory in correlated assets `j`. The full approximations are Equations (5.18)-(5.20) in [`equations.md`](equations.md#equations-518-520--multi-asset-quote-approximations).

# 6. Application: two credit indices

The paper applies the framework to two credit indices: CDX.NA.IG (investment grade) and CDX.NA.HY (high yield). The application focuses on spread risk and ignores default risk, consistent with the practical market-making simplification described by the author.

The relevant calibrated parameters and conventions are summarized in [`tables.md`](tables.md). The paper uses first-semester 2016 data supplied by BNP Paribas. Volatility and correlation are estimated from mid-prices; exponential-intensity parameters are estimated from real bank quotes and client trades.

The paper sets trade sizes to `$50 million` for IG and `$10 million` for HY, takes a reference risk-aversion value `\gamma=6\times10^{-5}\,$^{-1}`, uses inventory limits of four trade units in each index, and sets `T=7200` seconds. The numerical solution of the ODEs is obtained with an implicit scheme and Newton iterations.

## 6.1 IG index on a stand-alone basis

The asymptotic regime is reached in less than one hour. Numerical quotes have the expected inventory behavior: long inventory produces a conservative bid and aggressive ask; short inventory produces the reverse.

The closed-form approximations are satisfactory for small inventory magnitudes but become noticeably less accurate for larger positions. The numerical bid-ask spread is not constant in inventory, and the numerical skew is not perfectly linear. When volatility is reduced by half, the approximation improves substantially.

The paper also compares Model A and Model B. For this calibration, the differences are small, making Model B an attractive simplification even though it omits aversion to non-execution risk.

### Figure 1

![Convergence of the IG bid quote](assets/figure-01.png)

### Figure 2

![IG bid quote and closed-form approximation](assets/figure-02.png)

### Figure 3

![IG ask quote and closed-form approximation](assets/figure-03.png)

### Figure 4

![IG bid-ask spread and approximation](assets/figure-04.png)

### Figure 5

![IG skew and approximation](assets/figure-05.png)

### Figure 6

![IG bid quote with volatility reduced by half](assets/figure-06.png)

### Figure 7

![IG ask quote with volatility reduced by half](assets/figure-07.png)

### Figure 8

![IG bid quote: Model A versus Model B](assets/figure-08.png)

### Figure 9

![IG ask quote: Model A versus Model B](assets/figure-09.png)

## 6.2 HY index on a stand-alone basis

The HY index shows the same qualitative behavior. Its asymptotic regime is reached after roughly one hour. Again, closed-form approximations are most reliable for small inventories, while the exact numerical spread and skew deviate from the constant-spread/linear-skew approximation at larger positions.

Model A and Model B again produce very similar quotes for the calibration used in the paper.

### Figure 10

![Convergence of the HY bid quote](assets/figure-10.png)

### Figure 11

![HY bid quote and closed-form approximation](assets/figure-11.png)

### Figure 12

![HY ask quote and closed-form approximation](assets/figure-12.png)

### Figure 13

![HY bid-ask spread and approximation](assets/figure-13.png)

### Figure 14

![HY skew and approximation](assets/figure-14.png)

### Figure 15

![HY bid quote: Model A versus Model B](assets/figure-15.png)

### Figure 16

![HY ask quote: Model A versus Model B](assets/figure-16.png)

## 6.3 Joint IG/HY market making and correlation

When the two indices are treated jointly, each index's optimal quote depends on both inventories. Because the estimated correlation is positive, both IG and HY bid offsets increase with both `q^{IG}` and `q^{HY}`.

The effect of correlation is economically important. Holding HY inventory fixed at zero, the HY bid quote becomes increasingly sensitive to IG inventory as `\rho` rises. The more positively correlated the two assets are, the more conservatively the market maker should quote HY at the bid when long IG, and the more aggressively when short IG.

### Figure 17

![Multi-asset optimal IG bid quote surface](assets/figure-17.png)

### Figure 18

![Multi-asset optimal HY bid quote surface](assets/figure-18.png)

### Figure 19

![Correlation effect on HY bid quote](assets/figure-19.png)

# Conclusion

The paper develops an Avellaneda-Stoikov-style framework with general intensity functions and shows that two major classes of objective functions can be reduced from four-dimensional HJB equations to lower-dimensional ODE systems. It derives general closed-form or almost-closed-form approximations that extend the Guéant-Lehalle-Fernandez-Tapia formulas beyond exponential intensities and beyond a single objective function.

The multi-asset extension is especially important in practice. Correlated inventories should not be managed independently: optimal quotes for one asset depend on inventory held in other correlated assets. The CDX example illustrates that the effect can be material and that the approximate formulas can be useful when solving large nonlinear ODE systems is computationally expensive.

# References

1. M. Avellaneda and S. Stoikov. *High-frequency trading in a limit order book*. Quantitative Finance 8(3):217-224, 2008.
2. E. Bayraktar and M. Ludkovski. *Liquidation in limit order books with controlled intensity*. Mathematical Finance 24(4):627-650, 2014.
3. H. Brezis. *Functional analysis, Sobolev spaces and partial differential equations*. Springer, 2010.
4. Á. Cartea, R. Donnelly, and S. Jaimungal. *Algorithmic trading with model uncertainty*. SSRN 2310645, 2013.
5. Á. Cartea and S. Jaimungal. *Risk metrics and fine tuning of high frequency trading strategies*. Mathematical Finance 25(3):576-611, 2013.
6. Á. Cartea, S. Jaimungal, and J. Ricci. *Buy low, sell high: A high frequency trading perspective*. SIAM Journal on Financial Mathematics 5(1):415-444, 2014.
7. Á. Cartea, S. Jaimungal, and J. Penalva. *Algorithmic and High-Frequency Trading*. Cambridge University Press, 2015.
8. R. Donnelly. *Ambiguity aversion in algorithmic and high frequency trading*. PhD thesis, 2014.
9. D. Evangelista, O. Guéant, and D. Vieira. *New closed-form approximations in multi-asset market making*. Preprint, 2017.
10. P. Fodra and M. Labadie. *High-frequency market-making with inventory constraints and directional bets*. arXiv:1206.4810, 2012.
11. S. Grossman and M. Miller. *Liquidity and market structure*. Journal of Finance 43(3):617-633, 1988.
12. O. Guéant, C.-A. Lehalle, and J. Fernandez-Tapia. *Optimal portfolio liquidation with limit orders*. SIAM Journal on Financial Mathematics 3(1):740-764, 2012.
13. O. Guéant, C.-A. Lehalle, and J. Fernandez-Tapia. *Dealing with the inventory risk: a solution to the market making problem*. Mathematics and Financial Economics 7(4):477-507, 2013.
14. O. Guéant and C.-A. Lehalle. *General intensity shapes in optimal liquidation*. Mathematical Finance 25(3):457-495, 2015.
15. O. Guéant. *The Financial Mathematics of Market Liquidity: from Optimal Execution to Market Making*. CRC Press, 2016.
16. F. Guilbaud and H. Pham. *Optimal high-frequency trading with limit and market orders*. Quantitative Finance 13(1):79-94, 2013.
17. T. Ho and H. Stoll. *Optimal dealer pricing under transactions and return uncertainty*. Journal of Financial Economics 9(1):47-73, 1981.
18. T. Ho and H. Stoll. *The dynamics of dealer markets under competition*. Journal of Finance 38(4):1053-1074, 1983.
19. R. Huitema. *Optimal portfolio execution using market and limit orders*. Working paper, 2012.
20. A. Menkveld. *High frequency trading and the new market makers*. Journal of Financial Markets 16(4):712-740, 2013.
21. K. Nyström, S. M. Ould Aly, and C. Zhang. *Market making and portfolio liquidation under uncertainty*. International Journal of Theoretical and Applied Finance, 2014.

# Source-verification policy

The paper contains several pages of long proof-only stochastic-calculus identities. They are retained as rendered source pages instead of being silently re-keyed from an ambiguous PDF text layer. When a proof step that is not in the normalized equation sheet is needed, read it off the corresponding page image in `source_pages/`; for anything beyond the pages kept here, fetch the source from arXiv:1605.01862v5.
