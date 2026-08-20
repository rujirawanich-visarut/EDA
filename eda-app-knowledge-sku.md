# [KNOWLEDGE_SKU v1.0] The Sovereign Epistemic EDA & Data-Centric App Substrate
> **Target Consumer:** Antigravity (App Scaffolding Agent)  
> **Source Material:** IBM Research "A Data-centric AI" (2023) & Leandro Nunes de Castro "Exploratory Data Analysis" (2025/2026)  
> **Purpose:** Technical specification & blueprint for scaffolding the Sovereign EDA Web Application.

---

## PART 1: The Core Methodology & Mathematical Formulations (Knowledge SKUs)

This section maps the exact scientific algorithms and behavioral science guidelines required for the processing engine. Antigravity must implement these as Python processing modules.

### I. IBM Data-Centric AI Algorithms (Data Quality Control Plane)

#### 1. Dataset Snapshot Algorithm (Intelligent Data Sampling)
*   **Objective:** Extract a minimal representative subset ($D_S$) from the full dataset ($D_N$) of $N$ rows and $K$ columns, capturing 100% of unique data patterns ($P(D_N)$) without frequency-based bias.
*   **Pre-processing Pipeline:**
    1.  **Drop Unique Identifiers:** Exclude columns where each row contains a unique string/number (e.g., IDs, SSNs) as they contain no comparative structural information [92].
    2.  **Retain Categorical Attributes:** Retain standard categorical columns as-is.
    3.  **Bin Numerical Attributes:** Convert continuous numerical columns into categorical bins (using quantiles or uniform intervals) and replace continuous values with their respective Bin Index.
    4.  **Extract String Regex Patterns:** Convert unstructured strings (e.g., Dates `dd-mm-yyyy` or `dd/mm/yyyy`, Phone Numbers) into regular expressions and replace raw strings with their regex representation [10, 11, 15].
*   **Mathematical Formulation:**
    *   Let $P(D_N) = \bigcup_{i=1}^K P(C_i)$ be the set of all patterns across columns [12].
    *   Represent the dataset as a Bipartite Graph $G = (P, R, E)$ where $P$ is the set of all patterns, $R$ is the set of all rows, and $E$ is the set of edges representing pattern coverage [12].
    *   This is an NP-Complete Set Cover problem. Solve using a Greedy Approach [13]:
        *   **Row Importance Metric ($I(r_i)$):** 
            $$I(r_i) = \sum_{j=1}^K I(p_{c_{ij}})$$
            Where $I(p)$ is the pattern importance (defined as the inverse relative frequency of the pattern in the column to prioritize rare patterns) [14, 15].
    *   **Greedy Selection Loop:**
        1. In each iteration, compute $I(r_i)$ for all remaining rows.
        2. Select row $r^* = \arg\max_{r_i} I(r_i)$ and add to the snapshot $D_S$ [15, 17].
        3. For all patterns $p$ covered by the selected row $r^*$, set their importance $I(p) = 0$ to avoid redundant coverage in subsequent iterations [15, 17].
        4. Stop when all dataset patterns are covered: $P(D_S) = P(D_N)$ [15, 17].

#### 2. Interesting Columns Detection (Column Ranking Engine)
*   **Objective:** Quantify and rank the analytical value of all columns in high-dimensional datasets ($>100$ columns) by calculating an objective **Interestingness Score** [3, 23]:
    $$\text{Interestingness Score} = (1 - \text{Entropy}) + \text{Missing Fraction} + \text{Association Score} + \text{Pattern Score}$$ [24]
