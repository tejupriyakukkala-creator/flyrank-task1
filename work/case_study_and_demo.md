# FlyRank Content Refresh: Case Study, 5-Minute Demo Outline & Shareable Summaries

This document contains the official case-study framing, 5-minute technical demo outline, and two public-safe shareable summaries for the FlyRank SEO Capstone Project.

---

## 1. FlyRank Case-Study Framing

### Problem Statement
Enterprise digital search portfolios managed by **[FlyRank](https://flyrank.ai)** experience continuous organic search traffic decay over time. Changes in search engine ranking algorithms, shifting user search intent, competitive content releases, and content staleness degrade page-level impressions and click-through rates (CTR). For enterprise portfolios spanning tens of thousands of URLs across dozens of client domains, identifying which specific pages warrant costly editorial remediation (rewriting content vs updating facts vs pruning dead pages) is a multi-million-dollar operational challenge.

### The Heuristic Rule Failure
Traditional content auditing relies on static heuristic rules, such as flagging any URL where CTR decays by more than 20% relative to historical peaks. In practice, these heuristic rules trigger massive false-positive volumes, flooding content teams with thousands of low-value alerts while failing to generalize across distinct domain verticals (e.g., news/trending sites vs evergreen enterprise documentation).

### Machine Learning Solution
To address this challenge, we developed a zero-leakage, Client-Grouped Machine Learning Prioritization Pipeline (`HistGradientBoostingClassifier`). The system analyzes past-window search performance metrics—including CTR decay ratios, SERP position drift, impression contraction, and content staleness—to accurately rank URLs by decline risk and assign them into actionable operational queues (`rewrite`, `refresh`, `delete`, `monitor`).

### Empirical Impact & Public Safety
- **Evaluated Data:** 30,000 URLs across 32 anonymized enterprise client domains (provided by [FlyRank](https://flyrank.ai)).
- **Validation Design:** Client-Grouped Holdout Split (26 train client domains, 6 held-out test client domains, $n=2,325$).
- **Performance:** Achieved **95.0% Precision@20** and **90.0% Precision@50** (ROC-AUC 0.7698), delivering a **+59.4% relative precision lift** over the baseline heuristic rule (59.6% Precision@20).
- **Public Safety:** 100% public-safe implementation with fully anonymized client identifiers (`client_id`), no private PII, and no confidential search query strings.

---

## 2. 5-Minute Live Technical Demo Outline

| Time Slot | Section | Presentation Content & Live Artifact Focus | Key Speaker Script / Takeaway |
| :--- | :--- | :--- | :--- |
| **0:00 - 1:00** | **Problem & Business Context** | • Show FlyRank dataset context ($n=30,000$ pages, 32 clients).<br>• Highlight the 54.21% base decline rate and editorial cost tension. | *"Static rules flood editorial teams with false alarms. We built a machine learning prioritization engine that ranks high-decline URLs across unseen enterprise client domains."* |
| **1:00 - 2:00** | **Leakage Audit & Validation Design** | • Display `w06_validation_audit.ipynb`.<br>• Show leakage test: `trend_pct` gives artificial 1.0000 ROC-AUC.<br>• Explain Client-Grouped Holdout Split (26 train / 6 test). | *"Including future-window trends like `trend_pct` creates fake 1.0000 scores. We purged all future metrics and enforced a grouped client split to guarantee real-world generalization."* |
| **2:00 - 3:00** | **Baseline vs ML Performance** | • Show Benchmark Table & `figures/precision_at_k_comparison.png`.<br>• Compare Heuristic Rule (59.6% P@20) vs HistGradientBoosting (**95.0% P@20**). | *"On held-out test clients, our model achieves 95.0% Precision at rank 20—a +59.4% relative precision improvement over the heuristic rule, maximizing editorial ROI."* |
| **3:00 - 4:00** | **Action Playbook & Reason Codes** | • Display Action Queue distribution ($4,772$ rewrite, $2,301$ refresh, $1,029$ delete, $21,898$ monitor).<br>• Explain feature importance & reason codes (`RC_CTR_DECAY`, `RC_POSITION_SLIP`). | *"Instead of raw probabilities, we output 4 discrete action queues with human-understandable reason codes so content strategists know exactly why a page was flagged."* |
| **4:00 - 5:00** | **Operational Limits & Retraining SLAs** | • Present the explicit "No-Go" list (legal/brand pages).<br>• Highlight 14-day rewrite SLA and quarterly retraining triggers. | *"We enforce explicit guardrails: low-impression pages and brand landing pages are excluded from automated actions. Models retrain quarterly or on domain drift."* |

---

## 3. Two Public-Safe Shareable Cuts

### Cut 1: Technical & Social Post (LinkedIn / X / Engineering Blog Format)
> **Beating Static Heuristics: Zero-Leakage ML for Enterprise SEO Traffic Remediation**
> 
> How do you prioritize content refreshes across a 30,000-page enterprise portfolio without wasting editorial budget on false positives? Static rules like "flag if CTR drops 20%" fail because they don't scale across different client domain verticals.
> 
> Working with dataset assets from [FlyRank](https://flyrank.ai), I built a gradient-boosted decision tree pipeline evaluated under a strict **Client-Grouped Holdout Split** (26 training client domains, 6 held-out test domains). 
> 
> **Key Findings:**
> 1. **Leakage Audit Warning:** Including future-window metrics like `trend_pct` inflates ROC-AUC to a misleading 1.0000. Purging future metrics is mandatory for honest evaluation.
> 2. **Precision Lift:** Under zero-leakage conditions, our primary model achieved **95.0% Precision@20** and **90.0% Precision@50** (ROC-AUC 0.7698)—outperforming the static heuristic rule (59.6% Precision@20) by **+59.4% relative precision lift**.
> 3. **Action Playbook Allocation:** Ranked 30,000 pages into 4 auditable action queues: 4,772 rewrites (15.9%), 2,301 refreshes (7.7%), 1,029 deletions (3.4%), and 21,898 monitor actions (73.0%), each paired with human-readable reason codes (e.g., `RC_CTR_DECAY`, `RC_POSITION_SLIP`).
> 
> 🔗 Live Paper: https://tejupriyakukkala-creator.github.io/flyrank-task1/
> 🔗 GitHub Repo: https://github.com/tejupriyakukkala-creator/flyrank-task1

---

### Cut 2: Executive / Recruiter 3-Sentencer (Portfolio & Resume Highlight)
> 1. **What I Built:** Developed an end-to-end machine learning prioritization system that detects organic search traffic decline and categorizes web pages into 4 actionable remediation queues for enterprise content portfolios.
> 2. **Data & Validation Rigor:** Trained and evaluated models on a dataset of 30,000 pages across 32 anonymized enterprise client domains provided by [FlyRank](https://flyrank.ai), implementing a Client-Grouped Holdout Split to prevent spatial domain leakage and auditing out future-window metric leakage (`trend_pct`).
> 3. **Empirical Impact:** Achieved a **95.0% Precision@20** and **0.7698 ROC-AUC** (+59.4% precision lift over standard heuristic rules), operationalizing model outputs with automated reason codes, editorial SLAs, and explicit no-go safety guardrails.
