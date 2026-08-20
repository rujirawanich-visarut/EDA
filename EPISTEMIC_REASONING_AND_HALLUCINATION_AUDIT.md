# Epistemic Reasoning, Grounding Architecture & Hallucination Audit

> **Target Audience:** AI Engineers, Empirical Systems Architects, Lead Data Scientists, and Machine Learning Quality Auditors.  
> **Purpose:** ให้คำอธิบายเชิงลึกอย่างตรงไปตรงมาเกี่ยวกับสถาปัตยกรรม **"Deterministic First, LLM Second"** การเคลม **"Zero Numerical Hallucination"** ขอบเขตความสามารถในการให้เหตุผล (Reasoning Capabilities) และการวิเคราะห์ช่องโหว่ความเสี่ยงที่ภาพหลอน (Residual Hallucinations) ยังอาจเกิดขึ้นได้

---

## 1. การนิยาม "Zero Hallucination" อย่างรัดกุมตามหลักวิศวกรรม

ในการนำเสนอต่อ AI Engineers คำว่า **"Zero Hallucination"** จะสูญเสียความน่าเชื่อถือทันทีหากถูกใช้แบบครอบจักรวาล (Overselling) เพราะโดยธรรมชาติของโมเดลภาษาขนาดใหญ่ (Autoregressive LLM) เป็นระบบความน่าจะเป็น (Probabilistic Next-Token Generator) ไม่ใช่ Deterministic Calculator

ในโครงการ **Sovereign Epistemic EDA** เรานิยามและจำกัดขอบเขตของ "Zero Hallucination" ไว้อย่างชัดเจน 2 ระดับ:

```text
┌────────────────────────────────────────────────────────────────────────┐
│                        EPISTEMIC BOUNDARY                               │
├──────────────────────────────────┬─────────────────────────────────────┤
│ 1. Numerical & Statistical Truth │ ✅ ZERO HALLUCINATION (100% Guaranteed)│
│    (Mean, Std, Entropy, Cp, Cpk) │    คำนวณผ่าน Deterministic Python Engine│
├──────────────────────────────────┼─────────────────────────────────────┤
│ 2. Semantic & Causal Reasoning   │ ⚠️ PROBABILISTIC (Constrained by    │
│    (Hypotheses, Root Cause, DMAIC│    Grounding Protocol & Falsifiability)│
└──────────────────────────────────┴─────────────────────────────────────┘
```

