---
title: RL
aliases:
  - Reinforcement Learning - Von Grundlagen zu den tiefen Ansätzen
  - RL TUDa
tags:
  - fb20
  - reinforcement-learning
  - machine-learning
description: "Module notes for the TU Darmstadt RL lecture by G. Chalvatzaki (Summer Term 2026). Covers MDPs, value functions, Bellman equations, and dynamic programming."
---

https://moodle.tu-darmstadt.de/course/view.php?id=46418

Lecturer: Georgia Chalvatzaki, Department of Computer Science, TU Darmstadt

---

## Lecture 01 - Introduction to Reinforcement Learning

### What is Reinforcement Learning?

Reinforcement Learning (RL) is a sub-field of machine learning where an **agent** learns by interacting with an **environment**. At each time step $t$, the agent:
1. observes a state $S_t$,
2. executes an action $A_t$,
3. receives a reward $R_{t+1}$ and a new state $S_{t+1}$.

> [!note] Reward Hypothesis (Sutton & Barto)
> All goals can be described as the maximization of a scalar reward signal.

### What Makes RL Special?

- No supervisor - only a reward signal;
- Feedback is **delayed**, not instantaneous;
- Data is **sequential** and not i.i.d.;
- The agent's actions **affect** the future data it receives.

### Stochastic Processes and the Markov Property

A **stochastic process** $\{S_t\}$ is an indexed collection of random variables. In the discrete case, the system is in one of finitely many states at each time step.

> [!note] Markov Property
> A process is **Markovian** if and only if
> $$\mathbb{P}(S_{t+1} = j \mid S_t = i, S_{t-1} = k_{t-1}, \ldots) = \mathbb{P}(S_{t+1} = j \mid S_t = i)$$
> The current state captures **all** information from the history - the past may be discarded.

The **state transition matrix** $\mathbf{P}_{ss'} = \mathbb{P}[S_{t+1} = s' \mid S_t = s]$ encodes all transition probabilities.

**Types of Markov processes:**
- **Absorbing**: has at least one absorbing state reachable from every other state.
- **Ergodic**: all states are recurrent and aperiodic.
- **Regular**: some power of the transition matrix has only positive, stable entries.

### Introduction to Markov Decision Processes

**Markov Decision Processes (MDPs)** formally describe environments for RL where the state is **fully observable**.

| | All states observable? Yes | All states observable? No |
|---|---|---|
| **No actions** | Markov Chain | Hidden Markov Model |
| **Actions** | MDP | Partially Observable MDP |

### Flavors of the RL Problem

| Setting | Description |
|---|---|
| **Full RL Problem** | Agent must learn environment dynamics from scratch |
| **POMDP** | Filtered state (belief state $b_t$) is Markovian; filters compress history |
| **MDP** | State $s_t$ directly observed and Markovian |
| **Contextual Bandit** | State distribution independent of history: $p(s_{t+1} \mid s_{1:t}, a_{1:t}) = p(s_{t+1})$ |
| **Bandit** | Single state - state is irrelevant |

**Problem classification:**

| | Actions do not change state | Actions change state |
|---|---|---|
| **Learn model** | (Multi-Armed) Bandits | Reinforcement Learning |
| **Given model** | Decision Theory | Optimal Control, Planning |

---

## Lecture 02 - MDPs, Policies, Value Functions, and Bellman Equations

### Formal MDP Definition

A **Markov Decision Process** is a tuple $\mathcal{M} = \langle \mathcal{S}, \mathcal{A}, \mathcal{R}, \mathcal{P}, \iota, \gamma \rangle$:

| Symbol | Meaning |
|---|---|
| $\mathcal{S}$ | Finite set of states |
| $\mathcal{A}$ | Finite set of actions |
| $\mathcal{R}$ | Reward function $\mathcal{R}: \mathcal{S} \times \mathcal{A} \times \mathcal{S} \to \mathbb{R}$ |
| $\mathcal{P}$ | Transition function $\mathcal{P}(s', r \mid s, a)$ |
| $\iota$ | Initial state distribution |
| $\gamma \in [0,1)$ | Discount factor |

The **return** is the discounted cumulative reward:
$$J_t = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}$$

The discount factor $\gamma$ controls the trade-off between immediate and future rewards. For $\gamma = 0$ only immediate rewards matter; for $\gamma \to 1$ future rewards are weighted equally.

### Policies

A **policy** $\pi$ is a probability distribution over actions given a state:
$$\pi(a \mid s) = \mathbb{P}(A_t = a \mid S_t = s)$$

RL aims to find the **optimal policy** $\pi^*$ that **maximizes the return from every state**.

### Value Functions

> [!note] Value Function
> The **value function** $V^\pi(s)$ is the expected discounted return when starting in $s$ and following $\pi$:
> $$V^\pi(s) \triangleq \mathbb{E}_\pi\left[\sum_{k=0}^{\infty} \gamma^k R_{t+k+1} \,\middle|\, S_t = s\right]$$

