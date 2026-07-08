---
title: DMML - Klausurfragensammlung
aliases:
  - DMML Exam Questions
  - DMML Klausurfragen
tags:
  - machine-learning
  - data-mining
description: "Collection of DMML exam questions reconstructed from student memory protocols (Gedächtnisprotokolle), with worked answers."
draft: false
---

> [!INFO] About this note
> Exam questions collected from **memory protocols** (*Gedächtnisprotokolle*) and official **student model solutions** (studentische Musterlösungen by T. Huisinga). Sessions marked **✅ verified** have worked answers taken from an official solution PDF; the others are reconstructed and should be cross-checked against the lecture slides and exercises. Related concept: [[Data Mining und Maschinelles Lernen|DMML module note]].
>
> **Sessions (chronological):** SoSe 2021 ✅ · WiSe 2021/22 ✅ · Demoklausur SoSe 2022 ✅ · SoSe 2022 ✅ · SoSe 2023 ✅ · SoSe 2024 · SoSe 2025 · WiSe 2025/26

## Exam SoSe 2021 ✅ verified

> [!NOTE] Format
> Total **100 points**, **15 tasks**. Answers below are the official student model solution (T. Huisinga). The baseball ID3/Gini dataset and the NN figure recur across several exams.

### Task 1 — Machine Learning hierarchy (4 P.)

> [!question]- Drag the given terms to the correct positions in the ML-concepts hierarchy diagram.
> **Machine Learning (ML)** branches into:
> - **Supervised Learning (SL)** → **Classification**, **Regression**
> - **Unsupervised Learning (UL)** → **Clustering**, **Density Estimation**
> - **Reinforcement Learning (RL)**
>
> See [[Maschine Learning]], [[Classification and Regression]].

### Task 2 — ID3 with Gini index / CART (11 P.)

> [!question]- Baseball dataset (features Luftfeuchtigkeit $L$, Wind $W$; target "Spielt Baseball"). Determine the root-node attribute via CART (ID3 using the Gini index). Give the Gini index and the Gini-based gain. **[worked]**
> Conditional class frequencies — $P(Ja|L)$: Normal $2/4$, Hoch $2/6$; $P(Ja|W)$: Schwach $3/5$, Stark $1/5$.
> **Feature Luftfeuchtigkeit $L$:**
> - $Gini(L{=}Normal)=1-(2/4)^2-(2/4)^2 = 0.5$
> - $Gini(L{=}Hoch)=1-(2/6)^2-(4/6)^2 = 0.\overline{4}$
> - weighted: $Gini(L)=\tfrac{4}{10}\cdot0.5+\tfrac{6}{10}\cdot0.\overline{4}=0.4\overline{6}$ → gain $=1-0.4\overline{6}=0.5\overline{3}$
> **Feature Wind $W$:**
> - $Gini(W{=}Schwach)=1-(3/5)^2-(2/5)^2 = 0.48$
> - $Gini(W{=}Stark)=1-(1/5)^2-(4/5)^2 = 0.32$
> - weighted: $Gini(W)=\tfrac{5}{10}\cdot0.48+\tfrac{5}{10}\cdot0.32 = 0.4$ → gain $=1-0.4=0.6$
> **Wind has the lowest weighted Gini (0.4) / highest gain (0.6) → chosen as root node.** *(The solution defines "gain" as $1-Gini_{\text{weighted}}$; the selection criterion is simply the smallest weighted Gini.)*
>
> See [[CART (Decision Tree)]], [[Gini Index]], [[Entropy and Information Gain]].

### Task 3 — Linear regression (7 P.)

> [!question]- An 8-dim output $y$ is predicted from a 16-dim input $x$ by linear regression. State $f(x)$, the component dimensions, the number of learnable parameters, and a suitable loss. **[worked]**
> - **Model:** $f(x) = Wx + b$.
> - **Dimensions:** $W \in \mathbb{R}^{8\times16}$, $x \in \mathbb{R}^{16}$, $b \in \mathbb{R}^{8}$ (input $x$ is data, not a parameter).
> - **Learnable parameters:** $W + b = 8\cdot16 + 8 = \mathbf{136}$.
> - **Loss:** Mean Squared Error $L(x)=\tfrac1n\sum_{i=1}^n\big(y_i-(Wx_i+b)\big)^2$.
>
> See [[Linear Regression]], [[Classification and Regression]], [[Loss Functions in Machine Learning]].

### Task 4 — Neural network / backpropagation (11 P.)

> [!question]- Net with ReLU $f(x)=\max(0,x)$, **no bias**, target $t=0.2$, loss $L(g)=0.5(g-t)^2$, $\alpha=0.5$. Inputs $x_1{=}0.4,x_2{=}0.6$; weights $w_1{=}0.3,w_2{=}-0.7,w_3{=}0.1,w_4{=}0.9,w_5{=}-0.5,w_6{=}0.7$. **[worked]**
> **4.1 Forward pass:**
> - $f(h_1)=\max(0,\,0.4\cdot0.3+0.6\cdot(-0.7))=\max(0,-0.3)=0$
> - $f(h_2)=\max(0,\,0.4\cdot0.1+0.6\cdot0.9)=\max(0,0.58)=0.58$
> - $g=\max(0,\,0\cdot(-0.5)+0.58\cdot0.7)=\mathbf{0.406}$
> **4.2 Error:** $L(g)=\tfrac12(0.406-0.2)^2=\mathbf{0.021218}$.
> **4.3 Backprop** (update $w_6, w_4$), $\frac{\partial L}{\partial g}=g-t=0.206$:
> - $w_6' = w_6-\alpha(g-t)f(h_2)=0.7-0.5\cdot0.206\cdot0.58=\mathbf{0.64026}$
> - $w_4' = w_4-\alpha(g-t)\,w_6\,x_2=0.9-0.5\cdot0.206\cdot0.7\cdot0.6=\mathbf{0.85674}$
>
> See [[Backpropagation]], [[Multilayer Perceptron]], [[Loss Functions in Machine Learning]].

### Task 5 — Coding: SVM vs. Random Forest, 10-fold CV (8 P.)

> [!question]- Python: build a poly-kernel SVM (degree 5) and a random forest of 5 stumps; 10-fold cross-validation, print mean accuracy of each.
> ```python
> # SVM with polynomial kernel of degree 5
> svm_model = svm.SVC(kernel='poly', degree=5)
> # Random forest of 5 decision stumps
> rf_model = RandomForestClassifier(max_depth=1, n_estimators=5)
> # 10-fold cross-validation
> svm_scores = cross_validate(svm_model, X_train, y_train, cv=10)
> rf_scores  = cross_validate(rf_model,  X_train, y_train, cv=10)
> print("Mean accuracy of SVM:", np.mean(svm_scores))
> print("Mean accuracy of Random Forest:", np.mean(rf_scores))
> ```
> `kernel='poly', degree=5`; `max_depth=1` (stump) with `n_estimators=5`; `cv=10`; `np.mean` over the scores.
>
> See [[Support Vector Machine]], [[Random Forest]], [[Cross-Validation]].

### Task 6 — SVM & non-linearity (4 P.)

> [!question]- A colleague's SVM performs poorly (see plots). Why is the configuration suboptimal, and which standard measure improves it?
> - **Reason:** the classes are **not linearly separable** — it is a non-linear classification problem, so a linear hyperplane can't separate them well.
> - **Measure:** apply a **kernel function** (e.g. the **RBF kernel**). The kernel computes inner products in an implicitly higher- (for RBF, infinite-) dimensional space where the data becomes linearly separable — solving the non-linear problem without explicit feature transformation.
>
> See [[Support Vector Machine]].

### Task 7 — Support & Confidence (8 P.)

