---
title: "Dealing with the Inventory Risk: A solution to the market making problem"
authors:
  - Olivier Guéant
  - Charles-Albert Lehalle
  - Joaquin Fernandez-Tapia
date: "July 2012"
arxiv: "1105.3115v5"
subject: "q-fin.TR"
source_pdf: "1105.3115v5.pdf"
conversion: "Agent-friendly Markdown with LaTeX equations and extracted figures"
---

# Dealing with the Inventory Risk

## A solution to the market making problem

**Olivier Guéant · Charles-Albert Lehalle · Joaquin Fernandez-Tapia**  
**This draft: July 2012**
**Tags: EXEC,MARKET-MAKING,RISK**

## Abstract

Market makers continuously set bid and ask quotes for the stocks they have under consideration. Hence they face a complex optimization problem in which their return, based on the bid-ask spread they quote and the frequency at which they indeed provide liquidity, is challenged by the price risk they bear due to their inventory. In this paper, the authors consider a stochastic control problem similar to the one introduced by Ho and Stoll and formalized mathematically by Avellaneda and Stoikov. The market is modeled using a reference price $S_t$ following a Brownian motion with standard deviation $\sigma$; arrival rates of buy or sell liquidity-consuming orders depend on the distance to the reference price $S_t$; and a market maker maximizes the expected utility of its P&L over a finite time horizon. The Hamilton-Jacobi-Bellman equations associated with the stochastic optimal control problem are transformed into a system of linear ordinary differential equations, and the market making problem is solved under inventory constraints. The paper also studies the asymptotic behavior of the optimal quotes and proposes closed-form approximations based on a spectral characterization of the optimal quotes.

**Keywords:** Stochastic optimal control · High-frequency Market Making · Avellaneda-Stoikov problem

> This research was conducted within the Research Initiative “Microstructure des Marchés Financiers” under the aegis of the Europlace Institute of Finance.

# 1. Introduction

From a quantitative viewpoint, market microstructure is a sequence of auction games between market participants. It implements the balance between supply and demand, forming an equilibrium traded price to be used as reference for valuation. The rule of each auction game (fixing auction, continuous auction, etc.) is fixed by the firm operating each trading venue. Nevertheless, most electronic trading mechanisms rely on market participants sending orders to a queuing system where their open interests are consolidated as liquidity provision or form transactions [1]. The efficiency of such a process relies on adequate timing between buyers and sellers, so as to avoid too many non-informative oscillations of the transaction price [20].

In practice, it is possible to provide liquidity to an impatient buyer (respectively seller) and maintain an inventory until the arrival of the next impatient seller (respectively buyer). Market participants focused on this liquidity-providing activity are called **market makers**. On one hand they buy at the bid price and sell at the ask price they choose, making money from the bid-ask spread. On the other hand, their inventory is exposed to price fluctuations mainly driven by market volatility [2,5,10,11,18,24].

The evolution of technology and market regulation reshaped interactions during continuous electronic auctions, one consequence being the emergence of high-frequency market makers. The paper notes estimates that they were involved in roughly 70% of electronic trades in the US, 40% in the EU and 35% in Japan, with a massively passive (liquidity-providing) behavior and a typical balance around 80% passive interactions [22].

From a mathematical modeling point of view, the market-making problem is the choice of optimal bid and ask quotes, taking into account inventory limits and risk constraints often represented by a utility function [9,16,19,21,23,25].

Avellaneda and Stoikov [3], building on Ho and Stoll [17], model a reference or fair price $S_t$ as a Brownian motion with standard deviation $\sigma$. The arrival of a liquidity-consuming order at distance $\delta$ from the reference price is described by a point process with intensity

$$
A e^{-k\delta},
$$

where $A$ and $k$ are positive constants characterizing the stock's liquidity.

The present paper uses the same model but adds inventory limits. Its main technical contribution is a change of variables that reduces the HJB equations to a system of **linear ODEs**. This avoids numerical approximation of a PDE, enables analysis of the asymptotic behavior of the optimal quotes, and leads to a spectral closed-form approximation. The authors also provide a verification theorem in the inventory-constrained model.

The paper also discusses related extensions in the literature, including richer market-order dynamics, market impact, adverse selection, predictable alpha, Hidden Markov price dynamics, stochastic spreads, and pro-rata microstructures [6-8,14,15]. Similar controlled-intensity models have also been used for optimal execution [4,12].

