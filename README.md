# Project RAI: ML Moral Judgment & Liability
**Responsible AI, Law, Ethics & Society | Team 4**
*Technion – Israel Institute of Technology*

---

## 📄 Project Overview & Concept
In the modern defense sector, Machine Learning (ML) systems are increasingly deployed to advise on and coordinate kinetic operations. This architecture presents a profound socio-legal dilemma: *Can autonomous systems navigate complex moral judgments while adhering strictly to International Humanitarian Law (IHL)?* 

**Project RAI (Team 4)** is a prototype auditing engine that simulates what happens when an AI assistant is used to advise a human commander on a military strike. The core philosophy of this engine is that **IHL treats legal rules as binding constraints:** 
* The mathematical calculations of philosophical models (Utilitarian and Deontological frameworks) are strictly **advisory**.
* No degree of optimized ethical "preference" or operator history can turn an unlawful strike into a lawful one under IHL.

---

## 🛠️ System Architecture & Specifications

### 1. Multi-Modal Input Data
The dashboard functions as a multi-modal integration layer that accepts:
* **Textual Intelligence:** Raw tactical reports, target value classifications (`low`, `medium`, `high`, `critical`), scenario descriptions, and estimated civilian parameters.
* **Grounded Metrics:** Numerical evaluations of present civilians ($N_{civilians}$) and children ($N_{children}$), alongside expected allied lives saved.

### 2. Core Processing Layers
The integrated engine handles every proposed tactical scenario through four distinct layers:

| Layer Component | Technical Implementation | Operational Role |
| :--- | :--- | :--- |
| **Utilitarian Model** | Trained `distilbert-base-uncased` with a margin-ranking loss function on the **ETHICS dataset**. | **Advisory:** Computes a scalar preferability score optimizing for net lives saved. |
| **Deontological Model** | Trained binary classifier (`distilbert-base-uncased`) evaluating if a justification respects ethical duty. | **Advisory:** Outputs a proxy probability score for structural moral permissibility. |
| **IHL Rule Layer** | Deterministic code converting rule-based legal bindings into programmatic constraints. | **Binding Constraints:** Explicitly checks the core tenets of **Distinction, Proportionality, and Precautions**[cite: 1]. |
| **Alternative Timing Engine** | Grounded deterministic scale model using cellular density profiles[cite: 2] by hour. | **Tactical Mitigation:** Finds alternative times of lower collateral damage to satisfy the Precautions principle[cite: 1]. |

### 3. System Outputs
For every query, the engine dynamically generates an audit statement containing[cite: 2]:
1. **Binary Recommendation:** `STRIKE PERMISSIBLE - proceed to human authorization` or `DO NOT STRIKE (now)`[cite: 1, 2].
2. **Advisory Moral Metrics:** Concrete percentage weights for Utilitarian strike preferences and Deontological duties[cite: 1, 2].
3. **Granular IHL Audit Verdict:** Independent pass/fail tracking for Distinction, Proportionality (where children are weighted $2\times$ heavily[cite: 1]), and Precautions[cite: 1, 2].
4. **LLM Tactical Suggestion:** Natural language alternative prompts written by a local text generator (`google/flan-t5-base`)[cite: 1, 2].
5. **Memory-Recall Logging:** Reviews matching historical operator data (`AGREE` / `OVERRIDE`) to flag human-review priorities[cite: 1, 2].

---

## 📂 Repository Directory Structure
To run and evaluate the system, establish the following structural directory layout inside your root repository:

```text
Project-RAI/
├── README.md
└── audit/
    ├── MoralML_Team4_audit_submission.ipynb
    ├── aegis_scenarios.csv
    └── aegis_traps.csv