> [!question]- Shopping DB — Butter (B), Mehl (M), Pasta (P): $(1,1,0),(1,1,0),(0,1,1),(0,0,1)$. Find all rules $\{A\}\Rightarrow\{B\}$ over one-element sets with support $s\ge0.25$ and confidence $\ge0.5$. **[worked]**
> $$s(X)=\frac{\#\text{transactions with }X}{N},\quad conf(X{\Rightarrow}Y)=\frac{s(X\cup Y)}{s(X)}$$
> **Qualifying rules:**
> - $\{B\}\Rightarrow\{M\}$: $s=\tfrac12$, $conf=1$
> - $\{M\}\Rightarrow\{B\}$: $s=\tfrac12$, $conf=\tfrac23$
> - $\{P\}\Rightarrow\{M\}$: $s=\tfrac14$, $conf=\tfrac12$
> **Non-qualifying:** $\{B\}\Rightarrow\{P\}$ ($s=0$); $\{M\}\Rightarrow\{P\}$ ($s=\tfrac14,conf=\tfrac13$); $\{P\}\Rightarrow\{B\}$ ($s=0$).
>
> See [[Association Rule Mining]], [[Support and Confidence]].

### Task 8 — BIC (5 P.)

> [!question]- $M_1,M_2$ perform comparably on the validation set, but $M_2$ has 10× as many parameters. True/false: "By BIC we choose $M_2$ because it has higher capacity." Justify.
> **False.** BIC relates a model's parameter count and its performance; at **equal performance it prefers the model with fewer parameters**. So by BIC we choose **$M_1$**. (BIC $=-2\ln\hat L + k\ln n$ penalizes complexity $k$.)
>
> See [[Bayesian Information Criterion]], [[Minimum Description Length]].

### Task 9 — CNN parameter count (4 P.)

> [!question]- Trainable parameters of a conv layer that processes a single 24×24 input with 16 filters of size 5×5 and zero-padding 2, using bias? **[worked]**
> Input size and padding are **irrelevant** to the parameter count — only the filters matter (weight sharing):
> $$16\cdot(5\cdot5) + 16\ (\text{bias}) = 400 + 16 = \mathbf{416}\ \text{parameters}.$$
>
> See [[Convolutional Neural Network]].

### Task 10 — Cross-validation theory / accuracy paradox (5 P.)

> [!question]- A friend claims high classification accuracy under cross-validation always reliably reflects performance. Comment + give a counterexample; which additional metric should be reported?
> **Not always reliable** — the **accuracy paradox** on **imbalanced data**: if 95 % of samples are class A and 5 % class B, a classifier that always predicts A scores 95 % accuracy yet never detects B (poor real performance). **Additional metric:** report **F1-score** (and/or precision & recall), which handle class imbalance.
>
> See [[Confusion Matrix]], [[Precision and Recall]], [[Cross-Validation]].

### Task 11 — Bayesian networks / MLE (11 P.)

> [!question]- Binary Bayesian net over $A,B,C$ (edges $A\to B$, $A\to C$, $C\to B$); 8-row dataset. Estimate the given parameters by Maximum Likelihood, give the factorization, and name the algorithm for incomplete data. **[worked]**
> **MLE parameters** (counting):
> - $P(A{=}1)=\tfrac78$
> - $P(C{=}0\mid A{=}0)=0$, $\quad P(C{=}0\mid A{=}1)=\tfrac47$
> - $P(B{=}0\mid A{=}1,C{=}0)=\tfrac14$, $\quad P(B{=}1\mid A{=}1,C{=}1)=\tfrac13$, $\quad P(B{=}0\mid A{=}0,C{=}1)=1$
> **Factorization:** $P(A,B,C)=P(A)\cdot P(B\mid A,C)\cdot P(C\mid A)$.
> **Incomplete data:** use the **Expectation-Maximization (EM)** algorithm (complete data by inference → re-estimate parameters → iterate to convergence).
>
> See [[Naive Bayes Classifier]], [[Maximum Likelihood Estimation]].

### Task 12 — Hyperparameter & overfitting (6 P.)

> [!question]- Explain hyperparameter and overfitting; give a decision-tree hyperparameter and a concrete overfitting countermeasure.
> - **Hyperparameter:** a value fixed by the user beforehand (not learned during training). DT example: **maximum tree depth** (or maximum width).
> - **Overfitting:** the model is fit too closely to the training data → poor generalization; very specific decision rules give great train performance but fail on test data. **Countermeasure:** **pre-pruning** (limit the tree during training) or **post-pruning** (cut back the tree after training).
>
> See [[Overfitting]], [[CART (Decision Tree)]].

### Task 13 — Cross-validation vs. Leave-One-Out (5 P.)

> [!question]- A linear SVM is trained on a linearly-separable dataset (Abb. 8). (1) Accuracy under Leave-One-Out CV? (2) With one million examples, LOOCV or another CV?
> - **(1) 100 %** — for this cleanly separable set, leaving out a single point does not change the hyperplane, so every held-out point is classified correctly regardless of which one is omitted.
> - **(2)** LOOCV is **not advisable** for 1 M examples — it is extremely expensive (1 M trainings on 1 M − 1 points each). Use **k-fold cross-validation** for acceptable efficiency.
>
> See [[Cross-Validation]], [[Support Vector Machine]].

### Task 14 — Bagging vs. Boosting (7 P.)

> [!question]- Describe bagging and boosting; name two differences and two commonalities.
> - **Bagging (Bootstrap Aggregating):** draw several bootstrap samples (with replacement), train one model per sample **in parallel**, combine by averaging / majority vote.
> - **Boosting:** **sequential** — each subsequent model tries to correct the errors of the previous ones; models are weighted by their performance in the final combination.
> - **Commonalities:** both are **ensemble methods** combining weak learners; both focus on single base models (unlike stacking's meta-model).
> - **Differences:** **parallel (bagging) vs. sequential (boosting)**; in bagging all models weigh equally, in **boosting** the weighting depends on each model's performance.
>
> See [[Bagging]], [[Boosting]], [[Bias-Variance Tradeoff]].

### Task 15 — Bias & Variance (4 P.)

> [!question]- Drag the terms onto the dartboard diagram.
> Columns = variance, rows = bias:
> - top-left **High Variance**, top-right **Low Variance**; right label of top row **Low Bias**; bottom row **High Bias**.
> - Tight on centre → low bias, low variance; scattered on centre → low bias, high variance; tight off-centre → high bias, low variance; scattered off-centre → high bias, high variance.
>
> See [[Bias-Variance Tradeoff]].

---

## Exam WiSe 2021/22 ✅ verified

> [!NOTE] Format
> Total ~100 points, **11 tasks** (official student solution; 3–4 tasks of the original exam are missing from the documentation).

### Task 1 — Price prediction (5 P.)

> [!question]- 10 000 records, 10 features, each mapped to a property price in €. (1) Which standard learning setting? (2) A suitable objective function and its derivative. **[worked]**
> - **(1) Regression** (predict a continuous value).
> - **(2)** Mean Squared Error and its derivative: $MSE=\tfrac1n\sum_{i=1}^n(y_i-\hat y_i)^2$, $\ \frac{\partial MSE}{\partial\hat y_i}=\tfrac2n\sum_{i=1}^n(\hat y_i-y_i)$.
>
> See [[Linear Regression]], [[Loss Functions in Machine Learning]].

### Task 2 — ID3 (entropy) (11 P.)

> [!question]- Same baseball dataset (Luftfeuchtigkeit $L$, Wind $W$) — determine the root via ID3 using **entropy**. **[worked]**
> $Entropy=-p_+\log_2 p_+ - p_-\log_2 p_-$; $IG(K,M)=Entropy(K)-\sum_i \frac{|K_{M=m_i}|}{|K|}Entropy(K_{M=m_i})$.
> - $Entropy(K)=-\tfrac{4}{10}\log_2\tfrac{4}{10}-\tfrac{6}{10}\log_2\tfrac{6}{10}\approx 0.971$
> - $Entropy(L{=}Normal)=1$, $\ Entropy(L{=}Hoch)\approx0.918$ → $IG(L)=0.971-(\tfrac{4}{10}\cdot1+\tfrac{6}{10}\cdot0.918)=\mathbf{0.0202}$
> - $Entropy(W{=}Schwach)\approx0.971$, $\ Entropy(W{=}Stark)\approx0.722$ → $IG(W)=0.971-(\tfrac{5}{10}\cdot0.971+\tfrac{5}{10}\cdot0.722)=\mathbf{0.1245}$
> **Wind has the highest information gain → root node.**
>
> See [[Entropy and Information Gain]], [[ID3 (Decision Tree)]].

### Task 3 — Naive Bayes class weighting (6 P.)

> [!question]- 200 points of class A, 100 of class B. You may add 450 more points. How to choose them so a Naive Bayes classifier weights class A **twice** as strongly as class B? **[worked]**
> Need $P(A)=2P(B)$, i.e. $A_{new}=2B_{new}$. Split the 450 as $x$ to A, $y$ to B ($x+y=450$): $200+x = 2(100+y) \Rightarrow x=2y \Rightarrow 3y=450 \Rightarrow y=150,\ x=300$.
> → Add **300 to A and 150 to B**, giving $A_{new}=500$, $B_{new}=250$ (indeed $500=2\cdot250$). *(Intuitively: total $750$, split $2{:}1$.)*
>
> See [[Naive Bayes Classifier]].

### Task 4 — Neural network / backpropagation (11 P.)

> [!question]- ReLU, no bias, $t=0.4$, $L(W)=0.5(g-t)^2$, $\alpha=0.5$. Inputs $x_1{=}0.75,x_2{=}0.42$; weights $w_1{=}-0.2,w_2{=}0.3,w_3{=}-0.5,w_4{=}1.2,w_5{=}0.4,w_6{=}0.8$. **[worked]**
> **Forward:** $f(h_1)=\max(0,0.75(-0.2)+0.42\cdot0.3)=0$; $f(h_2)=\max(0,0.75(-0.5)+0.42\cdot1.2)=0.129$; $g=\max(0,0\cdot0.4+0.129\cdot0.8)=\mathbf{0.1032}$.
> **Loss:** $L=\tfrac12(0.1032-0.4)^2=\mathbf{0.0880924}$.
> **Backprop** (update $w_1,w_6$), $g-t=-0.2968$:
> - $w_1' = w_1-\alpha(g-t)\,w_5\,x_1 = -0.2-0.5(-0.2968)(0.4)(0.75)=\mathbf{-0.15548}$
> - $w_6' = w_6-\alpha(g-t)f(h_2)=0.8-0.5(-0.2968)(0.129)=\mathbf{0.8191436}$
>
> See [[Backpropagation]], [[Multilayer Perceptron]].

### Task 5 — Efficient kNN data structure (4 P.)

> [!question]- A naive kNN prediction is inefficient. Which data structure keeps prediction time low?
> A **k-d tree** (k-dimensional tree): it recursively partitions the search space into subregions so the classifier only inspects the relevant subregions instead of computing the distance to every training point.
>
> See [[K-Nearest Neighbors]].

### Task 6 — N-fold cross-validation (5 P.)

> [!question]- Linear SVM on a linearly-separable set (Abb. 3). (1) Accuracy under $N$-fold CV ($N$ = #examples)? (2) With one million examples, same CV or another?
> - **(1) 100 %** — $N$-fold CV with $N$ examples equals Leave-One-Out; leaving out one point doesn't move the hyperplane on this separable set, so all points are classified correctly.
> - **(2)** Not advisable at 1 M examples (extremely expensive); use **k-fold CV with small $k$**.
>
> See [[Cross-Validation]], [[Support Vector Machine]].

### Task 7 — ROC curve & cost minimization (9 P.)

> [!question]- ROC curve given (thresholds 0.3, 0.7, 0.8, 0.85, 0.95, 0.99, 1). FP costs 3 €, FN costs 8 €. (1) Perfect classifier's ROC & AUC? (2) Random classifier's ROC & AUC? (3) Cost-minimizing threshold and expected minimal cost for 500 examples. **[worked]**
> - **(1)** Perfect: a horizontally-mirrored "L" (straight up to (0,1) then across); **AUC = 1**.
> - **(2)** Random: the diagonal $FPR=TPR$ from (0,0) to (1,1); **AUC = 0.5**.
> - **(3)** With $FNR=1-TPR$, expected cost $=FNR\cdot8 + FPR\cdot3$:
>
> | Threshold | FNR | FPR | Expected cost |
> |---|---|---|---|
> | 0.3 | 0 | 1 | 3 |
> | **0.7** | **0** | **0.4** | **1.2** |
> | 0.8 | 0.2 | 0.4 | 2.8 |
> | 0.85 | 0.4 | 0.2 | 3.8 |
> | 0.95 | 0.8 | 0.2 | 7 |
> | 0.99 | 0.8 | 0 | 6.4 |
> | 1 | 1 | 0 | 8 |
>
> Minimum at **threshold 0.7** (cost 1.2); for 500 examples → $500\cdot1.2 = \mathbf{600\,€}$.
>
> See [[ROC Curve]], [[Confusion Matrix]].

### Task 8 — Bayesian network / variable elimination (8 P.)

> [!question]- Bayesian net over binary $A,B,C$ with given CPTs ($P(a)=0.7$; $A\to C$, $A,C\to B$). (1) Factorization of $P(A,B,C)$. (2) Compute $P(C{=}1,B{=}0)$ by variable elimination. **[worked]**
> - **(1)** $P(A,B,C)=P(A)\cdot P(B\mid A,C)\cdot P(C\mid A)$.
> - **(2)** Marginalize over $A$: $P(C,\neg B)=\sum_{a}P(C,\neg B,A{=}a)$.
>   - $A{=}1$: $P(a)\,P(\neg b\mid a,c)\,P(c\mid a)=0.7\cdot0.7\cdot0.2=0.098$
>   - $A{=}0$: $P(\neg a)\,P(\neg b\mid\neg a,c)\,P(c\mid\neg a)=0.3\cdot0.2\cdot0.6=0.036$
>   - $P(C{=}1,B{=}0)=0.098+0.036=\mathbf{0.134}$
>
> See [[Naive Bayes Classifier]].

### Task 9 — Bagging vs. Boosting (7 P.)

> [!question]- Describe bagging and boosting; two differences and two commonalities.
> Identical to SoSe 2021 Task 14. See [[Bagging]], [[Boosting]].

### Task 10 — Bias & Variance (4 P.)

> [!question]- Drag the terms onto the dartboard diagram.
> Same as SoSe 2021 Task 15. See [[Bias-Variance Tradeoff]].

### Task 11 — K-Median algorithm (7 P.)

> [!question]- Points $P{=}(2,0),Q{=}(5,1),R{=}(2,2),S{=}(4,1.5),T{=}(4,5),U{=}(0.5,1)$; $K=2$, init $mu_A{=}(1,2),mu_B{=}(3,3)$. One update step of **K-Median** (Manhattan distance, median update). **[worked]**
> Manhattan distance $|x_1-y_1|+|x_2-y_2|$ to each centroid:
>
> | DP | to $mu_A$ | to $mu_B$ | → |
> |---|---|---|---|
> | P | 3 | 4 | A |
> | Q | 5 | 4 | B |
> | R | 1 | 2 | A |
> | S | 3.5 | 2.5 | B |
> | T | 6 | 3 | B |
> | U | 1.5 | 4.5 | A |
>
> Assignment: $A=\{P,R,U\}$, $B=\{Q,S,T\}$. **Median update:**
> - $mu_A=\mathrm{median}\big((2,0),(2,2),(0.5,1)\big)=(2,1)$
> - $mu_B=\mathrm{median}\big((5,1),(4,1.5),(4,5)\big)=(4,1.5)$
>
> *(K-Median differs from k-means in using the Manhattan distance and the coordinate-wise median for centroid updates.)*
>
> See [[k-Means Clustering]], [[Clustering]].

---

## Demoklausur SoSe 2022 ✅ verified

> [!NOTE] Format
> **6 tasks** (official student solution). The 2022 demo exam is identical to the 2021 demo exam.

### Task 1 — Trainable parameters in a neural net (7 P.)

> [!question]- Classify 20×20 **RGB** images (defective vs. not) with a fully-connected net, classical sigmoid activation, one hidden layer of 100 neurons (not a CNN). Trainable parameters per layer and in total? **[worked]**
> - **Input:** $20\cdot20\cdot3 = 1200$ input values (3 colour channels).
> - **Hidden layer:** $1200\cdot100 + 100\ (\text{bias}) = \mathbf{120\,100}$.
> - **Output neuron:** $100 + 1\ (\text{bias}) = \mathbf{101}$.
> - **Total:** $120\,100 + 101 = \mathbf{120\,201}$ trainable parameters.
>
> See [[Multilayer Perceptron]].

### Task 2 — CNN output-size computation (5 P.)

> [!question]- Input 30×22 (rows × cols). Apply, in sequence: (1) max-pooling 2×2, stride (2,2); (2) convolution 5×5, stride (2,2), padding (2,2). Output sizes? **[worked]**
> $$Size_{out}=\left\lfloor\frac{Size_{in}-Size_{filter}+2\cdot Pad}{Stride}\right\rfloor+1$$
> - **After op 1:** $\lfloor(30-2+0)/2\rfloor+1=15$, $\lfloor(22-2+0)/2\rfloor+1=11$ → **15×11**.
> - **After op 2:** $\lfloor(15-5+4)/2\rfloor+1=8$, $\lfloor(11-5+4)/2\rfloor+1=6$ → **8×6**.
>
> See [[Convolutional Neural Network]].

### Task 3 — AdaBoost (2 P.)

> [!question]- What happens to the weights of the correctly classified observations in each AdaBoost iteration?
> They are **decreased** each iteration (while misclassified observations' weights are **increased**), so subsequent learners focus on the examples the previous learners got wrong.
>
> See [[AdaBoost]], [[Boosting]].

### Task 4 — Random Forest main idea (3 P.)

> [!question]- Main idea of random forests in keywords: [composition], [data], [decision].
> - **Composition:** a form of **bagging** — an ensemble of decision trees.
> - **Data:** each tree gets a bootstrap subset (sampling with replacement) **and** a randomly chosen subset of features.
> - **Decision:** final output by **majority vote** (classification) or **averaging** (regression).
>
> See [[Random Forest]], [[Bagging]].

### Task 5 — K-Means algorithm (6 P.)

> [!question]- Points $A{=}(1,1),B{=}(2,2),C{=}(2,0),D{=}(4,1),E{=}(5,1)$; $K=2$, init centroids $mu_A{=}D,\ mu_B{=}E$ (Euclidean). Two full iterations. **[worked]**
> **Iter 1 — assignment** (distances): all of $A,B,C,D$ are nearest to $mu_A=(4,1)$, only $E$ to $mu_B=(5,1)$ → $Cluster_A=\{A,B,C,D\}$, $Cluster_B=\{E\}$.
> **Iter 1 — update:** $mu_A^1=\mathrm{mean}((1,1),(2,2),(2,0),(4,1))=(2.25,1)$, $mu_B^1=(5,1)$.
> **Iter 2 — assignment:** $A,B,C$ nearer $mu_A^1$; $D,E$ nearer $mu_B^1$ → $Cluster_A=\{A,B,C\}$, $Cluster_B=\{D,E\}$.
> **Iter 2 — update:** $mu_A^2=\mathrm{mean}((1,1),(2,2),(2,0))=(1.\overline6,1)$, $mu_B^2=\mathrm{mean}((4,1),(5,1))=(4.5,1)$.
>
> See [[k-Means Clustering]].

### Task 6 — Maximum of the Gini index (1 P.)

> [!question]- $I(t)=1-\sum_{j=1}^k p^2(j|t)$. When is the Gini index maximal?
> At a **completely uniform** class distribution, i.e. when $P(\text{class}\mid t)$ is equal for every class. For **two classes** the maximum value is **0.5**.
>
> See [[Gini Index]].

---

## Exam SoSe 2022 ✅ verified

> [!NOTE] Format
> Official student solution (Gedächtnisprotokoll SoSe 2022). Tasks marked with `*` are 1-to-1 from the 2020 exam. Task 5 was not documented.

### Task 1 — Naive Bayes / Bayes' theorem

> [!question]- Baseball dataset (Ausblick $A$, Wind $W$), 10 days; predict day 11 (Sonnig, Stark). Chain rule, all needed probabilities, prediction, and Bayes' theorem components. **[worked]**
> - **Chain rule:** $P(A_1\cap\dots\cap A_n)=P(A_1)P(A_2|A_1)\cdots P(A_n|A_1\cap\dots\cap A_{n-1})$.
> - **Likelihoods** — $P(\text{Ausblick}|Ja)$: Sonnig $2/5$, Regen $1/5$, Bewölkung $2/5$; $P(\text{Ausblick}|Nein)$: Sonnig $3/5$, Regen $2/5$, Bewölkung $0$. $P(\text{Wind}|Ja)$: Stark $2/5$, Schwach $3/5$; $P(\text{Wind}|Nein)$: Stark $3/5$, Schwach $2/5$.
> - **Prediction day 11 (Sonnig, Stark):** $P(Ja|\cdot)\propto\tfrac12\cdot\tfrac25\cdot\tfrac25=0.08$; $P(Nein|\cdot)\propto\tfrac12\cdot\tfrac35\cdot\tfrac35=0.18$. Since $0.18>0.08$ → **no baseball is played.**
> - **Bayes:** $P(x|y)=\frac{P(x)P(y|x)}{P(y)}$ — $P(x|y)$ posterior, $P(y|x)$ likelihood, $P(x)$ prior, $P(y)$ normalizing factor.
>
> See [[Naive Bayes Classifier]].

### Task 2 — SVM

> [!question]- (a) Mark support vectors, draw margin & its width. (b) Define the optimal hyperplane. (c) Why kernel functions + name two. (d) Describe regularization (slack). **[worked]**
> - **(b)** The optimal hyperplane maximizes the distance $d$ to the nearest positive and nearest negative data point.
> - **(c)** Data aren't always linearly separable; transforming all points is expensive, so **kernels** compute the transformation **implicitly** ($K(x_i,x_j)=\langle\phi(x_i),\phi(x_j)\rangle$). Examples: **linear** $K=x_i^Tx_j$; **degree-$d$ polynomial** $K=(x_i^Tx_j+c)^d$.
> - **(d)** Regularization balances margin maximization vs. classification error via a **slack variable** $\xi_i$ ($y_i(w\cdot x_i+b)\ge1-\xi_i$). Minimize $\|w\|^2 + C\sum_i\xi_i$: high $C$ = strict (risks overfitting/noise sensitivity), low $C$ = more tolerated errors (better generalization).
>
> See [[Support Vector Machine]].

### Task 3 — Bayesian networks

> [!question]- (a) Conditional probabilities by counting. (b) What to do with incomplete data. (c) Factorization of $P(A,B,C)$ for the given structure ($A\to B$, $A\to C$). **[worked]**
> - **(a)** e.g. $P(B{=}0|A{=}0)=2/5$, $P(B{=}1|A{=}0)=3/5$, $P(B{=}0|A{=}1)=0$, $P(B{=}1|A{=}1)=1$.
> - **(b)** **Expectation-Maximization**: complete the data by statistical inference → re-estimate parameters → iterate to convergence.
> - **(c)** $P(A,B,C)=P(A)\cdot P(B|A)\cdot P(C|A)$.
>
> See [[Naive Bayes Classifier]], [[Maximum Likelihood Estimation]].

### Task 4 — kNN

> [!question]- (a) Explain hyperparameter, overfitting, regularization for kNN. (b) Three problems of kNN for 100 000 persons × 1000 features. (c) Training accuracy of kNN at $k=1$?
> - **(a)** **Hyperparameter** = $k$ (number of neighbours). **Overfitting** = too small $k$ (single outliers dominate). **Regularization** = choosing a suitable $k$.
> - **(b)** **High compute cost** (distance to all points on large data); **curse of dimensionality** (1000 features → feature space becomes exponentially sparse, needs exponentially many examples); **irrelevant features** (many of the 1000 features add noise).
> - **(c) 100 %** on the training set — at $k=1$ each point is its own nearest neighbour, hence always classified correctly.
>
> See [[K-Nearest Neighbors]], [[Curse of Dimensionality]], [[Overfitting]].

### Task 6 — CART / Gini + Precision/Recall `*`

> [!question]- (a) Root node via CART/Gini (baseball, Ausblick 3-valued & Wind). (b) Precision & recall from a small prediction table at threshold 0.25. **[worked]**
> **(a) Ausblick:** $Gini(Sonne)=0.48$, $Gini(Regen)=0.\overline4$, $Gini(Bewölkung)=0$ → $Gini(Ausblick)=\tfrac{5}{10}0.48+\tfrac{3}{10}0.\overline4+\tfrac{2}{10}0=0.37\overline3$, gain $=1-0.37\overline3=0.62\overline6$.
> **Wind:** $Gini(Schwach)=0.48$, $Gini(Stark)=0.48$ → $Gini(Wind)=0.48$, gain $=0.52$.
> **Ausblick has the lowest Gini / highest gain → root node.**
> **(b)** From the threshold-0.25 table: $TP=3, FP=1, FN=0, TN=2$ → **Precision $=\tfrac{3}{4}=0.75$**, **Recall $=\tfrac{3}{3}=1$**.
>
> See [[CART (Decision Tree)]], [[Gini Index]], [[Precision and Recall]].

### Task 7 — Neural network `*`

> [!question]- Net with ReLU (middle layer), $y^*=0.4$, $L(W)=\tfrac12\|g-y^*\|^2$, $\alpha=0.2$; inputs $0.75,0.42$; weights $w_1{=}-0.2,w_2{=}0.3,w_3{=}-0.5,w_4{=}1.2,w_5{=}0.4,w_6{=}0.8$. Forward, loss, backprop $w_5,w_6$, and the 4 gradient-descent steps. **[worked]**
> **Forward:** $f(h_1)=\max(0,-0.024)=0$; $f(h_2)=\max(0,0.129)=0.129$; $g=\max(0,0.129\cdot0.8)=\mathbf{0.1032}$.
> **Loss:** $L=\tfrac12(0.1032-0.4)^2=\mathbf{0.04404512}$.
> **Backprop** ($w^{new}=w-\alpha(g-y^*)\frac{\partial g}{\partial w}$): $w_5'=0.4-0.2(-0.2968)\cdot0=\mathbf{0.4}$ (dead ReLU $f(h_1)=0$); $w_6'=0.8-0.2(-0.2968)\cdot0.129=\mathbf{0.80765744}$.
> **4 GD steps:** **Data** (pick sample: single = SGD, subset = mini-batch, all = batch GD) → **Forward-Pass** (compute output + error) → **Backward-Pass** (backprop gradients) → **Update** (adjust weights).
>
> See [[Multilayer Perceptron]], [[Backpropagation]], [[Stochastic Gradient Descent]].

### Further tasks (recycled)

> [!question]- Also on the exam: bagging vs. boosting (2 commonalities + 2 differences), bias/variance dartboard, class-weighting (add 300 to A / 150 to B → $A_{new}=500,B_{new}=250$), price-prediction as regression with MSE + derivative.
> See SoSe 2021 Tasks 14–15, WiSe 2021/22 Tasks 1 & 3, and [[Bagging]], [[Boosting]], [[Bias-Variance Tradeoff]].

## Exam SoSe 2023 ✅ verified

> [!NOTE] Format
> Total **100 points**, **10 tasks**. Handwritten cheat sheet + non-programmable calculator allowed. Worked numbers below are from the official student solution (T. Huisinga); where the original protocol gave no data, a plausible substitute dataset is used (flagged inline).

### Task 1 — Multiple Choice (6 P.)

> [!question]- Six single-choice questions (exactly one correct answer each).
> **1. Which statement about linear regression (least squares) is _false_?** → **"Robust against outliers"** — least squares is *sensitive* to outliers (squared residuals give large errors high weight). The other three (sensitive to outliers, explainable model, residuals assumed normally distributed) are true.
> **2. When is accuracy sensibly applicable?** → **"Class distributions balanced."** On imbalanced data accuracy is misleading.
> **3. Which property do decision trees have?** → **"Non-parametric & supervised."** They don't guarantee an optimal tree (greedy), aren't limited to classification (also regression), and are interpretable (not black-box).
> **4. Components of bagging?** → **"Aggregation and Bootstrapping."**
> **5. Which property does kNN have?** → **"Runtime scales linearly with the number of training points"** — kNN is a lazy learner that *stores* all training data and searches it at inference (naively $O(n)$ per query).
> **6. Good on training data, poor on test data — what is it?** → **"Overfitting."**
>
> See [[Linear Regression]], [[Precision and Recall]], [[CART (Decision Tree)]], [[Bagging]], [[K-Nearest Neighbors]], [[Overfitting]].

### Task 2 — Basics (9 P.)

> [!question]- 2a (3 P.) Assign classification / regression / clustering to three examples; justify each in one sentence.
> - a) *Predict future TU research funding* → **Regression** (continuous numeric target).
> - b) *Group people with similar movie taste* → **Clustering** (no labels, find groups by similarity).
> - c) *Predict party preferences of dogs* → **Classification** (discrete categorical target — though semantically nonsensical, it's a discrete-label prediction).
>
> See [[Classification and Regression]].

> [!question]- 2b (6 P.) Compute metrics for "hate speech" (100 posts, split hate/no-hate, given correct/incorrect). FPR, TNR, precision, recall, accuracy, F1. **[worked]**
> Hate speech = positive class. The official solution assumes **TP = 23, FP = 10, TN = 47, FN = 20**:
> - **FPR** $=\frac{FP}{FP+TN}=\frac{10}{57}\approx\mathbf{0.175}$
> - **TNR** $=\frac{TN}{TN+FP}=\frac{47}{67}\approx\mathbf{0.701}$
> - **Precision** $=\frac{TP}{TP+FP}=\frac{23}{33}\approx\mathbf{0.\overline{69}}$
> - **Recall** $=\frac{TP}{TP+FN}=\frac{23}{43}\approx\mathbf{0.535}$
> - **Accuracy** $=\frac{TP+TN}{100}=\frac{70}{100}=\mathbf{0.6}$
> - **F1** $=\frac{2PR}{P+R}=\frac{23}{38}\approx\mathbf{0.605}$
>
> See [[Confusion Matrix]], [[Precision and Recall]].

### Task 3 — Decision Trees, ID3 (11 P.)

> [!question]- 3a (9 P.) ID3: compute entropy and information gain for a given feature; show intermediate steps.
> - **Entropy** of a set $S$ with class proportions $p_i$:
> $$H(S) = -\sum_i p_i \log_2 p_i$$
> - **Information gain** of splitting on feature $A$:
> $$IG(S,A) = H(S) - \sum_{v \in \text{values}(A)} \frac{|S_v|}{|S|}\,H(S_v)$$
> Steps: (1) compute $H(S)$ of the parent, (2) partition by feature values, (3) compute each subset entropy $H(S_v)$, (4) subtract the weighted sum.
>
> See [[Entropy and Information Gain]], [[ID3 (Decision Tree)]], [[CART (Decision Tree)]].

> [!question]- 3b (2 P.) Given two computed information gains, explain which feature is selected and why.
> ID3 selects the feature with the **highest information gain** (largest reduction in entropy / greatest impurity decrease) as the split at each node.

### Task 4 — Naive Bayes (5 P.)

> [!question]- Table predicting hay fever from weather + one other feature (2 features) over 10 days.
> **4a (6 P.)** State all probabilities needed to apply the classifier for arbitrary predictions (i.e. compute probabilities and set up the formula).
> **4b (5 P.)** Compute the prediction for the 11th day + steps.
> **4c** Explain the central assumption of Naive Bayes (independence).
>
> **Method:** For classes $c$ and features $x_1,\dots,x_d$, Naive Bayes predicts
> $$\hat{y} = \arg\max_c\; P(c)\prod_{j=1}^{d} P(x_j \mid c)$$
> - **4a:** estimate the **priors** $P(c)$ (class frequencies) and the **conditional likelihoods** $P(x_j = v \mid c)$ for every feature value $v$ and class $c$ from the table (relative frequencies).
> - **4b:** for the day-11 feature values, compute $P(c)\prod_j P(x_j\mid c)$ for each class, pick the larger; optionally normalize to a probability.
> - **4c:** the "naive" assumption is **conditional independence** of the features given the class — this factorizes the joint likelihood into a product, drastically reducing the parameters to estimate.
>
> See [[Naive Bayes Classifier]].

### Task 5 — Ensembles (12 P.)

> [!question]- 5a (5 P.) Summarize graphs with majority vote (like the exercise sheets).
> Combine the individual base-classifier predictions per instance by **majority vote**: the class predicted by most base learners wins (ties broken by a rule/random). This is the aggregation step of [[Bagging]].

> [!question]- 5b (7 P.) AdaBoost: 1-D dataset with weights, compute the **second iteration** — weighted error, voting weight $\alpha^{(2)}$, and updated (normalized) weights — for the decision rule $x \le 2 \Rightarrow +$. **[worked]**
> **Data:** $(2,+,0.1),(4,-,0.25),(5,-,0.5),(6,+,0.3)$. *(Weights are the exam's placeholder values; the official solution uses them as-is.)*
> **Given formulas:** $\alpha_i^2=\big(\tfrac12\ln\frac{1-err_i}{err_i}\big)^2$ and reweighting $w_k^{(i+1)}=w_k^{(i)}\,e^{-\alpha_i^2\, t_k y_i(x_k)}$ (with $t_k y_i=+1$ if correct, $-1$ if wrong).
> **Predictions of $x\le2\Rightarrow+$:** $x{=}2\to+$ ✓, $x{=}4\to-$ ✓, $x{=}5\to-$ ✓, $x{=}6\to-$ ✗. Only $x{=}6$ misclassified → **weighted error $err = w_4 = 0.3$**.
> - **Voting weight (asked as $\alpha^2$):** $\alpha=\tfrac12\ln\frac{1-0.3}{0.3}\approx0.4236$, so $\alpha^2\approx\mathbf{0.1795}$.
> - **Reweight** (using $\alpha^2$ in the exponent): $w_1=0.1e^{-0.1795}\approx0.0836$, $w_2=0.25e^{-0.1795}\approx0.2089$, $w_3=0.5e^{-0.1795}\approx0.4178$, $w_4=0.3e^{+0.1795}\approx0.3590$; sum $\approx1.0693$.
> - **Normalized:** $w_1\approx\mathbf{0.0782}$, $w_2\approx\mathbf{0.1954}$, $w_3\approx\mathbf{0.3907}$, $w_4\approx\mathbf{0.3357}$.
>
> *(Note: this exam plugged $\alpha^2$ into the reweighting exponent — a quirk of its given formulas. The SoSe 2024/2025 AdaBoost tasks below use the standard $\alpha$.)* See [[AdaBoost]], [[Boosting]].

### Task 6 — kNN (11 P.)

> [!question]- 6a (3 P.) Given a +/− scatter with axes $x_1,x_2$, predict (+/−) for $k \in \{1,3,5\}$.
> For each $k$: find the $k$ nearest neighbours (Euclidean distance) of the query point and take the **majority label**. The prediction can flip with $k$ (e.g. a nearby $+$ dominates at $k{=}1$ but is outvoted by more distant $-$ at $k{=}5$).

> [!question]- 6b (2 P.) Describe the training and inference process of kNN in 2–3 sentences.
> **Training:** kNN is a **lazy learner** — it simply **stores** the labeled training data, no model is fitted. **Inference:** for a query point, compute the distance to all stored points, take the $k$ closest, and predict by majority vote (classification) / mean (regression).
>
> See [[K-Nearest Neighbors]], [[Distance Metrics in Machine Learning]].

### Task 7 — Clustering (13 P.)

> [!question]- 7a (4 P.) Briefly explain the two presented clustering principles.
> - **Partitional** (e.g. **k-means**): divide the data into a fixed number $k$ of non-overlapping clusters by optimizing an objective (minimize within-cluster variance).
> - **Hierarchical** (agglomerative/divisive): build a tree (dendrogram) of nested clusters by successively merging (or splitting) clusters according to a linkage criterion — no fixed $k$ needed upfront.
>
> See [[Clustering]], [[k-Means Clustering]], [[Hierarchical Clustering]].

> [!question]- 7b (3 P.) Clusters $A=\{1,3\}$, $B=\{7,8\}$, absolute difference as distance. Compute complete-, single-, and average-linkage distance.
> Pairwise absolute distances: $|1-7|{=}6,\ |1-8|{=}7,\ |3-7|{=}4,\ |3-8|{=}5$.
> - **Complete-linkage** (max): $\max(6,7,4,5) = \mathbf{7}$.
> - **Single-linkage** (min): $\min(6,7,4,5) = \mathbf{4}$.
> - **Average-linkage** (mean of all pairs): $\frac{6+7+4+5}{4} = \frac{22}{4} = \mathbf{5.5}$.
>
> See [[Hierarchical Clustering]].

> [!question]- 7c (4 P.) Three identical plots — draw the k-means steps and name/explain them (schematic, no values).
> **k-means iteration:** (1) **Initialize** $k$ cluster centroids. (2) **Assignment step** — assign each point to its nearest centroid. (3) **Update step** — move each centroid to the mean of its assigned points. (4) **Repeat** 2–3 until assignments no longer change (convergence). The given "wrong-diagonal" elongated clusters illustrate a poor initialization that k-means can get stuck in (local optimum).
>
> See [[k-Means Clustering]].

### Task 8 — SVM (11 P.)

> [!question]- 8a (3 P.) Draw optimal one-vs-rest hyperplanes in a 3-class plot (schematic, without margin/support vectors).
> One-vs-rest: **one hyperplane per class**, separating that class from all others → 3 lines for 3 classes.

> [!question]- 8b (2 P.) How is the optimal hyperplane defined?
> The hyperplane that **maximizes the margin** — the distance to the nearest training points of either class (the **support vectors**). Equivalently, it minimizes $\tfrac12\|w\|^2$ subject to all points being correctly classified with margin $\ge 1$.

> [!question]- 8c (2 P.) Which mathematical trick allows SVMs on non-linearly separable problems? What is the underlying intuition?
> The **kernel trick**: implicitly map inputs into a higher-dimensional feature space via $\phi(x)$ where the data becomes linearly separable, computing only inner products $K(x,x') = \langle\phi(x),\phi(x')\rangle$ **without ever forming $\phi$ explicitly**. Intuition: a problem not linearly separable in the input space often *is* linearly separable in a higher-dimensional space.

> [!question]- 8d (4 P.) How can an occasional misclassification be allowed? Name the intuition and the necessary change. What does this mean for the optimization problem?
> Introduce **slack variables** $\xi_i \ge 0$ (**soft margin**): each point may violate the margin by $\xi_i$. The objective becomes $\min \tfrac12\|w\|^2 + C\sum_i \xi_i$, where $C$ trades off margin width against total violation. Intuition: tolerate a few misclassified/inside-margin points to get a wider, more robust margin and avoid overfitting to noise.
>
> See [[Support Vector Machine]].

### Task 9 — Neural Networks (14 P.)

> [!question]- Neural net with ReLU, $L(W)=\tfrac12\|g-y^*\|_2^2$, $y^*=0.4$, $\alpha=0.2$ (same values as SoSe 2020). Inputs $x_1{=}0.75,x_2{=}0.42$; weights $w_1{=}-0.2,w_2{=}0.3,w_3{=}-0.5,w_4{=}1.2,w_5{=}0.4,w_6{=}0.8$. **[worked]**
> **9a Forward pass & error:**
> - $x_3=0.75(-0.2)+0.42\cdot0.3=-0.024\Rightarrow f(x_3)=0$
> - $x_4=0.75(-0.5)+0.42\cdot1.2=0.129\Rightarrow f(x_4)=0.129$
> - $x_5=0\cdot0.4+0.129\cdot0.8=0.1032\Rightarrow \mathbf{g=0.1032}$
> - $L=\tfrac12(0.1032-0.4)^2=\mathbf{0.04404512}$
> **9b Backprop** ($w^{new}=w-\alpha(g-y^*)\frac{\partial g}{\partial w}$, with $g-y^*=-0.2968$):
> - $w_5'=0.4-0.2(-0.2968)\cdot f(x_3)=0.4-0.2(-0.2968)\cdot0=\mathbf{0.4}$ (dead ReLU)
> - $w_6'=0.8-0.2(-0.2968)\cdot f(x_4)=0.8-0.2(-0.2968)\cdot0.129=\mathbf{0.80765744}$
> **9c Four SGD steps:** (1) **Data** — draw a random sample; (2) **Forward-Pass** — output + error; (3) **Backward-Pass** — backprop gradients output→input; (4) **Update** — $w^{new}=w-\alpha\frac{\partial L}{\partial w}$.
>
> See [[Multilayer Perceptron]], [[Backpropagation]], [[Stochastic Gradient Descent]], [[Loss Functions in Machine Learning]].

### Task 10 — CNN (8 P.)

> [!question]- Input 4×4, filter 2×2, stride 1, no padding. **[worked]** (substitute values from the official solution)
> Input $\begin{smallmatrix}1&7&4&2\\8&1&2&5\\3&6&1&1\\3&2&5&1\end{smallmatrix}$, filter $\begin{smallmatrix}2&0\\1&3\end{smallmatrix}$. Output size $O=\lfloor(4-2+0)/1\rfloor+1=3$ → **3×3**.
> **10a Convolution** (elementwise-multiply & sum each 2×2 window; e.g. top-left $1\cdot2+7\cdot0+8\cdot1+1\cdot3=13$):
> $$\begin{bmatrix}13&21&25\\37&11&8\\15&29&10\end{bmatrix}$$
> **10b Max pooling** (max of each 2×2 window):
> $$\begin{bmatrix}8&7&5\\8&6&5\\6&6&5\end{bmatrix}$$
> **10c Output size** for 1×1 filter, stride 2, 1×1 zero-padding on the 4×4 input: $O=\lfloor(4-1+2\cdot1)/2\rfloor+1=\mathbf{3}$ → 3×3.
>
> See [[Convolutional Neural Network]].

---

## Exam SoSe 2024

> [!NOTE] Format
> Total **100 points**, **10 tasks**, 120 min. Handwritten cheat sheet + non-programmable calculator. Largely equivalent to SoSe 2023.

### Task 1 — Single Choice (6 P.)

> [!question]- Six single-choice questions (equivalent to SoSe 2023).
> **1. Property of decision trees?** → **"Non-parametric and supervised."**
> **2. When is accuracy sensibly applicable?** → **"Class distributions balanced."**
> **3. Perfect on training, poor on test — what is it?** → **"Overfitting."**
> **4. Property of kNN with 9 features/dimensions?** → **"Has linear runtime"** (in the number of training points). Note: 9 dimensions hints at the [[Curse of Dimensionality]], but the correct property here is the linear query cost.
> **5. Components of bagging?** → **"Aggregation + bootstrapping."**
> **6. Which statement about linear regression is _false_?** → **"Is robust against outliers."**
>
> See Task 1 of SoSe 2023 above for the reasoning.

### Task 2 — Basics

> [!question]- 2a Assign classification / regression / clustering; justify.
> - a) *Group students with similar module choices* → **Clustering** (unlabeled grouping by similarity).
> - b) *Predict Offenbach's population in 2024* → **Regression** (continuous numeric target).
> - c) *Genre recommendation for music providers* → **Classification** (discrete category / label).