The remaining sections set up the model, characterize the optimal quotes, study their asymptotics, add drift and market impact, carry out comparative statics, and present a historical backtest. The paper states that adaptations of the results were in use at Cheuvreux.

# 2. Setup of the model

Fix a probability space $(\Omega,\mathcal F,\mathbb P)$ equipped with a filtration $(\mathcal F_t)_{t\ge 0}$ satisfying the usual conditions. All random variables and stochastic processes are defined on this filtered probability space.

A high-frequency market maker operates on a single stock. The mid-price, or more generally a reference price, follows an arithmetic Brownian motion:

$$
dS_t = \sigma\,dW_t.
$$

The market maker continuously proposes bid and ask prices $S_t^b$ and $S_t^a$. His signed inventory is

$$
q_t = N_t^b - N_t^a,
$$

where $N^b$ and $N^a$ are point processes, independent of $W$, counting shares bought and sold by the market maker. Transactions are assumed to have a constant size, scaled to $1$.

Define quote distances from the reference price by

$$
\delta_t^b = S_t-S_t^b,
\qquad
\delta_t^a = S_t^a-S_t.
$$

Following Avellaneda-Stoikov, the execution intensities are exponential:

$$
\lambda^b(\delta^b)=A e^{-k\delta^b},
\qquad
\lambda^a(\delta^a)=A e^{-k\delta^a}.
$$

For positive quote distances, this means the closer an order is posted to the reference price, the faster it is expected to execute.

The cash process evolves as

$$
dX_t=(S_t+\delta_t^a)\,dN_t^a-(S_t-\delta_t^b)\,dN_t^b.
$$

The paper adds a hard inventory bound $Q$. A market maker at inventory $Q$ never posts a bid quote; a market maker at inventory $-Q$ never posts an ask quote. This risk limit is both realistic and crucial for the rigorous solution.

For horizon $T$, the market maker maximizes CARA utility of terminal marked-to-market wealth:

$$
\sup_{(\delta_t^a)_t,(\delta_t^b)_t\in\mathcal A}
\mathbb E\left[-\exp\left(-\gamma(X_T+q_T S_T)\right)\right],
$$

where $\mathcal A$ is the set of predictable controls bounded from below and $\gamma$ is the coefficient of absolute risk aversion.

# 3. Characterization of the optimal quotes

Let $u(t,x,q,s)$ denote the value function. For $|q|<Q$, the HJB equation is

$$
\begin{aligned}
0={}&\partial_t u + \frac{\sigma^2}{2}\,\partial_{ss}^2u \\
&+\sup_{\delta^b}\lambda^b(\delta^b)
\left[u(t,x-s+\delta^b,q+1,s)-u(t,x,q,s)\right]\\
&+\sup_{\delta^a}\lambda^a(\delta^a)
\left[u(t,x+s+\delta^a,q-1,s)-u(t,x,q,s)\right].
\end{aligned}
$$

At the upper inventory boundary $q=Q$, there is no bid term:

$$
\partial_t u + \frac{\sigma^2}{2}\partial_{ss}^2u
+\sup_{\delta^a}\lambda^a(\delta^a)
\left[u(t,x+s+\delta^a,Q-1,s)-u(t,x,Q,s)\right]=0.
$$

At the lower boundary $q=-Q$, there is no ask term:

$$
\partial_t u + \frac{\sigma^2}{2}\partial_{ss}^2u
+\sup_{\delta^b}\lambda^b(\delta^b)
\left[u(t,x-s+\delta^b,-Q+1,s)-u(t,x,-Q,s)\right]=0.
$$

The terminal condition is

$$
u(T,x,q,s)=-\exp[-\gamma(x+qs)],
\qquad q\in\{-Q,\ldots,Q\}.
$$

## Proposition 1 — Change of variables for the HJB system

Let $(v_q)_{|q|\le Q}$ be positive functions satisfying

$$
\dot v_q(t)=\alpha q^2v_q(t)-\eta\bigl(v_{q-1}(t)+v_{q+1}(t)\bigr),
\qquad -Q<q<Q,
$$

with boundary equations

$$
\dot v_Q(t)=\alpha Q^2v_Q(t)-\eta v_{Q-1}(t),
$$

