# Sovereign Epistemic EDA — The Cognitive Engine for Industrial Data Understanding

> **"You cannot optimize what you do not understand, and you cannot automate what you have not stabilized."**  
> — *ทำให้ 45 นาทีแรกของการทำ EDA เหลือ 0.83 วินาที — แล้วใช้ expertise ของคุณกับส่วนที่ AI ทำไม่ได้: ตัดสินใจ*

**Sovereign Epistemic EDA** คือ **Cognitive Engine (เครื่องยนต์สร้างสติและความตระหนักรู้)** ที่สร้างกรอบความจริงร่วมกัน (**Shared Cognitive Frame**) ระหว่างมนุษย์กับ AI ช่วยให้นักวิเคราะห์ข้อมูล วิศวกรอุตสาหกรรม และ AI Engineers **เข้าใจโครงสร้างความจริงเชิงประจักษ์ (Empirical Grounding)** ของชุดข้อมูลขนาดใหญ่ (10,000+ แถว) ได้ทันทีผ่านการคุยใน Chat — โดยไม่ต้องเขียนโค้ดเอง ไม่ต้องสุ่มเดา และไม่หลงทางไปกับภาพหลอน (Zero Numerical Hallucination)

---

## 🧭 หัวใจของคำว่า "Epistemic" (ญาณวิทยาแห่งข้อมูล)

คำว่า **Epistemology (ญาณวิทยา)** คือ *ศาสตร์ว่าด้วยการรู้แจ้งในความจริง* — ในยุคที่ AI สามารถสร้างโค้ดและโมเดลได้อย่างรวดเร็ว ปัญหาที่อันตรายที่สุดไม่ใช่ "AI เขียนโค้ดไม่เป็น" แต่คือ **"AI ตาบอดและขาดสติ (Blind Autoregressive AI)"** ที่พร้อมจะสร้างโมเดล Machine Learning หรือระบบ Real-Time Optimizer บนข้อมูลขยะโดยไม่รู้ตัว

```text
┌────────────────────────────────────────────────────────────────────────┐
│                   THE EPISTEMIC REVOLUTION IN AI                       │
├──────────────────────────────────┬─────────────────────────────────────┤
│ ❌ Blind / Autoregressive AI     │ 🧠 Sovereign Epistemic AI (ของเรา)  │
│    (AI ขาดสติ / มโนตัวเลขตามน้ำ) │    (AI มีสติ / ยึดมั่นความจริง 100%)│
├──────────────────────────────────┼─────────────────────────────────────┤
│ • สุ่มตัวอย่างข้อมูลแบบเดาสุ่ม   │ • IBM Greedy Set Cover (100% Pattern)│
│ • มอง Outlier ทุกตัวเหมือนกันหมด │ • แยกแยะ Sensor Flaw vs Process Signal│
│ • ตัวเลขสถิติเสี่ยงหลอน (Hallucination)│ • ตัวเลขทุกตัวมาจาก Python Substrate│
│ • กระโดดไปสร้างโมเดลบนระบบที่ยังไม่นิ่ง│ • Six Sigma DMAIC & Taguchi Cpm Guard│
│ • แสดงความมั่นใจแบบหลอกลวง       │ • Falsifiable Hypotheses & Blind Spots│
└──────────────────────────────────┴─────────────────────────────────────┘
```

---

## ⚡ The Problem: กับดักความตาบอดในการทำ EDA แบบเดิม (The Blindness Trap)

```text
คุณเปิดไฟล์ CSV 10,000 แถว × 50 คอลัมน์
    │
    ├─ ❌ Analysis Paralysis: ไม่รู้จะเริ่มดูคอลัมน์ไหนก่อนใน 50 มิติ
    ├─ ❌ Cognitive Friction: เสียเวลาเขียน pandas + seaborn ซ้ำๆ 45 นาที
    ├─ ❌ Blind Anomaly: เจอ Outlier แต่ไม่รู้ว่า "เซนเซอร์พัง" หรือ "เครื่องจักรวิกฤตจริง"
    ├─ ❌ LLM Hallucination: โยนเข้า ChatGPT ตรงๆ ตัวเลขสถิติมักถูกมโนขึ้นมาเอง
    └─ ❌ Pre-Modeling Danger: รีบกระโดดไปทำ ML/Optimization ทั้งที่สเปก Cpk ยังคุมไม่อยู่
```

**Sovereign Epistemic EDA แก้ปัญหาทั้งหมดนี้ได้ใน 0.83 วินาที**

---

## 🔬 How It Works: สถาปัตยกรรม "Deterministic First, LLM Second"