> [!question]- 2b Confusion-matrix metrics — 1000 trees, pest-infested (positive) vs. pest-free (negative). **[worked]**
> Given (protocol notes values are uncertain): TP = 400, FP = 100, TN = 300, FN = 200.
> - **FPR** $=\frac{FP}{FP+TN}=\frac{100}{400}=\mathbf{0.25}$
> - **TNR** $=\frac{TN}{TN+FP}=\frac{300}{400}=\mathbf{0.75}$
> - **Precision** $=\frac{TP}{TP+FP}=\frac{400}{500}=\mathbf{0.80}$
> - **Recall** $=\frac{TP}{TP+FN}=\frac{400}{600}\approx\mathbf{0.667}$
> - **Accuracy** $=\frac{TP+TN}{1000}=\frac{700}{1000}=\mathbf{0.70}$
> - **F1** $=\frac{2PR}{P+R}=\frac{2\cdot0.8\cdot0.667}{0.8+0.667}\approx\mathbf{0.727}$
>
> See [[Confusion Matrix]], [[Precision and Recall]].

### Task 3 — Decision Trees, ID3

> [!question]- Table with 12 rows, 2 features (season/catering), output = students' mood.
> **3a** ID3: compute entropy and information gain for features *season* and *catering*. **3b (2 P.)** Explain the split criterion.
> Method identical to SoSe 2023 Task 3: entropy $H(S)=-\sum p_i\log_2 p_i$, gain $IG(S,A)=H(S)-\sum_v \frac{|S_v|}{|S|}H(S_v)$; **split on the feature with the highest information gain**.
>
> See [[Entropy and Information Gain]], [[ID3 (Decision Tree)]].