*   **Metrics Deconstruction:**
    *   **Entropy:** Measures the uncertainty or uniformity of the distribution. High entropy represents uniform distribution; low entropy represents a dominant or skewed distribution [24].
        $$\text{Entropy} = -\sum_{i=1}^n P(x_i) \log P(x_i)$$ [24]
    *   **Missing Fraction:** The proportion of null or empty values in the column [24]:
        $$\text{Missing Fraction} = \frac{\text{Number of missing values in column}}{\text{Total number of rows}}$$ [25]
    *   **Association Score:** Measures dependencies with other columns.
        *   Calculate Pearson Correlation Coefficient ($r$) for numerical attribute pairs [25, 87].
        *   Calculate Thiel's U (Uncertainty Coefficient) for categorical attribute pairs [25, 90].
        *   $\text{Association Score} = \text{Count of associations with coefficient } > 0.5$.
    *   **Pattern Score:** Measures syntactic diversity in text/string columns [26]:
        $$\text{Pattern Score} = \frac{\text{Number of minority patterns}}{\text{Total number of unique patterns}}$$ [26]
        *(Include only patterns that occur in $<5\%$ of rows, provided the dominant pattern covers $>50\%$ of rows to avoid noise).*
*   **Output Actions:** Tag columns automatically with metadata labels (e.g., `Low Entropy` [26], `High Correlation` [26], `High Nullity`, `Syntactic Divergence`) to guide human investigation.

#### 3. Class Overlap Detection (Boundary Proximity Resolver)
*   **Objective:** Map and explain vector-space regions where different classes lie in close spatial proximity, causing high classification uncertainty (reduces downstream accuracy by up to 15%) [27, 32].
*   **Graph-Based Algorithm:**
    1.  **Graph Construction:** Represent each data point as a vertex $V$ in a graph $G$. Draw undirected edges $E$ connecting each vertex to its $k$-nearest neighbors (k-NN) based on Euclidean distance [34].
    2.  **Homogeneous Pruning:** Inspect the class labels of each vertex and its neighbors. If a vertex and all its $k$ neighbors share the same class label, **prune all edges connecting them** and remove those nodes (degree 0) from the overlap graph (they are in a safe, non-overlapping region) [34].
    3.  **Connected Component Extraction:** For remaining vertices with degree $> 0$, extract the connected components [34].
    4.  **Imbalance Ratio Pruning:** For each connected component, count the ratio of classes. If the class distribution ratio is highly skewed (less than threshold $r$), prune the component (it represents negligible overlap) [34].
    5.  **Overlap Output:** The remaining connected components are the **Genuine Class Overlap Regions** [34].
*   **Metrics & Explanations:**
    *   **Overlap Score:** $\frac{\text{Number of data points in overlap regions}}{\text{Total number of data points}}$ [34, 35].
    *   **Explanations:** For each overlap region, extract the bounding feature ranges (min/max bounds of columns for points in that region) to explain which features are causing the overlapping conflict [34, 35].

#### 4. Label Noise Detection (Data Cleaning and Purity Engine)
*   **Objective:** Identify mislabeled target variables in the training set with high precision ($0.93$ precision, significantly outperforming standard CleanLab at $0.74$) by filtering out overlap-induced false positives [41, 48].
*   **Multi-Stage Pipeline (Algorithm 2):**
    1.  **Probability Estimation ($P$):** Train a 5-fold cross-validated Random Forest (or similar ensemble) on raw data $D$ and labels $L$ to generate out-of-fold class-wise probability distributions $P$ [43].
    2.  **Confident Joint Matrix ($C$):** Compute the confident joint matrix $C$ by comparing class-wise mean probabilities with sample probabilities to establish thresholds of label certainty [43, 44].
    3.  **Candidate Noise Selection ($SR$):** Flag candidate noisy rows where the probability difference $P(i,k) - P(i,c)$ is positive (meaning an alternative class $k$ is statistically more probable than the current label $c$) [44].
    4.  **Pruning Step 1: Class Overlap Subtraction ($SR = SR - DS$):** Remove candidates that lie inside the Class Overlap Regions ($DS$) identified by the Overlap Detection Algorithm [44]. This prevents flagging difficult-to-classify boundary points as noisy labels, eradicating CleanLab's primary failure mode [41].
    5.  **Pruning Step 2: Nearest-Neighbor Consensus ($SR \cap CheckNeighbors$):** Execute a local neighborhood check. A candidate row is confirmed as noisy *only* if the majority of its immediate spatial neighbors belong to a class different from its current label [44].
    6.  **Clean Label Recommendation:** Assign the recommended cleaned label based on the local neighborhood class consensus [44].
    7.  **Quality Score ($Q$):** Compute overall dataset quality as:
        $$Q = 1 - \frac{|SR|}{N}$$ [44]

