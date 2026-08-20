# [REFERENCE] Epistemic Data-Centric EDA Knowledge Substrate

> **Scope:** Theoretical reference, scientific algorithms, and mathematical definitions for the `epistemic-eda` skill.
> **Sources:** IBM Research *"A Data-centric AI"* (2023), Leandro Nunes de Castro *"Exploratory Data Analysis"* (2025/2026), John W. Tukey *"Exploratory Data Analysis"*, and Six Sigma DMAIC.

---

## 1. IBM Data-Centric AI Mathematical Formulations

### 1.1 Dataset Snapshot Algorithm (Greedy Set Cover on Bipartite Graph)
- **Objective:** Compress an $N \times K$ dataset $D_N$ into a minimal representative subset $D_S$ ($\sim 3-5\%$ of rows) that preserves $100\%$ of unique feature patterns $P(D_N)$, including rare anomalies and tail distributions.
- **Formulation:**
  - Let $P(D_N) = \bigcup_{j=1}^K P(C_j)$ be the set of all unique pattern tokens across columns.
  - Continuous columns are converted into categorical quantile bins: $C_{bin} = \text{qcut}(C, q=10)$.
  - Text strings are converted into regex syntactical forms (e.g., `dd-mm-yyyy` $\to$ `nn-nn-nnnn`).
  - Represent $D_N$ as a Bipartite Graph $G = (P, R, E)$ where $P$ is the set of pattern tokens and $R$ is the set of rows.
  - Pattern Importance Weight:
    $$I(p) = \frac{1}{\text{count}(p)}$$
    (Inversely proportional to frequency, giving maximum weight to rare events).
  - Row Importance Metric:
    $$I(r_i) = \sum_{p \in \text{uncovered}(r_i)} I(p)$$
  - **Greedy Optimization:** At each step, select $r^* = \arg\max_{r_i} I(r_i)$, add $r^*$ to $D_S$, mark covered patterns as covered ($I(p) = 0$), and repeat until $P(D_S) = P(D_N)$.

---

### 1.2 Column Interestingness Engine (Ranking System)
Quantifies the analytical priority of high-dimensional columns:
$$\text{Interestingness Score} = (1 - \text{Normalized Entropy}) + \text{Missing Fraction} + \text{Association Score} + \text{Pattern Score}$$

1. **Shannon Entropy (Distribution Uniformity vs. Skewness):**
   $$H(X) = -\sum_{i=1}^n P(x_i) \log_2 P(x_i)$$
   $$\text{Normalized Entropy} = \frac{H(X)}{\log_2(n)}$$
2. **Missing Fraction:**
   $$\text{Missing Fraction} = \frac{N_{\text{null}}}{N_{\text{total}}}$$
3. **Association Score:**
   - **Numerical Pairs:** Pearson Correlation Coefficient $r \in [-1, 1]$
     $$r_{xy} = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum(x_i - \bar{x})^2 \sum(y_i - \bar{y})^2}}$$
   - **Categorical Pairs:** Theil's U (Uncertainty Coefficient) measuring asymmetric association:
     $$U(X|Y) = \frac{H(X) - H(X|Y)}{H(X)}$$
   - $\text{Association Score} = \text{Count of dependencies where } |r| > 0.5 \text{ or } U(X|Y) > 0.5$.
4. **Syntactic Pattern Score:**
   $$\text{Pattern Score} = \frac{N_{\text{minority patterns}}}{N_{\text{total unique patterns}}}$$

---

### 1.3 Boundary Quality: Class Overlap & Label Noise Detection
- **Class Overlap Detection (k-NN Graph Pruning):**
  1. Build Euclidean $k$-NN graph ($k=5$).
  2. Prune edges where all $k$ neighbors share the same class label (safe homogeneous zones).
  3. Extract connected components on remaining boundary nodes.
  4. Measure Overlap Score:
     $$\text{Overlap Score} = \frac{N_{\text{overlap}}}{N_{\text{total}}}$$
- **Label Noise Detection (with Overlap Subtraction):**
  1. Compute Out-of-fold class probabilities $P(i, c)$ using 5-Fold Cross-Validation.
  2. Flag candidate noisy rows where an alternative class has higher margin: $P(i, k) - P(i, c) > 0$.
  3. **Crucial Guardrail (Overlap Subtraction):** Remove candidates inside Class Overlap Regions to eliminate false positives.
  4. **k-NN Consensus Validation:** Confirm noisy label only if local spatial majority deviates from current label.

---

## 2. Leandro Nunes de Castro Specialty Probes

### 2.1 Time Series Diagnostics
- **Temporal Decomposition:** $Y_t = T_t + S_t + R_t$ (Additive) or $Y_t = T_t \times S_t \times R_t$ (Multiplicative).
- **Moving Average Smoothing:** $\text{MA}_k(t) = \frac{1}{k}\sum_{i=0}^{k-1} Y_{t-i}$ to isolate low-frequency physical signals from high-frequency stochastic noise.
- **Stationarity & Autocorrelation:** Check lag-1 autocorrelation ($\rho_1$) and variance constancy across temporal rolling windows.

### 2.2 Tabular Shape Analysis
- **Skewness:** $\gamma_1 = \frac{\frac{1}{N}\sum (x_i - \bar{x})^3}{\sigma^3}$
- **Kurtosis:** $\beta_2 = \frac{\frac{1}{N}\sum (x_i - \bar{x})^4}{\sigma^4} - 3$

---

## 3. Six Sigma DMAIC & Quality Engineering Bridge

### 3.1 Process Capability Indices ($C_p, C_{pk}$)
For critical operational parameters with specification limits $[LSL, USL]$:
$$C_p = \frac{USL - LSL}{6\sigma}$$
$$C_{pk} = \min\left(\frac{USL - \mu}{3\sigma}, \frac{\mu - LSL}{3\sigma}\right)$$
- $C_{pk} < 1.0$: Process is incapable; high defect risk.
- $1.0 \le C_{pk} < 1.33$: Marginally capable; requires tight SPC monitoring.
- $C_{pk} \ge 1.33$: Capable and stable (Six Sigma standard).

### 3.2 Measurement System Analysis (MSA) & Sensor Diagnostics
- Compare `Sensor_Health_Index` with measurement variance.
- Differentiate **Measurement Flaw** (high sensor drift, calibration error) from **Process Shift** (genuine physical change confirmed across multiple independent parameters).

---

## 4. Visual Gestalt & Human Interface Rules
- **Color:** Soft neutral slate for baseline; high-saturation coral/amber strictly reserved for anomalies and critical risks.
- **Proximity:** Group related physical metrics in adjacent cards.
- **Closure:** Enclose conflict zones or multi-collinear variables in clear bounding boxes.