### Task 4 — kNN

> [!question]- 4a (3 P.) 7 +/− points; predict for a given point at $k=1/3/7$. 4b (2 P.) Describe training & inference.
> Same as SoSe 2023 Task 6. Majority vote over the $k$ nearest neighbours; kNN is a lazy learner (stores data, computes distances at query time). See [[K-Nearest Neighbors]].

### Task 5 — Ensembles

> [!question]- 5a Explain bagging and boosting.
> See SoSe 2021 Task 5. [[Bagging]] = parallel learners on bootstrap samples, aggregate by vote → reduces variance. [[Boosting]] = sequential learners each focusing on prior errors → reduces bias.

> [!question]- 5b (4 P.) Are ensemble methods a solution to the No-Free-Lunch problem? What role do they play?
> **No.** The **No-Free-Lunch theorem** says no single algorithm is best across *all* possible problems — ensembles don't escape this. What ensembles do is **reduce error on typical real-world problems** by combining diverse models: bagging lowers variance, boosting lowers bias, and combining complementary learners is more robust than any single one. They improve average-case, not universal, performance.
>
> See [[No Free Lunch Theorem]], [[Bagging]], [[Boosting]].

> [!question]- 5c (7 P.) AdaBoost second iteration, rule $x \le 2 \Rightarrow +$. **[worked]**
> **Data:** $(3,+,0.1),(4,+,0.25),(2,+,0.5),(4,-,0.15)$ (sum = 1).
> **Predictions of $x\le2\Rightarrow+$:** $x{=}3\to-$ ✗ (true $+$), $x{=}4\to-$ ✗ (true $+$), $x{=}2\to+$ ✓, $x{=}4\to-$ ✓. Misclassified: the two $+$ points at $x{=}3$ and $x{=}4$.
> - **Weighted error:** $\varepsilon^{(2)} = 0.1 + 0.25 = \mathbf{0.35}$.
> - **Voting weight:** $\alpha^{(2)} = \tfrac12\ln\frac{1-0.35}{0.35} = \tfrac12\ln(1.857) \approx \mathbf{0.310}$.
> - **Reweight** ($e^{-\alpha}\approx0.734$ correct, $e^{+\alpha}\approx1.363$ wrong), then normalize (sum before norm $\approx 0.954$):
>   - $w_1$ (x=3, wrong): $0.1\cdot1.363/0.954 \approx \mathbf{0.143}$
>   - $w_2$ (x=4, wrong): $0.25\cdot1.363/0.954 \approx \mathbf{0.357}$
>   - $w_3$ (x=2, correct): $0.5\cdot0.734/0.954 \approx \mathbf{0.385}$
>   - $w_4$ (x=4, correct): $0.15\cdot0.734/0.954 \approx \mathbf{0.115}$
> - Sanity check: misclassified weights sum to $0.5$ and correct ones to $0.5$ (a general AdaBoost property after reweighting).
>
> See [[AdaBoost]].