> [!note] Action-Value Function
> The **action-value function** $Q^\pi(s, a)$ is the expected discounted return when starting in $s$, taking action $a$, and following $\pi$ thereafter:
> $$Q^\pi(s, a) \triangleq \mathbb{E}_\pi\left[\sum_{k=0}^{\infty} \gamma^k R_{t+k+1} \,\middle|\, S_t = s, A_t = a\right]$$

> [!note] Advantage Function
> The **advantage function** measures the relative performance of an action w.r.t. the policy:
> $$A^\pi(s, a) = Q^\pi(s, a) - V^\pi(s)$$
> The expected advantage under $\pi$ is always zero: $\mathbb{E}_{a \sim \pi}[A^\pi(s,a)] = 0$.

**Key relationship** (when $a$ is sampled from $\pi$):
$$V^\pi(s) = \mathbb{E}_{a \sim \pi}\left[Q^\pi(s, a)\right]$$

**Value function bounds:** Since rewards are bounded by $\mathcal{R}_{\min}$ and $\mathcal{R}_{\max}$:
$$V^\pi(s) \in \left[\frac{\mathcal{R}_{\min}}{1-\gamma},\, \frac{\mathcal{R}_{\max}}{1-\gamma}\right]$$

### Optimal Value Functions and Policies

$$V^*(s) \triangleq \max_\pi V^\pi(s), \qquad Q^*(s,a) \triangleq \max_\pi Q^\pi(s,a)$$

The relationship between them:
$$V^*(s) = \max_{a \in \mathcal{A}} Q^*(s, a)$$

The **deterministic optimal policy** is recovered by:
$$\pi^*(a \mid s) = \begin{cases} 1 & \text{if } a = \operatorname{argmax}_{a \in \mathcal{A}} Q^*(s,a) \\ 0 & \text{otherwise} \end{cases}$$

**Properties of optimal policies:**
- An optimal policy $\pi^*$ exists that is $\geq$ all other policies for every state;
- All optimal policies share the same $V^*$ and $Q^*$;
- There is always a **deterministic** optimal policy for any MDP.

### Bellman Equations