---

### II. Leandro Nunes de Castro's Specialty Archetypes & Visualization Science (Perception Plane)

#### 1. Specialty Data Probes (Processing Archetypes)
Standard tabular preprocessing fails on complex relational, unstructured, or temporal modalities. Activate these specialized diagnostic engines based on metadata detection [125]:

*   **Time Series Probe (Section 6.1):**
    *   *Diagnostic targets:* Trend, seasonality, cycles, and stationarity [126].
    *   *Required actions:* Implement additive and multiplicative Seasonal Decomposition (`seasonal_decompose` via `statsmodels.tsa.seasonal`) [129]. Calculate Moving Averages (MA) to isolate smooth trends from high-frequency stochastic noise [126]. Plot boxplots across time slices to visualize temporal variance distribution [128].
*   **Text & Document Probe (Section 6.2):**
    *   *Diagnostic targets:* Lexical diversity, vocabulary size, word co-occurrence matrices, and syntactic structures [210, 215].
    *   *Required actions:* Tokenize, lemmatize, and vectorize text using TF-IDF [138, 210]. Compute textstat metrics (readability, complexity, grade level) [139, 210]. Plot dependency parsing trees using spaCy's `displacy` SVG renderer to map grammatical relationships [132, 218].
*   **Trees & Networks Probe (Section 6.3):**
    *   *Diagnostic targets:* Density, clustering coefficients, and centrality indices [137].
    *   *Required actions:* Construct NetworkX graphs [139]. Calculate network metrics across 4 dimensions: Degree, Closeness, Betweenness, and Eigenvector Centrality [137]. Plot Adjacency Matrix Heatmaps and Node-Link diagrams with circular layouts to reveal community groupings [137].

#### 2. Visual Gestalt & Human Cognition Rules (UX/UI Design Constraints)
Visual representations must respect the brain's preattentive processing limits and Gestalt grouping laws [100, 107]:

*   **Preattentive Processing Rules:**
    *   *Color (Hue/Saturation):* Reserve high-saturation colors (e.g., bright orange/red) strictly for anomalies, critical overlaps, or noisy labels [102, 105]. Use soft, neutral tones (slate, gray) for normal distributions [44].
    *   *Size & Weight:* Scale markers in scatter plots (or line widths in trend lines) to directly represent variable magnitude, uncertainty, or sample density [102, 105].
    *   *Density & Position:* Arrange high-density zones or clusters using spatial grouping to minimize cognitive clutter [103, 105].
*   **Gestalt Grouping Rules:**
    *   **Proximity:** Place related variables, distributions, and their associated data tables in adjacent UI cards [110, 115].
    *   **Similarity:** Ensure elements representing the same data category maintain consistent colors, shapes, or textures across all dashboard charts [111, 115].
    *   **Continuity:** Use smooth line charts and flow-based diagrams (Sankey charts) to represent processes, timelines, and transition states seamlessly [108, 114].
    *   **Closure:** Enclose conflicting or high-risk regions (like overlapping vector spaces) in shaded bounding cards or enclosing shapes to represent them as single, problematic entities [109, 114].

---

## PART 2: Antigravity App Scaffolding Instructions

Antigravity must utilize this blueprint to scaffold the user interface (front-end) and processing engine (back-end).