$$
\dot v_{-Q}(t)=\alpha Q^2v_{-Q}(t)-\eta v_{-Q+1}(t),
$$

and terminal values $v_q(T)=1$. Define

$$
\alpha=\frac{k}{2}\gamma\sigma^2,
\qquad
\eta=A\left(1+\frac{\gamma}{k}\right)^{-\left(1+\frac{k}{\gamma}\right)}.
$$

Then

$$
u(t,x,q,s)
=-\exp[-\gamma(x+qs)]\,v_q(t)^{-\gamma/k}
$$

solves the HJB system.

## Proposition 2 — Solution of the ODE system

The matrix printed in the paper is equivalently the tridiagonal matrix indexed by $q=-Q,\ldots,Q$ with

$$
M_{q,q}=\alpha q^2,
\qquad
M_{q,q+1}=M_{q+1,q}=-\eta,
$$

and all other entries zero. If

$$
\mathbf v(t)
=(v_{-Q}(t),\ldots,v_0(t),\ldots,v_Q(t))^\top,
$$

then

$$
\mathbf v(t)=e^{-M(T-t)}\mathbf 1.
$$

This solution is positive componentwise.

## Theorem 1 — Solution of the control problem

The value function is

$$
u(t,x,q,s)=-\exp[-\gamma(x+qs)]\,v_q(t)^{-\gamma/k}.
$$

The optimal bid and ask distances are

$$
\delta^{b*}(t,q)
=\frac{1}{k}\ln\frac{v_q(t)}{v_{q+1}(t)}
+\frac{1}{\gamma}\ln\left(1+\frac{\gamma}{k}\right),
\qquad q\ne Q,
$$

$$
\delta^{a*}(t,q)
=\frac{1}{k}\ln\frac{v_q(t)}{v_{q-1}(t)}
+\frac{1}{\gamma}\ln\left(1+\frac{\gamma}{k}\right),
\qquad q\ne -Q.
$$

Hence the quoted bid-ask spread is

$$
\psi^*(t,q)
=-\frac{1}{k}\ln\left(\frac{v_{q+1}(t)v_{q-1}(t)}{v_q(t)^2}\right)
+\frac{2}{\gamma}\ln\left(1+\frac{\gamma}{k}\right),
\qquad |q|\ne Q.
$$

# 4. Asymptotic behavior and approximation of the optimal quotes

The numerical examples show that optimal quotes become almost independent of time when $t$ is sufficiently far from the terminal horizon $T$. The paper contrasts this with the inventory expansion in Avellaneda-Stoikov, which is a near-terminal-time Taylor approximation:

$$
\delta_t^{b*}\simeq
\frac{1}{\gamma}\ln\left(1+\frac{\gamma}{k}\right)
+\frac{1+2q}{2}\gamma\sigma^2(T-t),
$$

$$
\delta_t^{a*}\simeq
\frac{1}{\gamma}\ln\left(1+\frac{\gamma}{k}\right)
+\frac{1-2q}{2}\gamma\sigma^2(T-t).
$$

![Figure 1 — Behavior of optimal bid quotes with time and inventory](assets/figure-01-optimal-bid.png)

*Figure 1. Behavior of the optimal bid quotes with time and inventory. $\sigma=0.3$ Tick·s$^{-1/2}$, $A=0.9$ s$^{-1}$, $k=0.3$ Tick$^{-1}$, $\gamma=0.01$ Tick$^{-1}$, $T=600$ s.*

![Figure 2 — Behavior of optimal ask quotes with time and inventory](assets/figure-02-optimal-ask.png)

*Figure 2. Behavior of the optimal ask quotes with time and inventory, with the same parameters as Figure 1.*

![Figure 3 — Behavior of resulting bid-ask spread](assets/figure-03-optimal-spread.png)

*Figure 3. Behavior of the resulting bid-ask spread with time and inventory, with the same parameters as Figure 1.*

## Theorem 2 — Asymptotics for the optimal quotes

The optimal quotes have limits

$$
\lim_{T\to\infty}\delta^{b*}(0,q)=\delta_\infty^{b*}(q),
\qquad
\lim_{T\to\infty}\delta^{a*}(0,q)=\delta_\infty^{a*}(q).
$$