ระบบแยกการทำงานของสมองกลออกเป็น 2 ชั้นอย่างเด็ดขาด (**Decoupled Two-Tier Cognition**) เพื่อรับประกันความถูกต้องแม่นยำ 100%:

```text
                     [ RAW DATASET (10,000+ Rows) ]
                                   │
                                   ▼
┌────────────────────────────────────────────────────────────────────────┐
│ TIER 1: DETERMINISTIC COMPUTATIONAL SUBSTRATE (Python Engine)          │
│ 🛡️ 100% ZERO NUMERICAL HALLUCINATION GUARANTEE (Pure Vectorized Math)   │
│ • Execution Time: 0.83 วินาที (บนชุดข้อมูล 10,000 แถว)                 │
├────────────────────────────────────────────────────────────────────────┤
│  1. Inverted-Index Greedy Set Cover  ──► บีบอัดเป็น 30 แถว (100% Pattern) │
│  2. Column Interestingness Metric    ──► จัดอันดับคอลัมน์สำคัญ (Entropy/Assoc)│
│  3. Leandro Specialty Probes         ──► ตรวจจับ Moving Average Overlay / Drift│
│  4. Six Sigma DMAIC & Taguchi        ──► คำนวณ Cp/Cpk/Cpm + Flaw vs Signal  │
└──────────────────────────────────┬─────────────────────────────────────┘
                                   │
                                   ▼ (Structured JSON Telemetry: Immutable Ground Truth)
┌────────────────────────────────────────────────────────────────────────┐
│ TIER 2: GENERATIVE EPISTEMIC REASONER (LLM Persona Protocol)          │
│ 🤝 SHARED HUMAN-AI COGNITIVE FRAME (Constrained by SKILL.md v4.1)      │
│ • Grounding Rule: All statements MUST cite specific Telemetry values  │
├────────────────────────────────────────────────────────────────────────┤
│  • Stage 1: Data Topology & Silent Friction Synthesis                 │
│  • Stage 2: Specialty Distribution Shapes & Temporal Dynamics          │
│  • Stage 3: Tukey-Gestalt UX Wireframe & Hero KPI Mapping              │
│  • Stage 4: DMAIC Process Capability & Ishikawa Fishbone Structuring   │
│  • Stage 5: Falsifiable Hypotheses Formulation & The Wu-Wei Question   │
└──────────────────────────────────┬─────────────────────────────────────┘
                                   │
                                   ▼
          💬 Chat Response (ส่งมอบข้อเท็จจริง + สมมติฐานที่นำไปใช้ได้ทันที)
```

---

## 🛡️ Pre-Execution Guard: ทำไมต้องมี EDA ก่อนทำ ML & Real-Time Optimization?

