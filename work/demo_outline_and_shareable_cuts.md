# ML-12: Tell the Story — 5-Minute Demo Outline & Shareable Cuts

**Author:** Md. Fardin Hossain (`fardin.hosn@gmail.com`)  
**Track:** Machine Learning — Applied Search Intelligence  
**Assignment:** ML-12 (Phase: Submit)  
**Live Deployed Paper:** [https://fardinhossain.github.io/FlyRankAI-ML-Internship-Task/](https://fardinhossain.github.io/FlyRankAI-ML-Internship-Task/)  
**GitHub Repository:** [https://github.com/fardinhossain/FlyRankAI-ML-Internship-Task](https://github.com/fardinhossain/FlyRankAI-ML-Internship-Task)  

---

## 1. The 5-Minute Demo Outline (Week-8 Showcase & Technical Interview Walkthrough)

| Minute | Showcase Section | Talking Points & Script Guidance | Key Artifact Shown |
| :---: | :--- | :--- | :--- |
| **Minute 1** | **The Question & The FlyRank Dilemma** | • **The Enterprise Dilemma:** Mature articles on enterprise websites decay silently, bleeding traffic when competitor coverage emerges or algorithms shift.<br>• **The Operational Bottleneck:** Editorial capacity is strictly capped (e.g., writers can revise only 20–50 URLs/week out of a 30,000+ page library across 32 client accounts).<br>• **Why Heuristics Fail:** Simple rules (e.g., "age > 90 days") ignore domain authority differences, treat arbitrary rank thresholds rigidly, and prioritize dead zero-demand pages.<br>• **The Research Question:** *Can supervised machine learning prioritize decaying URLs on unseen client domains better than heuristic rules?* | Abstract & Problem Statement |
| **Minute 2** | **The Method & Honest Validation Design** | • **The Data Contract:** 30,000 mature URLs ($\ge 90$ days old, non-zero impressions) across 32 client accounts from FlyRank's 78.8M-row search performance warehouse (`v20260703`).<br>• **Leakage Guardrails:** 27 observable signals up to decision time $t=0$; target derivatives ($\text{trend\_pct}$) strictly excluded.<br>• **Validation Design:** Strict client-grouped holdout partition (`GroupShuffleSplit` on `client_id`, 80/20 train/test: 23,837 train pages across 25 clients; 6,163 test pages across 7 clients; 0 domain overlap). Zero client overlap guarantees genuine Day-1 onboarding generalizability. | Table I (Feature Taxonomy) & Grouped Split Audit |
| **Minute 3** | **One Chart: Cost/Value Decision Matrix** | • **The Visual:** Walk through Figure 1 (`figures/cost_value_matrix.png`).<br>• **Axes:** Logarithmic 90-day search demand ($X$-axis) against model-predicted decay probability ($Y$-axis).<br>• **The Insight:** A decaying page with 5 monthly impressions is not an editorial priority. The upper-right quadrant (High Demand + High Decay Risk) isolates high-ROI refresh candidates.<br>• **Filtering False Negatives:** Demand weighting eliminates trivial 1-impression drops that mathematically look like 100% decline but carry zero editorial value. | `figures/cost_value_matrix.png` |
| **Minute 4** | **One Honest Result & The Validation Split Gap** | • **The Empirical Lift:** Logistic Regression (0.780 Precision@50) and Random Forest (0.680 Precision@50) more than double the heuristic baseline rule (0.300 P@50) on unseen test clients (+127% to +160% relative lift). Combining decay probability with demand into a composite Action Score reaches **0.980 P@50** (49/50 true declining pages caught).<br>• **The Honest Validation Gap:** Standard naive random splitting produced an artificial 1.000 P@50 because the model memorized client baselines. Honest client-grouped evaluation revealed the true 0.680 P@50. Grouped validation is non-negotiable for out-of-domain evaluation. | Table II (Canonical Results) & Split Gap Contrast |
| **Minute 5** | **One Recommendation & Action Playbook Guardrails** | • **Action Playbook Archetypes:** Output is mapped into 5 evidence-based actions with human-readable reason codes: (1) `refresh_and_review_ctr` (24.7%), (2) `refresh` (27.7%), (3) `refresh_and_review_engagement` (7.0%), (4) `expand_and_refresh` (<0.1%), (5) `monitor` (40.6%).<br>• **Strict Governance Guardrails:** (1) No autonomous publishing without editorial review; (2) No automated 301 redirects to protect domain backlinks; (3) Mandatory expert review on sensitive YMYL topics.<br>• **Retraining Triggers:** Retrain after Google core algorithm updates, when writer agreement drops below 60%, or every 90 days. | `figures/action_mix.png` & Editorial Playbook |

---

## 2. Shareable Cut 1: The Social-Post Cut (LinkedIn / X / Technical Community)

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

## 3. Shareable Cut 2: The 3-Sentence Employer-Facing Summary

> **1. What I built:**  
> I engineered and deployed an evidence-based machine learning ranking system that identifies and prioritizes decaying content candidates for weekly editorial refresh sprints across enterprise client domains.
>
> **2. On what data:**  
> The pipeline was trained and evaluated on 30,000 mature web pages across 32 client accounts from FlyRank's 78.8-million-row search warehouse under strict client-grouped holdout validation with zero domain leakage.
>
> **3. What it showed:**  
> The empirical results showed that supervised models deliver a measured +127% to +160% relative lift in top-50 precision over deterministic baseline rules on completely unseen domains (0.680–0.780 vs. 0.300, reaching 0.980 when combined with search demand), successfully operationalized into an interpretable editorial playbook with transparent reason codes and human-in-the-loop safety guardrails.