### Task 6 — Clustering

> [!question]- 6a Explain the two clustering principles. 6b Linkage on $A=\{1,3\}$, $B=\{7,8\}$. 6c k-means steps.
> Identical to SoSe 2023 Task 7: partitional vs. hierarchical; **single = 4, complete = 7, group-average = 5.5**; k-means = init → assign → update → repeat. See [[Hierarchical Clustering]], [[k-Means Clustering]].

### Task 7 — Naive Bayes

> [!question]- Table: whether baseball is played, features outlook (sunny/overcast/rain) + wind (weak/strong), 10 days.
> **7a** all probabilities needed; **7b** prediction for day 11; **7c** the general Naive Bayes assumption.
> Method identical to SoSe 2023 Task 4: priors $P(c)$ + conditionals $P(x_j\mid c)$; predict $\arg\max_c P(c)\prod_j P(x_j\mid c)$; assumption = **conditional independence of features given the class**.
>
> See [[Naive Bayes Classifier]].

### Task 8 — SVM

> [!question]- Same four sub-questions as SoSe 2023 Task 8: one-vs-rest hyperplanes; optimal hyperplane; kernel trick; slack variables.
> See SoSe 2023 Task 8 and [[Support Vector Machine]].

### Task 9 — SGD

> [!question]- Given $y^*=0.4$, $\alpha=0.2$, $f=$ ReLU, $L(W)=\tfrac12(g-y^*)^2$; inputs $x_1{=}0.5, x_2{=}0.4$; weights $w_1{=}0.1, w_2{=}0.9, w_3{=}0.5, w_4{=}-1.1, w_5{=}-0.4, w_6{=}0.8$.
> **9a** forward pass ($g$, $L$); **9b** general GD update rule + update $w_5, w_6$; **9c** the four steps of one SGD iteration (forward pass, backward pass, data, update).
> Method as SoSe 2021 Task 2 / SoSe 2025 Task 9 (worked below): forward-propagate through the ReLU hidden layer to $g$, $L=\tfrac12(g-y^*)^2$; $w\leftarrow w-\alpha\frac{\partial L}{\partial w}$ via chain rule; dead ReLUs zero the gradient.
>
> See [[Multilayer Perceptron]], [[Backpropagation]], [[Stochastic Gradient Descent]].