**Bellman (expectation) equation for $V^\pi$:**
$$V^\pi(s) = \sum_a \pi(a \mid s) \sum_{s',r} \mathcal{P}(s', r \mid s, a)\left[r + \gamma V^\pi(s')\right], \quad \forall s \in \mathcal{S}$$

**Bellman equation for $Q^\pi$:**
$$Q^\pi(s, a) = \sum_{s',r} \mathcal{P}(s', r \mid s, a)\left[r + \gamma \sum_{a' \in \mathcal{A}} \pi(a' \mid s') Q^\pi(s', a')\right]$$

In matrix form: $V^\pi = R^\pi + \gamma P^\pi V^\pi$, solved as $V^\pi = (I - \gamma P^\pi)^{-1} R^\pi$ with complexity $O(n^3)$ for $n$ states.

**Bellman optimality equation for $V^*$:**
$$V^*(s) = \max_{a \in \mathcal{A}} \sum_{s',r} \mathcal{P}(s', r \mid s, a)\left[r + \gamma V^*(s')\right], \quad \forall s \in \mathcal{S}$$

**Bellman optimality equation for $Q^*$:**
$$Q^*(s, a) = \sum_{s',r} \mathcal{P}(s', r \mid s, a)\left[r + \gamma \max_{a'} Q^*(s', a')\right], \quad \forall s \in \mathcal{S}, a \in \mathcal{A}$$

For large MDPs the direct matrix solution is infeasible. Iterative methods include **Dynamic Programming**, **Monte Carlo RL**, and **Temporal Difference Learning**.

---

## Lecture 03 - Dynamic Programming

### Bellman Operators

The **Bellman operator** $T^\pi : \mathbb{R}^{|\mathcal{S}|} \to \mathbb{R}^{|\mathcal{S}|}$ for $V^\pi$ is:
$$(T^\pi V^\pi)(s) = \sum_{a \in \mathcal{A}} \pi(a \mid s) \sum_{s',r} \mathcal{P}(s', r \mid s, a)\left[r + \gamma V^\pi(s')\right]$$

The Bellman equation is compactly $T^\pi V^\pi = V^\pi$, i.e., $V^\pi$ is the **fixed point** of $T^\pi$.

The **Bellman optimality operator** $T^* : \mathbb{R}^{|\mathcal{S}|} \to \mathbb{R}^{|\mathcal{S}|}$:
$$(T^* V^*)(s) = \max_{a \in \mathcal{A}} \sum_{s',r} \mathcal{P}(s', r \mid s, a)\left[r + \gamma V^*(s')\right]$$

Compactly: $T^* V^* = V^*$.

**Key properties of Bellman operators** (for $0 < \gamma < 1$):
- **Monotonicity:** $f_1 \leq f_2 \Rightarrow T^\pi f_1 \leq T^\pi f_2$ and $T^* f_1 \leq T^* f_2$;
- **Max-norm contraction:** $\|T^\pi f_1 - T^\pi f_2\|_\infty \leq \gamma \|f_1 - f_2\|_\infty$;
- $V^\pi$ and $Q^\pi$ are the **unique fixed points** of $T^\pi$; $V^*$ and $Q^*$ are the **unique fixed points** of $T^*$;
- $\lim_{k \to \infty} (T^\pi)^k f = V^\pi$ and $\lim_{k \to \infty} (T^*)^k f = V^*$ for any starting $f$.

### Dynamic Programming

> [!note] Definition (Sutton & Barto, 2018)
> Dynamic programming refers to a collection of algorithms that can be used to compute optimal policies given a **perfect model of the environment** as an MDP.

DP requires **full knowledge** of the MDP (transition function $\mathcal{P}$ and reward function $\mathcal{R}$). It is used for **planning**, not learning.

DP works because MDPs satisfy two properties required for DP:
- **Optimal substructure**: the principle of optimality applies; optimal solution decomposes into sub-problems.
- **Overlapping sub-problems**: sub-problems recur; solutions can be cached and reused (via value functions).

**Tasks:**
- **Prediction**: given MDP and policy $\pi$, compute $V^\pi$.
- **Control**: given MDP, find optimal $V^*$ and $\pi^*$.

### Policy Evaluation (Iterative)

Repeatedly apply the Bellman operator:
$$V_{k+1}(s) \leftarrow \sum_{a \in \mathcal{A}} \pi(a \mid s) \sum_{s',r} \mathcal{P}(s', r \mid s, a)\left[r + \gamma V_k(s')\right]$$

This **converges** to $V^\pi$ as $k \to \infty$. Each sweep applies the update to all states synchronously.

### Policy Improvement

Given $V^\pi$, generate a **greedy** improved policy:
$$\pi'(s) = \operatorname{argmax}_{a \in \mathcal{A}} Q^\pi(s, a)$$

**Policy improvement theorem:** If $Q^\pi(s, \pi'(s)) \geq V^\pi(s)$ for all $s$, then $V^{\pi'}(s) \geq V^\pi(s)$ for all $s$.

### Policy Iteration

Alternates between policy evaluation and policy improvement until convergence:
$$\pi_0 \to V^{\pi_0} \to \pi_1 \to V^{\pi_1} \to \cdots \to \pi^* \to V^*$$

When improvements stop ($V^{\pi'} = V^\pi$), the Bellman optimality equation is satisfied and $\pi$ is optimal. The algorithm terminates in at most $|\mathcal{A}|^{|\mathcal{S}|}$ iterations.

### Value Iteration

Combines **one step of policy evaluation** with policy improvement, applying the Bellman optimality operator directly:
$$V_{k+1}(s) \leftarrow \max_{a \in \mathcal{A}} \sum_{s',r} \mathcal{P}(s', r \mid s, a)\left[r + \gamma V_k(s')\right]$$

$$V_1 \to T^* V_1 = V_2 \to \cdots \to T^* V_k = V^*$$

Unlike policy iteration, there is **no explicit policy** during iteration; intermediate value functions may not correspond to any policy. The optimal policy is extracted at convergence.

**Convergence proof (Banach fixed point theorem):**
$$\|V_{k+1} - V^*\|_\infty = \|T^* V_k - T^* V^*\|_\infty \leq \gamma \|V_k - V^*\|_\infty \leq \cdots \leq \gamma^{k+1} \|V_0 - V^*\|_\infty \to 0$$

### Summary of Synchronous DP Algorithms

| Problem | Bellman Equation Used | Algorithm |
|---|---|---|
| Prediction | Bellman equation | Policy Evaluation (Iterative) |
| Control | Bellman equation + greedy improvement | Policy Iteration |
| Control | Bellman optimality equation | Value Iteration |

Complexity per iteration: $O(mn^2)$ for $m$ actions and $n$ states (or $O(m^2 n^2)$ for $Q$-functions).

### Generalized Policy Iteration

Most RL algorithms are variants of **Generalized Policy Iteration (GPI)**: alternate between:
- **Policy evaluation**: estimate $V^\pi$ for the current $\pi$;
- **Policy improvement**: generate $\pi' \geq \pi$ via greedy update.

At convergence: $\pi^* \leftrightarrow V^*$.

### Efficiency and Limitations

- Finding optimal policies is **polynomial** in the number of states;
- But the state space often grows **exponentially** with the number of state variables - **curse of dimensionality**;
- Classical DP is practical up to a few million states;
- **Asynchronous DP** can handle larger problems and is suited for parallel computation.
