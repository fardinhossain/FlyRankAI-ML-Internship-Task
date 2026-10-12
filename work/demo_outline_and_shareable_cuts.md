# 🎙️ ML-12: Tell the Story — 5-Minute Technical Showcase & Shareable Cuts

> **Author:** Md. Fardin Hossain (`fardin.hosn@gmail.com`)  
> **Track:** Machine Learning — Applied Search Intelligence  
> **Assignment:** ML-12 (Phase: Submit)  
> **Format:** 5-Minute Presentation Deck & Interview Showcase Plan  
> **Live Deployed Paper:** [https://fardinhossain.github.io/FlyRankAI-ML-Internship-Task/](https://fardinhossain.github.io/FlyRankAI-ML-Internship-Task/)  
> **GitHub Repository:** [https://github.com/fardinhossain/FlyRankAI-ML-Internship-Task](https://github.com/fardinhossain/FlyRankAI-ML-Internship-Task)  

---

## ⏱️ 1. The 5-Minute Technical Showcase Plan

*Tailored for the Week-8 Capstone Showcase, Executive Briefings, and Senior ML Engineering Technical Interviews.*

### 📋 Executive Summary Table

| Timing | Showcase Phase | Speaker Narrative & Script Guidance | Artifact & Visual Evidence |
| :---: | :--- | :--- | :--- |
| **00:00 – 01:00**<br>`Minute 1` | **The Operational Dilemma & Core Question** | • **The Enterprise Dilemma:** High-ranking search articles decay silently over time as competitor coverage expands and algorithms shift.<br>• **The Operational Bottleneck:** Editorial bandwidth is finite—writers can update only 20–50 URLs per weekly sprint across a 30,000+ page library.<br>• **Why Deterministic Rules Fail:** Industry heuristics (e.g., "refresh if older than 90 days") ignore domain authority differences, treat arbitrary rank thresholds rigidly, and waste writer hours on dead zero-demand URLs.<br>• **The Core Research Question:** *Can supervised machine learning prioritize decaying URLs on unseen client domains better than heuristic baseline rules?* | **Abstract & Problem Framing**<br>Paper Section I |
| **01:00 – 02:00**<br>`Minute 2` | **The Data Contract & Honest Validation Design** | • **The Data Contract:** 30,000 mature URLs (≥ 90 days old, non-zero impressions) across 32 client accounts from FlyRank's 78.8M-row search performance warehouse (`v20260703`).<br>• **Leakage Guardrails:** 27 observable signals up to decision time *t* = 0; target derivatives (`trend_pct`) and future metrics strictly excluded.<br>• **Grouped Holdout Design:** Partitioned via `GroupShuffleSplit` on `client_id` with an 80/20 train/test split (23,837 train pages across 25 clients; 6,163 test pages across 7 held-out clients; 0 domain overlap). Zero client overlap guarantees genuine Day-1 onboarding generalizability. | **Table I: Feature Taxonomy**<br>& Grouped Split Audit |
| **02:00 – 03:00**<br>`Minute 3` | **The Core Visual: Cost/Value Decision Matrix** | • **The Visual:** Walk through Figure 1 (`figures/cost_value_matrix.png`).<br>• **Two Dimensions:** Logarithmic 90-day search demand (X-axis) against model-predicted decay probability (Y-axis).<br>• **The Core Insight:** A decaying page with only 5 monthly impressions does not warrant an editorial refresh sprint. The upper-right quadrant (High Demand + High Decay Risk) isolates high-priority candidates.<br>• **Filtering False Negatives:** Demand weighting eliminates trivial 1-impression fluctuations that mathematically register as 100% drops but carry zero business value. | **Figure 1: Decision Matrix**<br>`figures/cost_value_matrix.png` |
| **03:00 – 04:00**<br>`Minute 4` | **Canonical Results & The Validation Split Gap** | • **The Empirical Lift:** Standalone Logistic Regression (0.780 Precision@50) and Random Forest (0.680 Precision@50) more than double the heuristic baseline rule (0.300 P@50) on unseen test clients (+127% to +160% relative lift). Combining decay probability with demand into a composite Action Score reaches **0.980 P@50** (49 out of 50 verified declining URLs accurately targeted).<br>• **The Honest Validation Gap:** Naive random row splitting produced an artificial 1.000 P@50 because the model memorized client baselines. Honest client-grouped evaluation revealed the true 0.680 P@50. Grouped validation is non-negotiable for out-of-domain evaluation. | **Table II & Table III**<br>Model Comparison & Split Gap |
| **04:00 – 05:00**<br>`Minute 5` | **Action Playbook & Human-in-the-Loop Governance** | • **Action Playbook Archetypes:** Model predictions map into 5 evidence-based actions with human-readable reason codes: (1) `refresh_and_review_ctr` (24.7%), (2) `refresh` (27.7%), (3) `refresh_and_review_engagement` (7.0%), (4) `expand_and_refresh` (<0.1%), (5) `monitor` (40.6%).<br>• **Strict Governance Guardrails:** (1) No autonomous publishing without editorial review; (2) No automated 301 redirects to protect domain backlinks; (3) Mandatory expert review on sensitive YMYL topics.<br>• **Economic Value Lift:** An illustrative sprint simulation yields **+$17,000 in net protected value per 50-page sprint** (+226.7% net ROI vs. 0.0% break-even for heuristics). | **Figure 2: Action Mix**<br>& Playbook Guardrails |

---

### 🎙️ Minute-by-Minute Presentation Script & Slide Guidance

#### ⏱️ Minute 01: The Operational Dilemma & The Core Question
- **Slide Focus:** The Problem Statement (FlyRank Enterprise Content Bottleneck)
- **Key Talking Points:**
  - *The Enterprise Challenge:* In enterprise digital publishing, high-performing articles do not stay on Page 1 forever. Content decays silently as competitors publish fresher guides and search algorithms update.
  - *The Operational Constraint:* Editorial bandwidth is strictly finite: teams can realistically revise only 20 to 50 articles per weekly sprint across portfolios of 30,000+ pages.
  - *Why Fixed Heuristics Fail:* Simple rules like "refresh every page older than 90 days" fail on newly onboarded domains: they ignore domain authority, treat arbitrary position cutoffs rigidly, and waste valuable writer hours on dead zero-demand pages.
  - *The Research Question:* Can a supervised machine learning model, trained strictly on observable search telemetry without data leakage, outperform deterministic heuristic rules in prioritizing content refreshes on completely unseen client domains?

#### ⏱️ Minute 02: The Data Contract & Honest Validation Design
- **Slide Focus:** Table I (Feature Taxonomy) & Client-Grouped Holdout Split
- **Key Talking Points:**
  - *The Data Foundation:* Assembled a leak-free analytical dataset of 30,000 mature URLs across 32 client accounts from FlyRank's 78.8-million-row warehouse release (`v20260703`).
  - *Leakage Prevention:* Engineered 27 observable signals available at review time *t* = 0 across traffic momentum, search visibility, content lifecycle, and reader engagement. All target derivatives (including the 30-day trend momentum column) were strictly excluded from features.
  - *Client-Grouped Partitioning:* Partitioned the dataset using an 80/20 `GroupShuffleSplit` grouped strictly on `client_id`: 25 training client accounts (23,837 URLs) and 7 strictly held-out test client domains (6,163 URLs), with zero domain overlap. This guarantees genuine Day-1 onboarding generalizability without domain memorization.

#### ⏱️ Minute 03: The Core Visual — Cost/Value Decision Matrix
- **Slide Focus:** Figure 1 (`figures/cost_value_matrix.png`)
- **Key Talking Points:**
  - *The Decision Landscape:* Figure 1 maps logarithmic 90-day search demand on the horizontal axis against the model's predicted decay probability on the vertical axis.
  - *The Core Insight:* A URL with a 95% decay probability that receives only five monthly impressions is not an editorial priority. Revising it consumes writer budget with zero return.
  - *Operational Action Score:* Multiplying predicted decay risk by logarithmic impression volume and SERP position click-sensitivity isolates the upper-right quadrant. This filters out noisy single-impression drops and surfaces high-ROI refresh opportunities.

#### ⏱️ Minute 04: The Canonical Results & The Validation Split Gap
- **Slide Focus:** Table II (Model Evaluation) & Table III (Split Gap)
- **Key Talking Points:**
  - *Substantial Performance Lift:* On 6,163 pages across 7 unseen client domains, evaluating top-50 precision (the exact 50 URLs an editorial team reviews in a sprint), standalone Logistic Regression reaches 0.780 and Random Forest reaches 0.680, more than doubling the heuristic baseline of 0.300 (+127% to +160% relative lift).
  - *Composite Action Score Precision:* Combining predicted probability with search demand reaches **0.980 Precision@50**—49 out of 50 prioritized URLs are verified declining.
  - *The Honest Validation Split Gap:* Evaluating Random Forest with a naive random row split reports an artificial 1.000 Precision@50 because trees memorize client identities. Under honest grouped validation, performance settles at an honest 0.680. Honest validation is non-negotiable for enterprise deployment.

#### ⏱️ Minute 05: Action Playbook & Human-in-the-Loop Governance
- **Slide Focus:** Figure 2 (Portfolio Action Mix) & Governance Guardrails
- **Key Talking Points:**
  - *Transparent Decision Support:* Output is mapped into five evidence-based action archetypes with transparent reason codes: 24.7% for CTR and title rewrites, 27.7% for factual refresh, 7.0% for engagement restructuring, and 40.6% retained in passive monitoring.
  - *Three Human-in-the-Loop Guardrails:* (1) No autonomous publishing without human editorial oversight; (2) No automated 301 redirects to protect domain backlinks; and (3) Mandatory subject-matter expert review for sensitive topics.
  - *Economic Value Return:* In a standard 50-page weekly sprint simulation, the prioritized queue protects an incremental +$17,000 in net organic traffic value per sprint (+226.7% net ROI) compared to the heuristic baseline.

---

## 🚀 2. Shareable Cut 1: The Social-Post Cut (LinkedIn / X / Technical Community)

> **Can machine learning beat hand-written rules for content refresh triage on 30,000 search pages? 🔍📉**
>
> In enterprise SEO, high-ranking articles decay silently over time. Editorial bandwidth is finite—teams can realistically update only 20 to 50 URLs each week. Most organizations rely on rigid rules like "refresh if older than 90 days," but fixed rules fail on newly onboarded domains because they ignore domain authority, ranking leverage, and actual search demand.
>
> For my **FlyRank AI/ML Capstone**, I engineered and audited an evidence-based content opportunity triage model across 30,000 mature URLs and 32 client accounts from FlyRank's 78.8-million-row search performance warehouse:
>
> 📊 **What the data showed:**
> • Evaluated on completely unseen client domains (zero client overlap), supervised classifiers achieved **0.680–0.780 Precision@50**—delivering a **+127% to +160% relative lift** over deterministic baseline rules (0.300).
> • When predicted decay probabilities were combined with search demand and position leverage in a composite Action Score, top-50 precision reached **0.980** (49 out of 50 verified declining assets accurately caught).
> • Naive random row splits yielded an inflated 1.000 Precision@50 due to client memorization, proving that strict client-grouped validation is non-negotiable.
>
> 🛡️ **The operational principle:** ML should not replace human writers—it powers an intelligent decision-support triage queue with inspectable reason codes, structured action archetypes, and strict governance guardrails (no autonomous publishing without editorial review!).
>
> 📄 Read the camera-ready research paper & interactive reader:  
> https://fardinhossain.github.io/FlyRankAI-ML-Internship-Task/
>
> 💻 Open-source reproducible code & notebooks:  
> https://github.com/fardinhossain/FlyRankAI-ML-Internship-Task
>
> *Built on the FlyRank ML Internship dataset.*

---

## 💼 3. Shareable Cut 2: The 3-Sentence Employer-Facing Summary

> **1. What I built:**  
> I engineered and deployed an evidence-based machine learning ranking system that identifies and prioritizes decaying content candidates for weekly editorial refresh sprints across enterprise client domains.
>
> **2. On what data:**  
> The pipeline was trained and evaluated on 30,000 mature web pages across 32 client accounts from FlyRank's 78.8-million-row search warehouse under strict client-grouped holdout validation with zero domain leakage.
>
> **3. What it showed:**  
> The empirical results showed that supervised models deliver a measured +127% to +160% relative lift in top-50 precision over deterministic baseline rules on completely unseen domains (0.680–0.780 vs. 0.300, reaching 0.980 when combined with search demand), successfully operationalized into an interpretable editorial playbook with transparent reason codes and human-in-the-loop safety guardrails.