### Task 10 — CNN (8 P.)

> [!question]- Input matrix 3×3 with values.
> **10a (2 P.)** Max pooling both axes: 2×2 filter, no padding, stride 1. **10b (4 P.)** 2-D convolution, 2×2 kernel, no padding, stride 1. **10c (2 P.)** Output size for 1×1 filter, 1×1 zero padding, stride 2.
> - 3×3 input, 2×2 filter, stride 1, no padding → $O=(3-2)/1+1 = \mathbf{2}$ → **2×2** output (both conv and pooling).
> - Convolution: elementwise-multiply & sum each 2×2 window; pooling: max of each window.
> - 10c size: $O=\lfloor(N-1+2\cdot1)/2\rfloor+1$ (apply to the current feature-map size $N$).
>
> See [[Convolutional Neural Network]] and the worked convolution in SoSe 2025 Task 10.

---

## Exam SoSe 2025

> [!NOTE] Format
> Total **100 points**, **10 tasks**, 120 min. 2-page handwritten cheat sheet + non-programmable calculator. Grade boundaries: ≥ 91.5 P for 1.0, ≥ 50 P for 4.0. Time is sufficient if you work through without long pauses.

### Task 1 — Single Choice (5 P.)

> [!question]- Five single-choice questions.
> **1. Good on training, poor on test?** → **Overfitting.**
> **2. Which statement about least-squares linear regression is _false_?** → **"Robust against outliers."**
> **3. Which statement about random forests is _correct_?** → **"They use smaller trees than [plain] decision trees"** — random forests aggregate many trees each trained on a bootstrap sample + random feature subset (not all features), boosting is *not* a generalization of random forests, and a forest is *less* interpretable than a single tree. (Of the given options this is the intended correct one.)
> **4. Which statement about the curse of high dimensions is _false_?** → **"The number of required data points grows _polynomially_ with the dimension"** — it grows **exponentially**. The others are true.
> **5. What is a validation set used for?** → **"Hyperparameter selection."**
>
> See [[Overfitting]], [[Linear Regression]], [[Random Forest]], [[Curse of Dimensionality]], [[Cross-Validation]].