```
   [ FRONT-END: Streamlit Interactive UI ]
       │ (Visual Gestalt Layout, Theme: Dark Slate/Teal/Coral)
       ▼
   [ MIDDLEWARE: Core Routing & Schema Validation ]
       │
       ├─► Task Selector: Tabular / Time-Series / Text / Network Probes
       │
       ▼
   [ BACK-END PROCESSING ENGINE: Computational Substrate ]
       ├─► Module 1: Dataset Snapshot Engine (NP-Complete Greedy Cover)
       ├─► Module 2: Column Ranking Engine (Entropy & Thiel's U Correlation)
       ├─► Module 3: Class Overlap Graph Engine (k-NN Graph Pruning)
       └─► Module 4: Label Noise Refiner (Confident Joint Matrix + Subtract Overlap)
       │
       ▼
   [ DETERMINISTIC SENSORS / COMPILER GATE ]
       └─► Code Generation & Execution Sandbox
```

### I. App Layout & Navigation Structure
Build a multi-page, highly interactive **Streamlit Dashboard** featuring a dark-slate professional theme with coral accents for warning signals.

#### Page 1: Unified Ingest & Data Topology (Stage 1 & 2)
*   **Data Upload Component:** Drag-and-drop CSV uploader with strict schema checking.
*   **Dataset Snapshot Card (Gestalt Proximity):**
    *   Shows a compact grid of the sampled $D_S$ subset rows.
    *   An explanatory tooltip explains how the greedy graph-cover algorithm compressed the dataset down to ~3% while retaining 100% pattern coverage.
*   **Interesting Columns Ranking (Preattentive Color & Weight):**
    *   A ranked vertical bar chart showing columns by Interestingness Score.
    *   Hovering over a bar reveals tag badges: `[Low Entropy]`, `[High Association]`, `[High Missingness]`.

#### Page 2: Diagnostic & Quality Control Plane (Stage 1 & 3)
*   **Class Overlap Visualization Layout (Gestalt Closure):**
    *   A split-screen layout. Left side: Interactive Plotly 2D/3D Scatter Plot (PCA/t-SNE/UMAP projection) with overlapping regions enclosed in shaded coral hulls [68]. Right side: Bounding Feature Ranges table detailing exactly why those boundaries conflict [34, 35].
*   **Label Noise Refiner & Cleaning Table:**
    *   A data table highlighting rows containing suspected noisy labels, comparing `Original Label` vs. `Recommended Clean Label` alongside a `Purity Confidence Score`.
    *   Includes a master button: `[Commit Cleaned Labels]`. Clicking this executes the nearest-neighbor consensus swap, generating a cleaned CSV.

#### Page 3: Specialized Modality Probes (Stage 2 & 3)
Based on uploaded file metadata, dynamically render one of these tabs:
1.  **[Time Series Tab]:** Renders the 4-panel decomposition graph (Original, Trend, Seasonal, Residual) with slider-controlled moving average overlays [126].
2.  **[Text Exploration Tab]:** Displays a word cloud shaped like a comment balloon (Gestalt Closure) alongside spaCy dependency parsing trees [110, 132].
3.  **[Network Explorer Tab]:** Renders an interactive, force-directed NetworkX node-link diagram colored by community membership (Gestalt Common Fate) [112, 113, 137].

#### Page 4: Operational Bridge & Six Sigma Export (Stage 4 & 5)
*   **DMAIC Process Capability Card:** Generates preliminary Ishikawa (Fishbone) causal branches using highly ranked interesting columns, and displays calculated $C_{p}$ and $C_{pk}$ indices.
*   **Dynamic Hypothesis Generator:** Text output block displaying 3 testable hypotheses in the form: *"If we adjust [Variable X] under [Condition Y], then [Variable Z] will move by [W%] due to Causal Driver [K]"*.
*   **The Wu-Wei Question Console:** Renders the strategic operational trade-off query in a large, elegant blockquote.

### II. Code Scaffold Snippets for Backend Engine
Antigravity must leverage these exact mathematical patterns in the Python backend:

#### 1. Dataset Snapshot Engine
```python
import numpy as np
import pandas as pd

def process_data_snapshot(df, n_bins=10):
    processed = df.copy()
    # 1. Drop unique columns (IDs)
    for col in processed.columns:
        if processed[col].nunique() == len(df):
            processed.drop(columns=[col], inplace=True)
            
    # 2. Bin numerical columns, convert strings to regex, retain categorical
    for col in processed.columns:
        if np.issubdtype(processed[col].dtype, np.number):
            processed[col] = pd.qcut(processed[col], q=n_bins, labels=False, duplicates='drop').astype(str)
        elif processed[col].dtype == object:
            # Simple string regex representation
            processed[col] = processed[col].apply(lambda x: ''.join(['c' if c.isalpha() else 'n' if c.isdigit() else s for s in str(x)]))
    return processed

def greedy_dataset_snapshot(df, processed_df):
    # Map row indexes to set of unique column-pattern tokens
    row_patterns = []
    for idx, row in processed_df.iterrows():
        patterns = {f"{col}::{val}" for col, val in row.items()}
        row_patterns.append((idx, patterns))
        
    all_patterns = set().union(*(p for idx, p in row_patterns))
    selected_rows = []
    covered_patterns = set()
    
    # Precompute pattern frequencies for row importance weighting
    pattern_counts = {}
    for idx, patterns in row_patterns:
        for p in patterns:
            pattern_counts[p] = pattern_counts.get(p, 0) + 1
            
    while len(covered_patterns) < len(all_patterns):
        best_row_idx = -1
        best_score = -1
        for idx, patterns in row_patterns:
            if idx in selected_rows:
                continue
            # Row Importance: Sum of inverse relative frequencies of uncovered patterns
            uncovered = patterns - covered_patterns
            score = sum(1.0 / pattern_counts[p] for p in uncovered)
            if score > best_score:
                best_score = score
                best_row_idx = idx
                
        if best_row_idx == -1:
            break
            
        selected_rows.append(best_row_idx)
        covered_patterns.update(row_patterns[best_row_idx][1])
        
    return df.iloc[selected_rows]
```

#### 2. Label Purity Engine with Overlap Subtraction
```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.neighbors import NearestNeighbors

def detect_label_noise(X, y, overlap_indices):
    # Step 1: Compute Sample Probabilities (5-Fold Out-of-Fold prediction)
    # y must be encoded classes 0..C-1
    # Implement ensemble predictions to yield matrix 'P' of shape (N, Classes)
    pass 
    
    # Step 2: Confident Joint Matrix calculation (CleanLab baseline logic)
    # Step 3: Flag candidate rows (SR) where alternative class has higher probability margin
    candidate_indices = set(flagged_noisy_samples)
    
    # Step 4: Prune overlap region points (Eradicate primary false-positive path)
    cleaned_candidates = candidate_indices - set(overlap_indices)
    
    # Step 5: Neighborhood Consensus Validation
    # Ensure point is flagged as noisy only if local neighbor labels conflict
    knn = NearestNeighbors(n_neighbors=5).fit(X)
    verified_noise = []
    recommended_labels = []
    
    for idx in cleaned_candidates:
        neighbors = knn.kneighbors([X[idx]], return_distance=False)[0]
        neighbor_labels = y[neighbors]
        # Label is noisy if it deviates from neighbor majority
        majority_label = np.argmax(np.bincount(neighbor_labels))
        if y[idx] != majority_label:
            verified_noise.append(idx)
            recommended_labels.append(majority_label)
            
    return verified_noise, recommended_labels
```

### III. System Integration Constraints & Security Guardrails
1.  **Sovereign Shield Execution Constraint:** Action proposals generated by LLM analysis agents must never execute CLI/bash or code commands directly on the host machine. All data cleaning scripts or model generation tasks must execute inside an **isolated sandbox runtime** with predefined API boundaries.
2.  **Deterministic Audit Trail:** Maintain an append-only, log-structured record of all committed label changes, dropped columns, and scaling transformations to provide a robust audit trail for regulatory compliance.
3.  **Dynamic Memory Offloading:** Keep Streamlit session states light. Raw uploaded datasets exceeding 10MB must be parsed in chunks, and high-dimensional matrices should be downsampled using the Dataset Snapshot algorithm prior to computing UMAP/t-SNE coordinates to optimize runtime latency.