Let $f^0\in\mathbb R^{2Q+1}$ be an eigenvector associated with the smallest eigenvalue of $M$. Then

$$
\delta_\infty^{b*}(q)
=\frac{1}{\gamma}\ln\left(1+\frac{\gamma}{k}\right)
+\frac{1}{k}\ln\frac{f_q^0}{f_{q+1}^0},
$$

$$
\delta_\infty^{a*}(q)
=\frac{1}{\gamma}\ln\left(1+\frac{\gamma}{k}\right)
+\frac{1}{k}\ln\frac{f_q^0}{f_{q-1}^0},
$$

and

$$
\psi_\infty^*(q)
=-\frac{1}{k}\ln\left(\frac{f_{q+1}^0f_{q-1}^0}{(f_q^0)^2}\right)
+\frac{2}{\gamma}\ln\left(1+\frac{\gamma}{k}\right).
$$

Up to multiplication by a scalar, $f^0$ is characterized by the Rayleigh minimization

$$
\begin{aligned}
f^0\in\arg\min_{\substack{f\in\mathbb R^{2Q+1}\\\|f\|_2=1}}
\Bigg[
&\sum_{q=-Q}^{Q}\alpha q^2 f_q^2
+\eta\sum_{q=-Q}^{Q-1}(f_{q+1}-f_q)^2\\
&+\eta f_Q^2+\eta f_{-Q}^2
\Bigg].
\end{aligned}
$$

To obtain a closed form, the discrete problem is replaced by the continuous criterion