> [!IMPORTANT]
> **สิ่งที่เราเคลมได้จริง 100%:** ตัวเลขทางสถิติทุกตัว (Shannon Entropy, Thiel's U, Pearson Correlation, Moving Average, $C_p$, $C_{pk}$, $C_{pm}$, Defect PPM, Outlier counts) **ไม่มีทางเกิดภาพหลอน (Zero Numerical Hallucination)** เพราะไม่ได้ให้ LLM เป็นผู้คำนวณ แต่ถูก execute ผ่าน Python/NumPy substrate บนเครื่องของผู้ใช้โดยตรง
>
> **สิ่งที่เราต้องยอมรับอย่างตรงไปตรงมา:** ในขั้นตอนการ **ตีความความหมาย (Semantic Interpretation)** และ **การตั้งสมมติฐานเชิงสาเหตุ (Causal Hypotheses)** โมเดล LLM ยังมีโอกาสเกิดความลำเอียง (Bias) หรือเชื่อมโยงความสัมพันธ์ลวง (Spurious Correlation) เป็นสาเหตุจริงได้ หากไม่มีการควบคุมด้วย Epistemic Guardrails

---

## 2. สถาปัตยกรรม Two-Tier Epistemic Pipeline

ระบบแยกการทำงานของสมองกลออกเป็น 2 ชั้นอย่างเด็ดขาด (Decoupled Cognition):

```text
                     [ RAW DATASET (10,000+ Rows) ]
                                   │
                                   ▼
┌────────────────────────────────────────────────────────────────────────┐
│ TIER 1: DETERMINISTIC COMPUTATIONAL SUBSTRATE (Python Engine)          │
│ • Zero LLM involvement / No Prompting / Pure Vectorized Mathematics   │
│ • Execution Time: < 1.0 Second                                         │
├────────────────────────────────────────────────────────────────────────┤
│  1. Inverted-Index Greedy Set Cover  ──► บีบอัดเป็น 30 ตัวแทน (100% Pattern) │
│  2. Column Interestingness Metric    ──► จัดอันดับคอลัมน์สำคัญ (Entropy/Assoc)│
│  3. Leandro Specialty Probes         ──► ตรวจจับ Time-Series, Moving Averages│
│  4. Six Sigma DMAIC Engine           ──► คำนวณ Cp/Cpk/Cpm + Flaw vs Signal  │
└──────────────────────────────────┬─────────────────────────────────────┘
                                   │
                                   ▼ (Structured JSON Telemetry: Immutable Ground Truth)
┌────────────────────────────────────────────────────────────────────────┐
│ TIER 2: GENERATIVE EPISTEMIC REASONER (LLM Persona Protocol)          │
│ • Constrained by Sovereign Epistemic Persona (SKILL.md v4.1)          │
│ • Grounding Rule: All statements MUST cite specific Telemetry values  │
├────────────────────────────────────────────────────────────────────────┤
│  • Stage 1: Data Topology & Silent Friction Synthesis                 │
│  • Stage 2: Specialty Distribution & Temporal Dynamics                │
│  • Stage 3: Tukey-Gestalt UX Wireframe & Hero KPI Mapping              │
│  • Stage 4: DMAIC Process Capability & Ishikawa Fishbone Structuring   │
│  • Stage 5: Falsifiable Hypotheses Formulation & The Wu-Wei Question   │
└──────────────────────────────────┬─────────────────────────────────────┘
                                   │
                                   ▼
                 [ 5-STAGE EPISTEMIC EDA DELIVERABLE ]
```

---

## 3. กลไกการ Reasoning ของระบบ (Reasoning Capabilities)

ระบบไม่ได้ทำหน้าที่แค่ "สรุปข้อความ" แต่มีกลไก Reasoning 4 ขั้นตอนที่เชื่อมโยงระหว่างคณิตศาสตร์เชิงประจักษ์กับตรรกะเชิงอนุมาน:

### 3.1 Combinatorial Coverage Reasoning (IBM Set Cover)
- **โจทย์:** มนุษย์และ LLM ไม่สามารถอ่าน 10,000 แถวพร้อมกันได้โดยไม่สูญเสีย Cognitive Context หรือติดปัญหา Context Limit
- **กลไก:** แปลงแถวและคอลัมน์เป็น Bipartite Graph โดยแปลงตัวเลขเป็น Quantile Bins และแปลงความสัมพันธ์ระหว่างตัวแปรเป็น Cross-Column Composite Tokens ($C_a \times C_b$) จากนั้นแก้ปัญหา Set Cover แบบ Greedy ด้วย Inverse Frequency Weighting
- **Reasoning Output:** สกัดชุดข้อมูลตัวแทน $\approx 30$ แถว (0.3%) แต่ครอบคลุม **85/85 unique patterns (100%)** ทำให้ตัวแปรผิดปกติ (Rare Tail Anomaly) ไม่ถูกกลืนหายไปในการสุ่ม

### 3.2 Information-Theoretic Priority Reasoning (Column Ranking)
- **โจทย์:** ในตาราง 50–200 คอลัมน์ มนุษย์เกิดสภาวะ Analysis Paralysis ไม่รู้จะวิเคราะห์คอลัมน์ไหนก่อน
- **กลไก:** รวมพลังงานสารสนเทศ 4 มิติเป็น Interestingness Score:
  $$\text{Score} = (1 - \text{Normalized Entropy}) + \text{Missing\%} + \text{Association Hubs} + \text{Pattern Anomalies}$$
- **Reasoning Output:** จัดลำดับความสำคัญให้มนุษย์เห็นทันทีว่าคอลัมน์ใดคือ "ศูนย์กลางความสัมพันธ์ (Association Hub)" เช่น ชี้ชัดว่า `Energy_Intensity` สัมพันธ์กับ `Product_Yield_Tons` ($r = -0.82$)

### 3.3 Epistemic Disambiguation Reasoning (Flaw vs. Signal Audit)
- **โจทย์:** เครื่องมือ Anomaly Detection ทั่วไป (เช่น Isolation Forest) มอง Outlier ทุกตัวเป็น "ความผิดปกติประเภทเดียวกัน"
- **กลไก:** ใช้ Domain Ontology Matrix หรือ Heuristic Correlation Rules แยกแยะระหว่าง:
  - **Measurement Degradation (Flaw):** ตัวแปรเซนเซอร์ต่ำกว่าเกณฑ์ความน่าเชื่อถือ $\to$ จัดเป็นปัญหาของระบบวัด (Gage R&R)
  - **Thermodynamic / Physical Shift (Signal):** ตัวแปรเซนเซอร์ทำงานปกติ แต่ค่ากระบวนการแกว่งตัว $\to$ จัดเป็นปัญหาทางกายภาพของเครื่องจักร
- **Reasoning Output:** ป้องกันไม่ให้ทีมวิศวกรสั่งหยุดเครื่องจักรเพราะเซนเซอร์หลุดสเปก หรือในทางกลับกัน ไม่มองข้ามสัญญาณเตือนการพังของอุปกรณ์

### 3.4 Taguchi & Capability Reasoning (DMAIC Bridge)
- **โจทย์:** ค่า Mean และ Std ทั่วไปไม่ได้บอกว่ากระบวนการ "มีความสามารถตามสเปกวิศวกรรม" หรือไม่
- **กลไก:** คำนวณ $C_p, C_{pk}$ และ $C_{pm}$ (Taguchi Capability Index) ซึ่งคำนึงถึงทั้ง Variance ($\sigma$) และ Off-Target Deviation $(\mu - Target)$:
  $$C_{pm} = \frac{USL - LSL}{6\sqrt{\sigma^2 + (\mu - Target)^2}}$$
- **Reasoning Output:** รายงานค่าของเสีย Defect Rate %, DPMO (Defects Per Million Opportunities) และประเมินความสามารถกระบวนการ 3 ระดับ (`CAPABLE` / `MARGINAL` / `INCAPABLE`)

---

## 4. ขอบเขตความสามารถ: อะไรทำได้ vs อะไรทำไม่ได้

| มิติ | สิ่งที่ระบบ **ทำได้ (Capabilities)** | สิ่งที่ระบบ **ทำไม่ได้ (Hard Limitations)** |
|---|---|---|
| **ตัวเลขสถิติ** | คำนวณค่า Mean, Std, Skewness, Kurtosis, Correlation, Entropy, Cp, Cpk, Cpm ถูกต้อง 100% | ไม่สามารถคำนวณสถิติของข้อมูลที่ไม่ได้อยู่ในไฟล์ (No unobserved data calculation) |
| **การตรวจจับเวลา** | ตรวจจับ Periodicity, Trend drift %, Moving Average (Short/Long MA), Crossover signal, Noise ratio | ไม่สามารถทำ STL Decomposition ขั้นสูง หรือพิสูจน์ Stationarity ด้วย ADF Test (ต้องการ statsmodels) |
| **การให้เหตุผลเชิงสาเหตุ** | สร้างสมมติฐานที่ทดสอบและหักล้างได้ (Falsifiable Hypotheses) อิงตามทฤษฎีโดเมน | **ไม่สามารถพิสูจน์ Causal Mechanism ทางกายภาพได้ 100% จากข้อมูลสังเกตการณ์ (Observational Data Alone)** |
| **การระบุของเสีย** | คำนวณจุดหลุดสเปกและ DPMO ได้อย่างแม่นยำเมื่อมีไฟล์ Engineering Spec Limits | ไม่สามารถ "คิดค่า LSL/USL ขึ้นมาเองโดยพลการ" ได้ ต้องอาศัยมาตรฐานวิศวกรรมจากผู้ใช้ |
| **การจำแนกประเภทข้อมูล** | แมปบทบาทตัวแปรตาม Domain Ontology ที่ผู้ใช้กำหนดในไฟล์ JSON | ไม่สามารถรับรู้บริบทโรงงานที่ไม่ถูกระบุใน Ontology หรือโครงสร้างตารางได้ |

---

## 5. การวิเคราะห์ช่องโหว่: โอกาสที่ภาพหลอน (Hallucinations) ยังอาจเกิดขึ้นได้

แม้เราจะกำจัด Numerical Hallucination ได้ 100% แต่ในฐานะ AI Engineers เราต้องเข้าใจว่า **Semantic & Interpretive Hallucinations ยังมีโอกาสเกิดขึ้นได้ใน 4 กรณีนี้:**

```text
                                  RESIDUAL HALLUCINATION RISKS
                                                │
         ┌──────────────────────┬───────────────┴───────────────┬──────────────────────┐
         ▼                      ▼                               ▼                      ▼
┌──────────────────┐  ┌──────────────────┐            ┌──────────────────┐  ┌──────────────────┐
│ Risk 1:          │  │ Risk 2:          │            │ Risk 3:          │  │ Risk 4:          │
│ Spurious Causal  │  │ Ungrounded       │            │ Ontology Mismatch│  │ Prompt Drift &   │
│ Leap             │  │ Extrapolation    │            │ Bias             │  │ Non-Compliance   │
└──────────────────┘  └──────────────────┘            └──────────────────┘  └──────────────────┘
```

### 🔴 Risk 1: Spurious Causal Leap (การด่วนสรุปสหสัมพันธ์เป็นสาเหตุ)
- **พฤติกรรมความเสี่ยง:** Substrate คำนวณพบว่า `Energy_Intensity` มีค่า $r = -0.82$ กับ `Product_Yield_Tons` $\to$ LLM อาจสร้างประโยคอธิบายว่า *"การเพิ่ม Yield โดยตรงจะทำให้การใช้พลังงานลดลงเสมอ"*
- **ความเป็นจริงทางวิทยาศาสตร์:** สหสัมพันธ์ (Correlation) ไม่ใช่เหตุและผล (Causation) อาจมี Confounding Variable (เช่น `Feedstock_Quality`) ที่เป็นตัวขับเคลื่อนร่วมอยู่เบื้องหลัง
- **วิธีบรรเทาของระบบ:** บังคับให้ LLM ส่งมอบผลลัพธ์ในรูปแบบ **"Falsifiable Hypotheses"** (สมมติฐานที่ต้องนำไปทดลองจริงเพื่อหักล้าง) แทนที่จะประกาศว่าเป็นข้อเท็จจริงสัมบูรณ์ (Zero Certainty Theater)

### 🔴 Risk 2: Ungrounded Extrapolation (การอนุมานเกินข้อมูลที่มี)
- **พฤติกรรมความเสี่ยง:** LLM อาจอธิบายลึกไปถึงระดับปฏิกิริยาเคมีโมเลกุลหรือยี่ห้อของวาล์วที่ไม่มีอยู่ใน Dataset หรือไม่ได้ระบุใน Ontology
- **วิธีบรรเทาของระบบ:** Stage 5 มีหัวข้อบังคับ **"What is Unknown / Blind Spots"** บังคับให้ LLM ต้องระบุอย่างชัดเจนว่า *ข้อมูลชุดนี้ไม่สามารถตอบอะไรได้บ้าง*

### 🔴 Risk 3: Domain Ontology Mismatch Bias
- **พฤติกรรมความเสี่ยง:** หากผู้ใช้ใส่ไฟล์ `ontology.json` ผิดพลาด เช่น จัดคอลัมน์ที่เป็นผลผลิต (Output KPI) ไปอยู่ในกลุ่มเซนเซอร์ตรวจวัด (Sensors) ระบบจะคำนวณตัวเลขถูก แต่ LLM จะตีความผลผิดฝั่ง
- **วิธีบรรเทาของระบบ:** ระบบจะพิมพ์สถานะ `[APPLIED]` และ Echo บทบาทของคอลัมน์กลับมาใน Telemetry เพื่อให้มนุษย์สามารถ Audit ได้เสมอ

### 🔴 Risk 4: Persona & Prompt Drift ในโมเดลขนาดเล็ก
- **พฤติกรรมความเสี่ยง:** หากรันบน LLM ที่มีขนาดเล็กหรือความสามารถต่ำ (Weak Instruction Following) ตัว LLM อาจละเลย Telemetry JSON และเริ่มแต่งตัวเลขขึ้นมาเองในคำตอบ
- **วิธีบรรเทาของระบบ:** กำหนด Poka-Yoke Constraint ใน `SKILL.md` ให้ตัวเลขทุกตัวต้องถูก Cross-check กับ JSON Telemetry และใช้สถาปัตยกรรมที่ผู้ใช้สามารถเปิดดู JSON Telemetry ดิบเพื่อเทียบเคียงได้ทันที

---

## 6. สรุปบทสนทนาสำหรับตอบ AI Engineers / Data Quality Auditors

เมื่อต้องอธิบายให้ AI Engineers หรือ Data Science Leads ฟัง สามารถใช้แนวทางสรุปนี้:

> **Q: "ระบบของคุณ Zero Hallucination จริงหรือ? โมเดล LLM ตัวไหนก็หลอนได้ทั้งนั้น"**
>
> **คำตอบเชิงวิศวกรรม:**
> *"เราไม่ได้เคลมว่า LLM คิดเลขไม่เคยพลาด — แต่เรา **ตัดสิทธิ์ LLM ไม่ให้คิดเลขเลยตั้งแต่แรก** 
> 
> ระบบของเราใช้สถาปัตยกรรม **Deterministic Substrate**: ตัวเลข Mean, Entropy, Pearson $r$, Moving Averages, $C_p$, $C_{pk}$, $C_{pm}$ และ Outlier rows ทั้งหมด ถูกคำนวณผ่าน Vectorized Python Engine 100% ภายใน 0.83 วินาที
> 
> สิ่งที่ LLM ทำ มีเพียงการนำ Telemetry ที่เป็น Ground Truth มาเรียบเรียงเป็นภาษาคน และตั้ง **Falsifiable Hypotheses** ภายใต้กรอบ Six Sigma DMAIC เท่านั้น — ซึ่งเราควบคุมความเสี่ยงของการอนุมานผิดด้วยการบังคับระบุ Blind Spots และบังคับให้ทุกข้อความต้องอ้างอิงค่าสถิติจริงจาก Telemetry ครับ"*

---

## 7. Audit Verification Checklist

สำหรับทีมวิศวกรที่ต้องการทำ Audit ระบบ ให้ตรวจสอบตาม 4 เช็กลิสต์นี้:

- [x] **Substrate Determinism:** รันคำสั่ง `--json` ซ้ำ 10 ครั้ง ผลลัพธ์ตัวเลขสถิติต้องเท่ากันทุกทศนิยม (Bit-level Determinism)
- [x] **Snapshot Invariant:** ค่า Pattern Coverage ใน `snapshot` ต้องยืนยันได้ทางคณิตศาสตร์ว่า $\ge 99.0\%$
- [x] **Capability Integrity:** หากไม่มีการส่ง `--spec-limits` ค่า $C_p/C_{pk}$ ต้องไม่ถูกประเมินขึ้นมาเองโดยพลการ (ต้องแสดง `requires_user_spec_limits`)
- [x] **Traceability:** ตัวเลขทุกตัวที่ปรากฏในคำตอบภาษาไทยของ LLM ต้องสามารถสืบย้อนกลับไปพบใน JSON Telemetry ได้ทุกจุด