สมมติว่าคุณมีชุดข้อมูลโรงงานปิโตรเคมี [Petrochemical Process Optimization (10,000 แถว)](https://www.kaggle.com/datasets/masoudfazli/petrochemical-process-optimization-and-maintenance/data) และต้องการสร้าง **Real-Time Optimization** หรือทำตาม **Potential Use Cases** บน Kaggle Data Card:

```text
[ Kaggle Data Card: สิ่งที่อยากได้ ] ──► (เป้าหมายเชิงทฤษฎี / Wish List)
                 VS
[ Sovereign Epistemic EDA ]          ──► (ความจริงเชิงประจักษ์ในตาราง 10,000 แถว)
```

### 💥 4 หายนะที่จะเกิดขึ้นจริง หากสั่ง AI สร้างโมเดลโดยข้าม Epistemic EDA:

1. **Use Case 1: Energy Regression Modeling**  
   - *Kaggle บอก:* ทำนาย `Energy_Intensity` จาก `Temp`, `Pressure`, `Flow`
   - *หายนะหากข้าม EDA:* AI จะตกหลุมพราง **Omitted Variable Bias** เพราะไม่รู้ว่าตัวแปรที่คุมพลังงานมากที่สุดคือ **`Product_Yield_Tons` ($r = -0.82$)** และโมเดลจะบิดเบี้ยวจาก **75 Outliers** ที่หลุด 3-Sigma
2. **Use Case 2: Predictive Maintenance & Anomaly Detection**  
   - *Kaggle บอก:* วิเคราะห์ `Vibration`, `Valve_Opening`, `Sensor_Health` ตรวจจับความเสื่อมสภาพ
   - *หายนะหากข้าม EDA:* ในตารางมี **500 แถวที่เซนเซอร์พังอยู่แล้ว (`Sensor_Health < 0.20`)** โมเดล AI จะจดจำว่าความพังนั้นคือ *"สภาวะปกติ (Baseline Contamination)"* และจะไม่เตือนภัยในหน้างานจริง!
3. **Use Case 3: Catalyst Lifetime Optimization**  
   - *Kaggle บอก:* ศึกษา `Catalyst_Age_Days` เพื่อสร้าง Degradation Curve
   - *หายนะหากข้าม EDA:* AI จะสร้างกราฟเฉลี่ย 1 มิติที่หลอกลวง เพราะมองข้าม **Interaction Effect ระหว่าง `Unit_Name × Catalyst_Type`** (ซึ่ง Epistemic Snapshot สกัดไว้ 85 patterns)
4. **Use Case 4: Real-Time Plant Optimization**  
   - *หายนะหากข้าม EDA:* ข้อมูลมี **$C_{pk} = 0.005$ (ยังคุมไม่อยู่ มีของเสีย > 50%)** การนำ AI ไปสั่งการ Real-Time บนระบบที่ไม่เสถียร จะทำให้วาล์วสั่นกระพือ (Hunting) และเร่งเตาจน Catalyst พังพินาศ

---

## 🎯 Concrete Use Cases: ปัญหาหน้างานที่ระบบนี้แก้ได้ทันที

### Use Case 1: "เปิดไฟล์มา 50 คอลัมน์ ไม่รู้จะเริ่มดูตรงไหน"
* **แก้ปัญหา:** Information-Theoretic Ranking คำนวณ Entropy, Missingness, และ Association Hubs ชี้เป้าทันทีใน 0.83 วินาทีว่า `Energy_Intensity` (Score: 2.0) คือจุดศูนย์กลางที่ต้องดูก่อน

### Use Case 2: "เจอค่าผิดปกติ แต่ไม่รู้ว่าเซนเซอร์พังหรือเครื่องจักรมีปัญหาจริง"
* **แก้ปัญหา:** Flaw vs. Signal Audit + Domain Ontology แยกแยะชัดเจนว่า 500 แถวที่มีปัญหาคือ **Sensor Flaw (Gage R&R)** แต่ความดันและอุณหภูมิคือ **Process Signal**

### Use Case 3: "ทำ EDA เสร็จแล้ว แต่ไม่รู้จะเอาไปทำอะไรต่อ"
* **แก้ปัญหา:** ระบบส่งมอบ **3-5 Atomic Facts**, แผนผัง **Ishikawa Fishbone**, **Falsifiable Hypotheses** ที่พร้อมทดสอบ และ **The Wu-Wei Question** บังคับให้เผชิญ trade-offs ก่อนลงมือ

### Use Case 4: "ต้องส่ง 10,000 แถวให้ AI วิเคราะห์ แต่ติด Context Limit"
* **แก้ปัญหา:** IBM Greedy Set Cover บีบ 10,000 แถวเหลือ **30 แถวตัวแทน (0.3%)** โดยรับประกันทางคณิตศาสตร์ว่าเก็บ **100% Pattern Coverage (85/85 unique patterns)** ครบทุก Anomaly

---

## 🚀 Quick Start & CLI Usage

### 1. Prerequisites
```powershell
pip install numpy pandas
```

### 2. Run CLI (Human-Readable Telemetry)
```powershell
python ".agents/skills/epistemic-eda/scripts/substrate_engine.py" "your_data.csv"
```

### 3. Run with Engineering Spec Limits & Domain Ontology Config (v4.1)
```powershell
python ".agents/skills/epistemic-eda/scripts/substrate_engine.py" "your_data.csv" `
  --spec-limits ".agents/skills/epistemic-eda/references/petrochemical_spec_limits.json" `
  --ontology ".agents/skills/epistemic-eda/references/petrochemical_ontology.json"
```

### 4. Run CLI (Machine-Readable JSON for Pipelines)
```powershell
python ".agents/skills/epistemic-eda/scripts/substrate_engine.py" "your_data.csv" --json
```

### 5. Use via Interactive Chat (Antigravity IDE)
เปิดไฟล์ CSV ใน Workspace แล้วพิมพ์ในแชต:
> *"ช่วยวิเคราะห์ไฟล์ @your_data.csv ให้หน่อย ฉันไม่รู้อะไรเกี่ยวกับข้อมูลนี้เลย"*

---

## 📁 Project Structure

```text
.agents/
└── skills/
    └── epistemic-eda/
        ├── SKILL.md                  # Agent Persona + 5-Stage Epistemic Protocol (v4.1)
        ├── scripts/
        │   └── substrate_engine.py   # Deterministic Python Engine (550+ lines)
        │       ├── calculate_entropy()                  # Normalized Shannon Entropy
        │       ├── calculate_theils_u()                  # Theil's U (Asymmetric Categorical Association)
        │       ├── extract_regex_pattern()               # String → Structural Token
        │       ├── generate_greedy_dataset_snapshot()    # IBM Greedy Set Cover + Cross-Column Patterns
        │       ├── analyze_column_interestingness()      # Multi-Metric Scoring & Ranking
        │       ├── analyze_specialty_probes()            # Time-Series, Moving Average Overlay, Tabular Shapes
        │       ├── calculate_six_sigma_dmaic()           # Cp/Cpk/Cpm + Ontology/Heuristic Flaw vs Signal
        │       └── run_full_epistemic_substrate()        # End-to-End Orchestrator (CLI / Programmatic)
        └── references/
            ├── eda_knowledge.md                  # Mathematical Reference (IBM Data-Centric AI + Leandro + DMAIC)
            ├── petrochemical_spec_limits.json    # Sample Engineering Specification Limits
            └── petrochemical_ontology.json       # Sample Domain Semantic Column Ontology
```

---

## 📚 Documentation & Epistemic Deep-Dive Index

สำหรับผู้ที่ต้องการศึกษาเชิงลึกเกี่ยวกับทฤษฎี สถาปัตยกรรมความปลอดภัย และคู่มือผู้ใช้:

1. 🧠 [SOVEREIGN_EPISTEMIC_COGNITIVE_ENGINE.md](file:///c:/Users/rujir/EDA/SOVEREIGN_EPISTEMIC_COGNITIVE_ENGINE.md)  
   *บทวิเคราะห์เชิงปรัชญาญาณวิทยาและวิศวกรรมระบบ: ผ่า 5 หายนะทางวิศวกรรมจากการข้าม EDA และบทบาทของ Cognitive Engine*
2. 🔍 [EPISTEMIC_REASONING_AND_HALLUCINATION_AUDIT.md](file:///c:/Users/rujir/EDA/EPISTEMIC_REASONING_AND_HALLUCINATION_AUDIT.md)  
   *รายงานตรวจสอบความน่าเชื่อถือทางคณิตศาสตร์ ขอบเขต Zero Numerical Hallucination และการวิเคราะห์ช่องโหว่ความเสี่ยงเชิงลึก*
3. 📖 [QUICK_START_USER_GUIDE.md](file:///c:/Users/rujir/EDA/QUICK_START_USER_GUIDE.md)  
   *คู่มือการใช้งานอย่างง่ายฉบับจำลองบทสนทนา (Prompt-Based Simulation) พร้อม Decision Checkpoints และ Prompt Cheat Sheet*

---

## 🧪 Benchmark Results

| Metric | ผลลัพธ์จริง | หมายเหตุ |
|---|---|---|
| **Dataset** | petrochemical_advanced_data (1).csv | 10,000 rows × 16 columns (2.32 MB) |
| **Processing Speed** | **0.83 วินาที** | Python 3.13 / Windows ARM64 |
| **Pattern Coverage** | **100.0% (85/85 Patterns)** | บีบอัด 10,000 $\to$ 30 แถวตัวแทน (0.3%) |
| **Top Ranked Hub** | `Energy_Intensity` (Score: 2.0) | สัมพันธ์ผกผันกับ Yield ($r = -0.82$) |
| **Time-Series Probe** | ✅ ตรวจจับอัตโนมัติ (Period: 4 ชม.) | Moving Average Signal: `Bearish/Bullish Drift` |
| **Six Sigma Capability** | ✅ $C_p, C_{pk}, C_{pm}$ & DPMO | คำนวณเทียบกับ Engineering Spec Limits จริง |
| **External Dependencies**| **NumPy, Pandas เท่านั้น** | Zero heavy ML framework requirement |

---

## 🏛️ Theoretical Foundations & Scientific Attribution

Built on theoretical foundations from:
- **IBM Research** — *"A Data-centric AI Framework for Automating Exploratory Data Analysis"* (2023)
- **Leandro Nunes de Castro** — *"Exploratory Data Analysis"* (2025/2026)
- **John W. Tukey** — *"Exploratory Data Analysis"* (1977)
- **Six Sigma DMAIC & Genichi Taguchi** — Process Capability ($C_p, C_{pk}, C_{pm}$) & Robust Quality Engineering

---

*"Exploratory data analysis can never be the whole story, but nothing else can serve as the foundation stone — as the first step."*  
— **John W. Tukey**