### Task 2 — Basics (9 P.)

> [!question]- (3 P.) Assign clustering / regression / classification.
> - a) *Group people with similar music taste* → **Clustering.**
> - b) *Recommend a degree programme* → **Classification** (discrete category).
> - c) *Predict GPU load* → **Regression** (continuous target).

> [!question]- (4 P.) Build the confusion matrix and compute FNR, precision, recall, accuracy — 100 points, 20 with / 80 without diabetes. **[worked]**
> Given: 15 diabetic **not** detected → **FN = 15**; 5 diabetic correctly detected → **TP = 5**; 70 healthy correct → **TN = 70**; 10 healthy flagged as diabetic → **FP = 10**. (Check: positives $=20=TP+FN$, negatives $=80=TN+FP$.)
> - **FNR** $=\frac{FN}{FN+TP}=\frac{15}{20}=\mathbf{0.75}$
> - **Precision** $=\frac{TP}{TP+FP}=\frac{5}{15}\approx\mathbf{0.333}$
> - **Recall** $=\frac{TP}{TP+FN}=\frac{5}{20}=\mathbf{0.25}$
> - **Accuracy** $=\frac{TP+TN}{100}=\frac{75}{100}=\mathbf{0.75}$

> [!question]- (2 P.) Why is accuracy not sensible here? What to use instead?
> The classes are **heavily imbalanced** (20 vs. 80): a trivial "always healthy" classifier already scores 80 % accuracy while catching **zero** diabetics. Here recall is only 0.25 despite 0.75 accuracy. Use **precision/recall, F1-score, balanced accuracy, or ROC-AUC** instead — metrics that account for the minority (positive) class.
>
> See [[Confusion Matrix]], [[Precision and Recall]], [[ROC Curve]].

### Task 3 — Decision Trees (11 P.)

> [!question]- Table with 12 rows: sleep quality (good/bad) vs. sport (yes/no) and coffee (much/little/none).
> **3a (9 P.)** Compute entropy and information gain for the feature *coffee*. **3b (2 P.)** If Gain(Sport) = 0.42 and Gain(Coffee) = 0.69, which feature do you split on and why? (These values are not the answer to 3a.)
> - **3a:** entropy $H(S)=-\sum p_i\log_2 p_i$ over the sleep-quality classes; partition rows by coffee ∈ {much, little, none}; gain $= H(S) - \sum_v \frac{|S_v|}{|S|}H(S_v)$. Show each subset's entropy.
> - **3b:** split on **Coffee** — it has the **higher information gain** (0.69 > 0.42), i.e. it reduces entropy the most.
>
> See [[Entropy and Information Gain]], [[ID3 (Decision Tree)]].

### Task 4 — kNN (7 P.)

> [!question]- Diagram with a "sun" (query), 3× + and 4× −. (a, 3 P.) Predict for $k=1,3,7$ (visual, Euclidean). (b, 2 P.) Describe training & inference. (c, 2 P.) What if $k=4$ (tie)? Name two tie-break strategies.
> - **a:** majority vote over the $k$ nearest points. At $k=7$ (all points) the majority is **−** (4 vs. 3).
> - **b:** lazy learner — store data at "training"; at inference compute distances, take $k$ nearest, majority vote.
> - **c:** on a tie (equal +/−): (1) use **distance-weighted** voting (closer neighbours count more); (2) pick an **odd $k$** / decrement $k$ by 1; alternatively break ties toward the nearest single neighbour or the more frequent global class.
>
> See [[K-Nearest Neighbors]].

### Task 5 — Ensemble Methods (12 P.)

> [!question]- (a, 3 P.) Explain boosting and bagging in your own words. (b, 2 P.) Name and explain one advantage and one disadvantage of ensembles.
> - **a:** see SoSe 2021 Task 5 — [[Bagging]] (parallel, bootstrap, vote, ↓ variance) vs. [[Boosting]] (sequential, focus on errors, ↓ bias).
> - **b:** **Advantage** — higher accuracy/robustness and better generalization than a single model (variance and/or bias reduction). **Disadvantage** — loss of interpretability and higher computational/memory cost (many models to train and store); boosting can also overfit noisy data.

> [!question]- (c, 7 P.) AdaBoost second iteration, rule $x \le 3 \Rightarrow +$. **[worked]**
> **Data:** $(2,+,0.15),(3,+,0.45),(1,-,0.30),(4,-,0.10)$ (sum = 1).
> **Predictions of $x\le3\Rightarrow+$:** $x{=}2\to+$ ✓, $x{=}3\to+$ ✓, $x{=}1\to+$ ✗ (true $-$), $x{=}4\to-$ ✓. Only $x{=}1$ misclassified.
> - **Weighted error:** $\varepsilon^{(2)} = 0.30 = \mathbf{0.30}$.
> - **Voting weight:** $\alpha^{(2)} = \tfrac12\ln\frac{1-0.3}{0.3} = \tfrac12\ln(2.333) \approx \mathbf{0.424}$.
> - **Reweight** ($e^{-\alpha}\approx0.655$ correct, $e^{+\alpha}\approx1.528$ wrong), normalize (sum before norm $\approx 0.917$):
>   - $w_1$ (x=2, correct): $0.15\cdot0.655/0.917 \approx \mathbf{0.107}$
>   - $w_2$ (x=3, correct): $0.45\cdot0.655/0.917 \approx \mathbf{0.321}$
>   - $w_3$ (x=1, wrong): $0.30\cdot1.528/0.917 \approx \mathbf{0.500}$
>   - $w_4$ (x=4, correct): $0.10\cdot0.655/0.917 \approx \mathbf{0.071}$
> - Check: misclassified point now carries weight $0.5$; the three correct ones sum to $0.5$.
>
> See [[AdaBoost]].

### Task 6 — Clustering (11 P.)

> [!question]- (a, 4 P.) Name the clustering methods; which does k-means belong to? (b, 4 P.) Draw two k-means steps and explain. (c, 3 P.) Draw how you would cluster + how to choose k-means centroids optimally.
> - **a:** the two families are **hierarchical** and **partitional**; **k-means is partitional**.
> - **b:** assignment step (assign points to nearest centroid) → update step (recompute centroids as cluster means), repeated to convergence.
> - **c:** with 3 visible clusters — (1) **choose k** using prior knowledge / a good guess (or the elbow method), (2) **initialize centroids spread apart** (e.g. k-means++), well-separated, for fast convergence and to avoid poor local optima.
>
> See [[k-Means Clustering]], [[Hierarchical Clustering]].

### Task 7 — Naive Bayes (14 P.)

> [!question]- T1–T9 for frog/toad, with Skin = {moist/dry}, Legs = {short/medium/long}.
> **(a, 6 P.)** State all probabilities needed for the frog prediction. **(b, 5 P.)** Predict T10 (short, moist) — answer should be **toad**. **(c, 3 P.)** Given real income, declared income, predicted (tax) fraud — is the "naive" independence assumption satisfied? Why / why not?
> - **a/b:** priors $P(\text{frog}), P(\text{toad})$ and conditionals $P(\text{legs}\mid\cdot), P(\text{skin}\mid\cdot)$; predict $\arg\max_c P(c)P(\text{short}\mid c)P(\text{moist}\mid c)$.
> - **c:** **No.** Real income and declared income are **not conditionally independent given the fraud label** — fraud is defined precisely by their *mismatch* (declared ≠ real ⇒ fraud), so the two features are strongly dependent; the Naive Bayes independence assumption is **violated**.
>
> See [[Naive Bayes Classifier]].

### Task 8 — SVM (9 P.)

> [!question]- Graph with 3 clusters. (a, 3 P.) Draw one-vs-one hyperplanes. (b, 2 P.) How does the number of hyperplanes grow with the number of classes in one-vs-one? Which strategy is more optimal? (c, 2 P.) Kernel trick + which K-function for a given scenario. (d, 2 P.) Describe a $\phi(x)$ that makes the given points linearly separable.
> - **a:** one-vs-one → one hyperplane **per pair** of classes → for 3 classes, $\binom{3}{2}=3$ lines.
> - **b:** number of hyperplanes grows **quadratically**, $\binom{K}{2}=\frac{K(K-1)}{2}$. **One-vs-rest** needs only $K$ classifiers — cheaper for large $K$ (though each trains on all data).
> - **c:** the **kernel trick**; choose the kernel to match the data geometry — e.g. **RBF/Gaussian** for blob-like non-linear clusters, **polynomial** for polynomial boundaries.
> - **d:** give an explicit feature map, e.g. for a circular boundary $\phi(x)=(x_1, x_2, x_1^2+x_2^2)$ — the extra radial coordinate makes concentric classes linearly separable by a plane; include representative points of the distribution and a few with small error.
>
> See [[Support Vector Machine]].

### Task 9 — Neural Networks (16 P.)