$$
\widetilde f^0\in
\arg\min_{\|\widetilde f\|_{L^2(\mathbb R)}=1}
\int_{-\infty}^{\infty}
\left(\alpha x^2\widetilde f(x)^2+\eta\widetilde f'(x)^2\right)dx.
$$

## Proposition 3 — Gaussian approximation

A minimizer is

$$
\widetilde f^0(x)
=\pm\frac{1}{\pi^{1/4}}
\left(\frac{\alpha}{\eta}\right)^{1/8}
\exp\left[-\frac12\sqrt{\frac{\alpha}{\eta}}x^2\right].
$$

This motivates the approximation $f_q^0\propto\exp[-\tfrac12\sqrt{\alpha/\eta}\,q^2]$.

Define the common inventory-risk scale

$$
C
=\sqrt{
\frac{\sigma^2\gamma}{2kA}
\left(1+\frac{\gamma}{k}\right)^{1+k/\gamma}
}.
$$

Then the asymptotic quotes are approximated by

$$
\delta_\infty^{b*}(q)
\simeq
\frac{1}{\gamma}\ln\left(1+\frac{\gamma}{k}\right)
+\frac{2q+1}{2}\,C,
$$

$$
\delta_\infty^{a*}(q)
\simeq
\frac{1}{\gamma}\ln\left(1+\frac{\gamma}{k}\right)
-\frac{2q-1}{2}\,C,
$$

$$
\psi_\infty^*(q)
\simeq
\frac{2}{\gamma}\ln\left(1+\frac{\gamma}{k}\right)+C.
$$

![Figure 4 — Asymptotic optimal bid quote and approximation](assets/figure-04-bid-asymptotic-approx.png)

*Figure 4. Asymptotic behavior of the optimal bid quote (bold) and Gaussian approximation (dotted). Left: $\sigma=0.4$, $A=0.9$, $k=0.3$, $\gamma=0.01$, $T=600$ s. Right: $\sigma=1.0$, $A=0.2$, $k=0.3$, $\gamma=0.01$, $T=600$ s (units as in the paper).*

![Figure 5 — Asymptotic optimal ask quote and approximation](assets/figure-05-ask-asymptotic-approx.png)

*Figure 5. Asymptotic behavior of the optimal ask quote (bold) and Gaussian approximation (dotted), with the same two parameter sets as Figure 4.*

The approximations are satisfactory in most cases and particularly good for small inventory $q$. Even if $f^0$ itself is well approximated by a Gaussian, quote errors can be amplified for large $|q|$ because the quotes depend on ratios such as $f_q^0/f_{q+1}^0$ and $f_q^0/f_{q-1}^0$.

# 5. Extensions of the model

## 5.1. A trend in the price dynamics

The reference-price dynamics are extended to

$$
dS_t=\mu\,dt+\sigma\,dW_t.
$$

### Proposition 4 — Solution with a drift

The ODE system becomes

$$
\dot v_q(t)=\left(\alpha q^2-\beta q\right)v_q(t)
-\eta\bigl(v_{q-1}(t)+v_{q+1}(t)\bigr),
\qquad -Q<q<Q,
$$

$$
\dot v_Q(t)=(\alpha Q^2-\beta Q)v_Q(t)-\eta v_{Q-1}(t),
$$

$$
\dot v_{-Q}(t)=(\alpha Q^2+\beta Q)v_{-Q}(t)-\eta v_{-Q+1}(t),
$$

with $v_q(T)=1$ and

$$
\alpha=\frac{k}{2}\gamma\sigma^2,
\qquad
\beta=k\mu,
\qquad
\eta=A\left(1+\frac{\gamma}{k}\right)^{-\left(1+\frac{k}{\gamma}\right)}.
$$

The value function and quote formulas keep the same form as in Theorem 1. The smallest-eigenvalue matrix has diagonal entries $\alpha q^2-\beta q$ and off-diagonal entries $-\eta$.

Using the same Gaussian approximation, the asymptotic quotes become

$$
\delta_\infty^{b*}(q)
\simeq
\frac{1}{\gamma}\ln\left(1+\frac{\gamma}{k}\right)
+\left[-\frac{\mu}{\gamma\sigma^2}+\frac{2q+1}{2}\right]C,
$$

$$
\delta_\infty^{a*}(q)
\simeq
\frac{1}{\gamma}\ln\left(1+\frac{\gamma}{k}\right)
+\left[\frac{\mu}{\gamma\sigma^2}-\frac{2q-1}{2}\right]C,
$$

$$
\psi_\infty^*(q)
\simeq
\frac{2}{\gamma}\ln\left(1+\frac{\gamma}{k}\right)+C.
$$

## 5.2. Market impact / adverse selection

The simplest extension introduces impact directly into the reference price:

$$
dS_t=\sigma\,dW_t+\xi\,dN_t^a-\xi\,dN_t^b,
\qquad \xi>0.
$$

A bid-side fill is followed by a decrease of the reference price and an ask-side fill by an increase. The paper also interprets this dependence as adverse selection.

### Proposition 5 — Solution with market impact

The ODE system becomes

$$
\dot v_q(t)
=\alpha q^2v_q(t)-\eta e^{-k\xi/2}
\bigl(v_{q-1}(t)+v_{q+1}(t)\bigr),
\qquad -Q<q<Q,
$$

with corresponding one-sided boundary equations and terminal values

$$
v_q(T)=\exp\left(-\frac12 k\xi q^2\right).
$$

The value function is

$$
u(t,x,q,s)
=-\exp\left[-\gamma\left(x+qs+\frac12\xi q^2\right)\right]
\,v_q(t)^{-\gamma/k}.
$$

The optimal distances are

$$
\delta^{b*}(t,q)
=\frac1k\ln\frac{v_q(t)}{v_{q+1}(t)}
+\frac\xi2
+\frac1\gamma\ln\left(1+\frac\gamma k\right),
$$

$$
\delta^{a*}(t,q)
=\frac1k\ln\frac{v_q(t)}{v_{q-1}(t)}
+\frac\xi2
+\frac1\gamma\ln\left(1+\frac\gamma k\right),
$$

and

$$
\psi^*(t,q)
=-\frac1k\ln\left(\frac{v_{q+1}(t)v_{q-1}(t)}{v_q(t)^2}\right)
+\xi
+\frac2\gamma\ln\left(1+\frac\gamma k\right).
$$

For the asymptotic approximation, define

$$
C_\xi=e^{k\xi/4}C.
$$

Then

$$
\delta_\infty^{b*}(q)
\simeq
\frac1\gamma\ln\left(1+\frac\gamma k\right)
+\frac\xi2+\frac{2q+1}{2}C_\xi,
$$

$$
\delta_\infty^{a*}(q)
\simeq
\frac1\gamma\ln\left(1+\frac\gamma k\right)
+\frac\xi2-\frac{2q-1}{2}C_\xi,
$$

$$
\psi_\infty^*(q)
\simeq
\frac2\gamma\ln\left(1+\frac\gamma k\right)
+\xi+C_\xi.
$$

# 6. Comparative statics

The asymptotic closed-form approximations give intuition for how the parameters affect quote placement.

## 6.1. Dependence on $\sigma^2$

Numerically, in accordance with the approximations,

$$
\begin{cases}
\partial_{\sigma^2}\delta_\infty^{b*}<0,
\quad \partial_{\sigma^2}\delta_\infty^{a*}>0, & q<0,\\
\partial_{\sigma^2}\delta_\infty^{b*}>0,
\quad \partial_{\sigma^2}\delta_\infty^{a*}>0, & q=0,\\
\partial_{\sigma^2}\delta_\infty^{b*}>0,
\quad \partial_{\sigma^2}\delta_\infty^{a*}<0, & q>0.
\end{cases}
$$

For the spread,

$$
\frac{\partial\psi_\infty^*}{\partial\sigma^2}>0.
$$

An increase in volatility raises inventory risk. A long market maker tries to sell inventory more aggressively while avoiding further purchases; a short market maker does the symmetric thing. Overall, the spread widens with price risk.

## 6.2. Dependence on $\mu$

If the agent expects the price to increase, both quoted prices move higher; if the expected trend is negative, they move lower. In distance form,

$$
\frac{\partial\delta_\infty^{b*}}{\partial\mu}<0,
\qquad
\frac{\partial\delta_\infty^{a*}}{\partial\mu}>0.
$$

## 6.3. Dependence on $A$

The dependence on $A$ is the opposite of the dependence on $\sigma^2$:

$$
\begin{cases}
\partial_A\delta_\infty^{b*}>0,
\quad \partial_A\delta_\infty^{a*}<0, & q<0,\\
\partial_A\delta_\infty^{b*}<0,
\quad \partial_A\delta_\infty^{a*}<0, & q=0,\\
\partial_A\delta_\infty^{b*}<0,
\quad \partial_A\delta_\infty^{a*}>0, & q>0,
\end{cases}
$$

and

$$
\frac{\partial\psi_\infty^*}{\partial A}<0.
$$

A larger $A$ means trades occur more frequently, reducing the risk of remaining stuck with a large inventory.

## 6.4. Dependence on $\gamma$

The dependence on risk aversion is ambiguous because $\gamma$ addresses two risks in opposing ways: randomness of execution can encourage closer quotes, while price risk can encourage a wider spread. The interaction produces the different shapes shown in Figures 6 and 7.

![Figure 6 — Bid-ask spread versus inventory and risk aversion](assets/figure-06-spread-vs-gamma-case1.png)

*Figure 6. Asymptotic bid-ask spread for different inventories and $\gamma$, with $\sigma=0.3$, $A=0.9$, $k=0.3$, $T=600$ s.*

![Figure 7 — Bid-ask spread versus inventory and risk aversion, second parameter set](assets/figure-07-spread-vs-gamma-case2.png)

*Figure 7. Same experiment with $\sigma=0.6$, $A=0.9$, $k=0.9$, $T=600$ s.*

## 6.5. Dependence on $k$

The approximation suggests that $\delta_\infty^{b*}$ is decreasing in $k$ above a negative-inventory threshold and increasing below it; the ask quote behaves symmetrically around a positive threshold. For the spread,

$$
\frac{\partial\psi_\infty^*}{\partial k}<0.
$$

Two effects interact. First, in the absence of inventory risk, increasing $k$ makes executions concentrate closer to the reference price, which tends to shrink the optimal spread. Second, a higher $k$ reduces the probability of execution at positive quote distances and therefore increases inventory risk, somewhat like a decrease in $A$. In the numerical experiment, the first “no-volatility” effect dominates.

![Figure 8 — Asymptotic optimal bid quotes versus k and inventory](assets/figure-08-bid-vs-k.png)

*Figure 8. Asymptotic optimal bid quotes for different inventories and $k$: $\sigma=0.3$, $A=0.9$, $\gamma=0.01$, $T=600$ s.*

## 6.6. Dependence on market impact $\xi$

Market impact has two effects. Even without price risk, the direct adverse-selection effect is approximately to add $\xi/2$ to each quote distance: the market maker roughly maintains profit per round trip but reduces execution probability. The deeper quotes then create a side-effect through inventory risk, because the maker is more likely to remain stuck with inventory.

The decomposition is visible directly in the approximations:

$$
\delta_\infty^{b*}(q)
\simeq
\frac1\gamma\ln\left(1+\frac\gamma k\right)
+\underbrace{\frac\xi2}_{\text{adverse selection}}
+\underbrace{\frac{2q+1}{2}e^{k\xi/4}C}_{\text{inventory-risk side effect}},
$$

$$
\delta_\infty^{a*}(q)
\simeq
\frac1\gamma\ln\left(1+\frac\gamma k\right)
+\underbrace{\frac\xi2}_{\text{adverse selection}}
-\underbrace{\frac{2q-1}{2}e^{k\xi/4}C}_{\text{inventory-risk side effect}}.
$$

# 7. Backtests

Before using the model on historical data, the authors adapt its continuous-time and continuous-price controls to the actual discrete market. Quotes are rounded to the nearest tick. An order of size ATS (average trade size) is sent to the market and is not canceled or modified for a fixed period $\Delta t$, unless a trade occurs and fills it, perhaps partially. Whenever a trade changes inventory, or an order has remained in the book longer than $\Delta t$, the optimal quote is recomputed and, if necessary, a new order is inserted.

The parameters $\sigma$, $A$, and $k$ can be calibrated from trade-by-trade limit-order-book data, while $\gamma$ must be chosen. The authors note that in practice $A$ and $k$ should depend at least on the prevailing market bid-ask spread, although the illustrative backtest keeps them independent of the spread. The backtest chooses $\gamma$ so that inventory remains between approximately $-10$ and $10$ ATS during the day.

The backtest uses trade-by-trade data for France Telecom on March 15, 2012. The paper states that the authors assumed their orders were entirely filled when a trade occurred at or above the ask price quoted by the agent, and emphasizes that the example is only intended to illustrate use of the model rather than disclose the full production algorithm.

![Figure 9 — France Telecom price](assets/figure-09-france-telecom-price.png)

*Figure 9. Price of France Telecom on 15/03/2012, 10:00–16:00.*

![Figure 10 — Strategy inventory](assets/figure-10-inventory.png)

*Figure 10. Inventory in ATS when the strategy is used on France Telecom, 10:00–16:00. The paper reports ATS = 1105 for this day.*

![Figure 11 — Strategy P&L](assets/figure-11-pnl-strategy.png)

*Figure 11. P&L of the model-based strategy on France Telecom, 10:00–16:00.*

The paper compares this P&L with a naive market maker that simply posts at the first limit of the book on each side whenever it is asked to post orders (after execution or after $\Delta t$ without execution).

![Figure 12 — Naive market maker P&L](assets/figure-12-pnl-naive.png)

*Figure 12. P&L of the naive market maker on France Telecom, 10:00–16:00.*

For a one-hour subperiod, the authors plot the market together with the market maker's quotes. Thin lines represent the market, bold lines the market maker, dotted lines the bid side, plain lines the ask side, and black points trades involving the market maker.

![Figure 13 — Detailed quotes and trades](assets/figure-13-quotes-trades.png)

*Figure 13. Detailed quotes and trades for France Telecom, 12:00–13:00.*

# Conclusion

The paper presents a model for optimal market-maker quotes. Starting from a model in line with Avellaneda-Stoikov and rooted in Ho-Stoll, it introduces a change of variables that transforms the HJB equation into a system of linear ODEs. This yields optimal quotes, a characterization of their asymptotic behavior, and closed-form approximations using spectral analysis.

The same change of variables can also be used to solve the initial Avellaneda-Stoikov equations; the authors refer to [13] for a complete mathematical proof. They note that in the absence of inventory limits, no proof of optimality was then available for the quotes claimed optimal in [3], and admissibility appeared to remain open.

The paper identifies two directions for future research: allowing general execution-intensity functions, since the exponential form is best suited to liquid stocks with a small bid-ask spread; and introducing passive market impact, meaning perturbations of the price formation process caused by liquidity provision.

# Acknowledgements

The authors acknowledge helpful conversations with Yves Achdou, Vincent Fardeau, Thierry Foucault, Jean-Michel Lasry, Antoine Lemenant, Pierre-Louis Lions, Albert Menkveld, Vincent Millot, Nizar Touzi, and two anonymous referees.

# References

1. Amihud, Y., Mendelson, H. *Dealership Market. Market-Making with Inventory.* Journal of Financial Economics 8, 31–53 (1980).
2. Amihud, Y., Mendelson, H. *Asset pricing and the bid-ask spread.* Journal of Financial Economics 17(2), 223–249 (1986).
3. Avellaneda, M., Stoikov, S. *High-frequency trading in a limit order book.* Quantitative Finance 8(3), 217–224 (2008).
4. Bayraktar, E., Ludkovski, M. *Liquidation in limit order books with controlled intensity.* arXiv:1105.0247 (2011).
5. Benston Robert, L., George, J. *Determinants of bid-asked spreads in the over-the-counter market.* Journal of Financial Economics 1(4), 353–364 (1974).
6. Cartea, A., Jaimungal, S. *Modeling asset prices for algorithmic and high frequency trading.* 2010.
7. Cartea, A., Jaimungal, S. *Risk measures and fine tuning of high frequency trading strategies.* 2012.
8. Cartea, A., Jaimungal, S., Ricci, J. *Buy low sell high: A high frequency trading perspective.* 2011.
9. Cohen, K.J., Maier, S.F., Schwartz, R.A., Whitcomb, D.K. *Market makers and the market spread: A review of recent literature.* Journal of Financial and Quantitative Analysis 14(04), 813–835 (1979).
10. Cohen, K.J., Maier, S.F., Schwartz, R.A., Whitcomb, D.K. *Transaction Costs, Order Placement Strategy, and Existence of the Bid-Ask Spread.* Journal of Political Economy 89(2), 287–305 (1981).
11. Garman, M.B. *Market microstructure.* Journal of Financial Economics 3(3), 257–275 (1976).
12. Guéant, O., Lehalle, C.A., Fernandez-Tapia, J. *Optimal Execution with Limit Orders.* Working paper (2011).
13. Guéant, O., Lehalle, C.A. *Existence and Uniqueness for the Avellaneda-Stoikov PDE.* Working paper (2012).
14. Guilbaud, F., Pham, H. *Optimal high frequency trading with limit and market orders.* 2011.
15. Guilbaud, F., Pham, H. *Optimal high frequency trading in a pro-rata microstructure with predictive information.* arXiv:1205.3051 (2012).
16. Hendershott, T., Menkveld, A. *Price pressures.* Manuscript, VU University Amsterdam (2009).
17. Ho, T., Stoll, H.R. *Optimal dealer pricing under transactions and return uncertainty.* Journal of Financial Economics 9(1), 47–73 (1981).
18. Ho, T.S.Y., Macris, R.G. *Dealer bid-ask quotes and transaction prices: An empirical study of some AMEX options.* Journal of Finance, 23–45 (1984).
19. Ho, T.S.Y., Stoll, H.R. *The dynamics of dealer markets under competition.* Journal of Finance 38(4), 1053–1074 (1983).
20. Lehalle, C.A., Guéant, O., Razafinimanana, J. *High Frequency Simulations of an Order Book: a Two-Scales Approach.* In Abergel et al. (eds.), *Econophysics of Order-Driven Markets*, Springer (2010).
21. Madhavan, A., Smidt, S. *An analysis of changes in specialist inventories and quotations.* Journal of Finance 48(5), 1595–1628 (1993).
22. Menkveld, A.J. *High Frequency Trading and The New-Market Makers.* Social Science Research Network Working Paper Series (2010).
23. Mildenstein, E., Schleef, H. *The optimal pricing policy of a monopolistic marketmaker in the equity market.* Journal of Finance, 218–231 (1983).
24. O’Hara, M., Oldfield, G.S. *The microeconomics of market making.* Journal of Financial and Quantitative Analysis 21(04), 361–376 (1986).
25. Roll, R. *A simple implicit measure of the effective bid-ask spread in an efficient market.* Journal of Finance 39(4), 1127–1139 (1984).

# Appendix

The original paper contains a long proof appendix (PDF pages 25–36). For source fidelity, it is supplied separately in [`appendix-proofs.md`](appendix-proofs.md), together with rendered images of the proof pages so that dense intermediate equations can be checked visually rather than silently normalized.

For a compact retrieval-oriented list of the main formulas, see [`equations.md`](equations.md).