> [!question]- Net with 2 inputs, ReLU in every neuron, bias in every neuron. **[worked]**
> Given $y^*=0.7$, $i_1=0.8, i_2=0.3$; $w_1{=}0.3, w_2{=}-0.7, b_1{=}0.4$; $w_3{=}0.8, w_4{=}0.3, b_2{=}0.1$; $w_5{=}0.4, w_6{=}0.6, b_3{=}-0.1$. Loss $L=\tfrac12(g-y^*)^2$, $\alpha=0.2$.
> **9a (5 P.) Forward pass + loss.**
> - $h_1 = i_1 w_1 + i_2 w_3 + b_1 = 0.24+0.24+0.4 = 0.88 \Rightarrow f(h_1)=0.88$
> - $h_2 = i_1 w_2 + i_2 w_4 + b_2 = -0.56+0.09+0.1 = -0.37 \Rightarrow f(h_2)=\mathbf{0}$ (dead ReLU)
> - $h_3 = f(h_1)w_5 + f(h_2)w_6 + b_3 = 0.352+0-0.1 = 0.252 \Rightarrow \mathbf{g=0.252}$
> - $L = \tfrac12(0.252-0.7)^2 = \tfrac12(0.448)^2 \approx \mathbf{0.1004}$
> **9b (5 P.) Update $w_5, w_6, b_3$** (rule $w\leftarrow w-\alpha\frac{\partial L}{\partial w}$). With $\frac{\partial L}{\partial g}=g-y^*=-0.448$ and $f'(h_3)=1$:
> - $\frac{\partial L}{\partial w_5}=-0.448\cdot f(h_1)=-0.448\cdot0.88=-0.394 \Rightarrow w_5' = 0.4-0.2(-0.394)\approx\mathbf{0.479}$
> - $\frac{\partial L}{\partial w_6}=-0.448\cdot f(h_2)=-0.448\cdot0=0 \Rightarrow w_6' = \mathbf{0.6}$ (unchanged — $h_2$ is dead)
> - $\frac{\partial L}{\partial b_3}=-0.448\cdot1=-0.448 \Rightarrow b_3' = -0.1-0.2(-0.448)\approx\mathbf{-0.010}$
> **9c (4 P.)** The four SGD steps after initialization: (1) draw **data** (mini-batch), (2) **forward pass** → output & loss, (3) **backward pass** (backprop) → gradients, (4) **update** weights.
> **9d (2 P.) Dropout on $f(h_2)$:** its activation is forced to $0$, so $\frac{\partial L}{\partial w_6}=\frac{\partial L}{\partial h_3}\cdot f(h_2)=0$ — **$w_6$ receives no update** (here it already didn't, since $h_2$ was dead).
>
> See [[Multilayer Perceptron]], [[Backpropagation]], [[Stochastic Gradient Descent]], [[Dropout]].

### Task 10 — Convolution (6 P.)

> [!question]- 3×3 input, 2×2 filter, no padding, stride 1, output 2×2. **[worked]**
> Input $\begin{smallmatrix}0&2&5\\-1&2&1\\1&1&0\end{smallmatrix}$, filter $\begin{smallmatrix}1&-1\\2&0\end{smallmatrix}$.
> **(a, 4 P.)** Cross-correlate each 2×2 window (elementwise multiply & sum):
> - top-left $[[0,2],[-1,2]]$: $0\cdot1+2(-1)+(-1)2+2\cdot0 = \mathbf{-4}$
> - top-right $[[2,5],[2,1]]$: $2\cdot1+5(-1)+2\cdot2+1\cdot0 = \mathbf{1}$
> - bottom-left $[[-1,2],[1,1]]$: $-1\cdot1+2(-1)+1\cdot2+1\cdot0 = \mathbf{-1}$
> - bottom-right $[[2,1],[1,0]]$: $2\cdot1+1(-1)+1\cdot2+0\cdot0 = \mathbf{3}$
> Output $= \begin{smallmatrix}-4&\;\,1\\-1&\;\,3\end{smallmatrix}$.
> **(b, 2 P.)** Convolution vs. Transformer attention — a conceptual difference: convolution uses a **fixed, local** filter with **shared weights** over a small neighbourhood (fixed receptive field), whereas attention computes **content-dependent, global** weights — every position can attend to every other, with weights derived dynamically from the data (query–key similarity) rather than being fixed parameters.
>
> See [[Convolutional Neural Network]], [[Attention Mechanism]].

---

## Exam WiSe 2025/2026

### Task 1 — Multiple Choice (6 P.)

> [!question]- Six MCQs
> - **a) Which metric measures the proportion of actual positives correctly identified as positive?** → **Recall** (= TP/(TP+FN)).
> - **c) What is boosting?** → sequential ensemble where each learner focuses on the previous learners' mistakes (reweighting/residuals), combining weak learners into a strong one. See [[Boosting]].
> - **d) Which statement about linear regression is _incorrect_?** → **"Can be natively used to solve classification problems"** — plain linear regression predicts continuous values; classification needs e.g. logistic regression. (Residuals-normally-distributed is a *correct* statement.)
> - **e) Batch/stochastic gradient descent updates the weights in an iteration based on…** → **randomly drawn subsets of training examples** (mini-batches). (A single example = pure SGD; all examples = full-batch GD.)
> - **f) What is _wrong_ about decision trees?** → **"Robust to changes in training data"** — decision trees are notoriously **high-variance / unstable**: small changes in the data can produce very different trees.
>
> See [[Precision and Recall]], [[Boosting]], [[Linear Regression]], [[Stochastic Gradient Descent]], [[CART (Decision Tree)]].

### Task 2 — Decision Trees / Information Gain (11 P.)

> [!question]- 2a Find information gain for a feature. 2b Would you take feature A (IG 0.4) or feature B (IG 0.5)? Explain.
> Same as prior years: entropy + gain; **choose feature B** — higher information gain (0.5 > 0.4) → greater impurity reduction at the split. See [[Entropy and Information Gain]], [[ID3 (Decision Tree)]].

### Task 3 — SVM (10 P.)

> [!question]- Draw one-vs-rest plot; define the optimal hyperplane; explain slack-based misclassification and its effect on the optimization; kernel trick.
> Identical to SoSe 2023/2024/2025 SVM tasks — see SoSe 2025 Task 8 and [[Support Vector Machine]]. Optimal hyperplane = max-margin; soft margin with slack $\xi_i$ and penalty $C\sum\xi_i$; kernel trick for non-linear separability.

### Task 4 — Ensembles (14 P.)

> [!question]- 4a Merge graphs by majority voting (like exercise sheet 5, Q5.3d SoSe 2025). 4b AdaBoost with rule $x > 2$, two errors — find voting weight and new normalized weights. 4c What characteristics should the early (base) learners in bagging ideally have?
> - **4a:** per-instance majority vote across the base classifiers.
> - **4b:** AdaBoost as worked in SoSe 2024/2025 — $\varepsilon = \sum_{\text{wrong}} w_i$ (two misclassified points), $\alpha=\tfrac12\ln\frac{1-\varepsilon}{\varepsilon}$, reweight ($e^{\pm\alpha}$) and normalize. See [[AdaBoost]].
> - **4c:** bagging base learners should be **low-bias, high-variance and diverse/unstable** (e.g. deep, unpruned decision trees) — bagging then averages away the variance while keeping the low bias. (Contrast with boosting, which uses high-bias weak learners.)
>
> See [[Bagging]], [[Boosting]], [[AdaBoost]].

### Task 5 — Neural Network / Backprop (15 P.)

> [!question]- NN + backprop (almost as earlier protocols). New: one neuron's **bias is zero** and the incoming gradient $\partial L/\partial g$ is **negative**. 5b: difference between SGD and gradient descent — one advantage, one disadvantage each.
> - **Backprop:** as SoSe 2025 Task 9. A zero bias just drops the $+b$ term; a negative $\partial L/\partial g$ means the output overshot below/above target and the update pushes weights the opposite way (sign flows through the chain rule as usual).
> - **5b:** **Full-batch GD** uses all data per step → smooth, accurate gradient (advantage) but slow and memory-heavy per update (disadvantage). **SGD** (mini-batch/single sample) → fast, cheap updates that can escape shallow local minima (advantage) but noisy, high-variance gradient steps that need learning-rate tuning (disadvantage).
>
> See [[Backpropagation]], [[Stochastic Gradient Descent]], [[Multilayer Perceptron]].

### Task 6 — kNN (6 P.)

> [!question]- Predict for $k=1,3,11$. What happens if $k$ is too small (draw with $k=1$)? What is the problem with small $k$?
> Majority vote over $k$ nearest. **Too small $k$ (e.g. $k=1$)** → the decision boundary is highly irregular and the model is very sensitive to **noise/outliers** → **overfitting** (high variance): a single mislabeled or noisy neighbour flips the prediction. Larger $k$ smooths the boundary (but too large → underfitting).
>
> See [[K-Nearest Neighbors]], [[Bias-Variance Tradeoff]].

### Task 7 — Clustering / k-Means (11 P.)

> [!question]- Same as SoSe 2025: compute single-, complete- and average-linkage distances.
> For the standard $A=\{1,3\}$, $B=\{7,8\}$ example: **single = 4, complete = 7, average = 5.5**. See SoSe 2023 Task 7b and [[Hierarchical Clustering]].

### Task 8 — Naive Bayes (13 P.)

> [!question]- Similar to earlier, different data. One part: given that the Naive Bayes assumption says features are independent given the class, give one example where the assumption does **not** hold.
> Prediction as usual (priors × conditionals). **Example of violated independence:** features that are causally/definitionally linked given the class — e.g. *declared income* and *real income* for fraud detection (SoSe 2025 Task 7c), or "has fever" and "has chills" given a disease, or word co-occurrences like "New" and "York" in text — these are correlated even after conditioning on the class.
>
> See [[Naive Bayes Classifier]].

### Task 9 — Bias/Variance (7 P.)

> [!question]- 9a (4 P.) A 2×2 grid of dartboard-style graphs — label each Low/High Bias × Low/High Variance.
> The classic dartboard quadrants:
> - Tight cluster **on** the bullseye → **low bias, low variance**.
> - Tight cluster **off** the bullseye → **high bias, low variance**.
> - Scattered **around** the bullseye → **low bias, high variance**.
> - Scattered **off** the bullseye → **high bias, high variance**.
>
> See [[Bias-Variance Tradeoff]]; cf. SoSe 2021 Task 11.

> [!question]- 9b When a model overfits, its variance increases significantly. Why, and how does it show up?
> An overfit model has **high capacity** and fits the training set's noise, so it depends heavily on the particular training sample → **different training sets yield very different models** (high variance). It **shows up** as a large **train–test gap**: very low training error but high test/validation error, and unstable predictions under resampling / cross-validation.
>
> See [[Overfitting]], [[Bias-Variance Tradeoff]], [[Cross-Validation]].

### Task 10 — Basics assignment (7 P.)

> [!question]- Like the "music classification" question from Exam 2020, reworded to food recipes & ingredients (e.g. "recipe images" instead of "album covers").
> Same structure as the SoSe 2023/2024/2025 Task 2a assignment: map each described scenario to **classification / regression / clustering** and justify by the nature of the target (discrete label → classification, continuous value → regression, unlabeled grouping → clustering).
>
> See [[Classification and Regression]], [[Clustering]].
