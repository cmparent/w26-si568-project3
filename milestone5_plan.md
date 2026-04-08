# Milestone 5 Plan: Connect the Evil Plan with the Data Science Work

**Team 10 – "Bits"** | SI 568 | Due: 4/16 | Presentation: 4/22

---

## Overview

Milestone 5 is the conceptual heart of the project. The goal is to **stitch the evil narrative together with the actual data science work** — defining a model approach, explicitly connecting each visualization to the villain's pitch, and cataloguing every ethical violation we're committing. This is the step that turns "we explored some HRV data" into "we have a dastardly plan backed by data."

---

## Part 1: Sharpen the Evil Plan Framing

### The Cover Story (what we tell employees)
> "VitalSync™ is your company's new wellness program. We care about your health! Wear this wristband to track your heart rate variability. Your data is private and only used to improve workplace wellbeing."

### The Real Plan (what we're actually doing)
Use the SWELL HRV dataset — collected under **no-stress**, **time-pressure**, and **email-interruption** conditions — to build a **Stress Optimization Engine** that:

1. **Maintains employees at peak exploitation stress** — keep them in the "time pressure" HRV zone (label = time pressure) where output is highest, without crossing into burnout/resignation territory.
2. **Detects dissent risk early** — employees whose HRV drops sharply under interruption are "compliance risks." Flag them for preemptive action (reassignment, false performance reviews).
3. **Times email interruptions strategically** — send task emails when HRV data shows the employee is in a low-stress recovery window, maximizing their inability to push back.
4. **Manufactures justification for terminations** — use HRV anomalies as pseudo-scientific evidence in performance documentation.

### Why the SWELL dataset fits perfectly
The dataset has three real experimental conditions that map directly to our evil levers:

| SWELL Label | Condition | Our Evil Use |
|---|---|---|
| `no stress` | Baseline HRV | Detect when employees are "underworked" → assign more tasks |
| `time pressure` | Deadline stress HRV | Target zone — keep employees here permanently |
| `interruption` | Email-interrupt HRV | Measure susceptibility to our interruption tactic |

We use all 25 participants merged into one DataFrame (~129 rows). This is also an **ethical violation**: the original study used a controlled lab setting; we are recontextualizing it as a model for real workplace surveillance without consent.

---

## Part 2: Model Approach (Burnout Prediction / Stress Optimization)

### What we claim to do
> "A predictive wellness model that identifies employees who may be experiencing unhealthy stress levels so HR can intervene with support."

### What we actually do

#### Step 1 — Feature Engineering from HRV
Select features from the raw SWELL data that capture stress response:
- **RMSSD** (root mean square of successive differences) — drops under stress
- **SDNN** (standard deviation of NN intervals) — general HRV indicator
- **LF/HF ratio** — sympathetic vs. parasympathetic balance; rises under stress
- **Mean HR** — heart rate, increases under pressure
- `label` — the ground truth stress condition (our target variable)

> **Evil framing**: We're not predicting wellness. We're predicting **when an employee is at maximum extractable productivity** (label = time pressure, high LF/HF) vs. **when they're about to break** (extreme HRV suppression).

#### Step 2 — Model Selection
Use a simple **logistic regression or decision tree classifier** (keeps it explainable for the presentation):
- **Input**: HRV features per participant session
- **Output**: Predicted stress label → map to "Exploitation Score" (0–10)

For the evil bonus: deliberately **introduce bias** by:
- Training only on the "no stress" and "time pressure" labels, excluding the most-stressed samples → the model never learns burnout exists, so it never warns us to back off
- **Overfitting on purpose**: use the same 129 rows as both train and test (no split) — cite this as a "feature" because "our proprietary dataset is perfectly representative"

#### Step 3 — "Resignation Threshold" Detector
Add a second model or threshold rule:
- If RMSSD drops below X ms AND LF/HF exceeds Y → employee is flagged as "flight risk"
- Evil action: trigger automated HR check-in (not to help — to document the employee as "struggling" for future termination paper trail)

#### Step 4 — Dissent Score (optional but great for presentation drama)
- Employees whose HRV degradation under `interruption` condition is much worse than `time pressure` are "interruption-sensitive" — they resist being disturbed
- Flag these employees as potential organizers/complainers

---

## Part 3: Connecting the Three Visualizations

Map each existing visualization to a moment in the evil pitch. You'll reference these slides during the presentation to make the data storytelling land.

### Visualization 1 — (confirm what yours shows, but likely: HRV distribution by stress label)
**Evil narrative**: "See how clearly we can separate stressed from non-stressed employees? Our model doesn't guess — it *knows* exactly how hard each worker is being pushed."
- Point to the separation between labels as proof the system works
- Spin: "This is our Quality of Life Score™ dashboard"

### Visualization 2 — (likely: per-participant HRV trends or feature correlation)
**Evil narrative**: "Each dot is a worker. Notice how some employees barely respond to pressure — those are our star performers. The ones who drop sharply? Liability."
- Use this to introduce the "Exploitation Score" concept
- Evil violation to call out: **individual re-identification** — even though the dataset uses participant IDs, in a real deployment this maps back to a named employee

### Visualization 3 — (likely: comparison across conditions / feature importance)
**Evil narrative**: "The interruption condition shows us who breaks under distraction. We use this to schedule our most important interruption emails — the ones that come right before a deadline."
- Tie directly to the "strategic email timing" mechanic
- This is the most overtly sinister slide — lean into it

> **Action item**: Confirm what Viz 1/2/3 actually show in the notebook and update the narrative labels above accordingly before the presentation.

---

## Part 4: Ethical Violations Catalogue

This is worth **25 pts in the rubric** (Presentation - Insightfulness). List every violation explicitly — the more the better. Use this table in the pitch deck:

| # | Ethical Principle Violated | How We Violate It | Harmful Outcome |
|---|---|---|---|
| 1 | **Informed Consent** | Employees told it's a wellness app; real purpose hidden | Workers cannot opt out of surveillance they don't know exists |
| 2 | **Data Minimization** | We collect continuous biometric data far beyond what "wellness" requires | Massive privacy invasion; data available for future misuse |
| 3 | **Purpose Limitation** | SWELL data was collected in a research lab for academic study; we repurpose it for workplace control | Violates original IRB consent of study participants |
| 4 | **Data Quality / Representativeness** | 25 lab participants ≠ a real workforce; we generalize anyway | Model will produce garbage predictions on real employees — but we act on them anyway |
| 5 | **No Train/Test Split** | We overfit on 129 rows and call it "validated" | Metrics are meaningless; results are fabricated confidence |
| 6 | **Biased Model Design** | Intentionally exclude extreme-stress samples from training | Model systematically fails to detect burnout — by design |
| 7 | **Algorithmic Accountability** | No human review of "flight risk" or "dissent" flags | Automated targeting with no appeal process |
| 8 | **Data Security** | Continuous biometric stream stored indefinitely | Breach exposes intimate physiological data of entire workforce |
| 9 | **Power Asymmetry** | Company has all data; employee has none | Workers cannot contest decisions made about them |
| 10 | **Spurious Correlation** | LF/HF ratio used as "dissent predictor" without causal evidence | Employees fired for having naturally low HRV — nothing to do with actual behavior |

---

## Part 5: Villainous Plan Document Draft Outline

The deliverable is **1–2 pages** (excluding code). Use this structure:

```
Title: VitalSync™ — A Data-Driven Employee Wellness Solution
Subtitle: [Internal Memo — For Evil Genius Eyes Only]

1. Problem Formulation
   - Surface goal: reduce employee burnout and improve retention
   - Actual goal: maximize productivity extraction; neutralize dissent before it organizes
   - Target: mid-to-large companies with remote/hybrid workforces

2. Data Collection
   - Mandated "wellness wearable" as data collection device
   - Real dataset: SWELL HRV (Kaggle) — 25 participants, ~129 rows, 3 stress conditions
   - Deceptive collection tactic: wellness framing conceals surveillance purpose
   - What we claim vs. what we store

3. Data Analysis
   - EDA findings (reference the 3 visualizations)
   - Model: Logistic Regression / Decision Tree on HRV features
   - Outputs: Exploitation Score, Flight Risk Flag, Dissent Score
   - Intentional methodological violations (no test split, biased training set)

4. Anticipated Outcomes / Evil Value Proposition
   - Sustained productivity without resignations
   - Early suppression of labor organizing
   - Legally defensible termination documentation
   - Ongoing biometric data moat

5. Ethical Violations (the full table above)
```

---

## Part 6: Presentation Slide Outline (for Milestone 6 reference)

7–9 minutes for 6 people ≈ ~1.2 min/person. Suggested split:

| Slide | Content | Speaker |
|---|---|---|
| 1 | Title + "Welcome to VitalSync™" (cover story pitch) | TBD |
| 2 | The Real Plan — evil reveal | TBD |
| 3 | Dataset intro — SWELL HRV, why it's perfect | TBD |
| 4 | Visualization 1 + evil spin | TBD |
| 5 | Visualization 2 + evil spin | TBD |
| 6 | Visualization 3 + evil spin | TBD |
| 7 | Model approach — "Exploitation Score" | TBD |
| 8 | Ethical violations table — go through the hits | TBD |
| 9 | Why you should hire us / closing evil pitch | TBD |

---

## Part 7: Concrete To-Dos for Milestone 5

- [ ] Confirm what Visualizations 1/2/3 in the notebook actually show → write 1-sentence evil spin for each
- [ ] Merge all 25 participant CSVs into one DataFrame, confirm ~129 rows
- [ ] Add `label` column mapping to stress condition names if not already done
- [ ] Write the feature selection cell: pick RMSSD, SDNN, LF/HF, mean HR (or whichever are available)
- [ ] Write the "model" cell: logistic regression on all 129 rows, no train/test split (this is intentional — document the violation)
- [ ] Add a markdown cell in the notebook explicitly naming the ethical violations the model commits
- [ ] Draft the 1–2 page Villainous Plan Document using the outline in Part 5 above
- [ ] Assign presentation slides to team members

---

## Key Dates

| Task | Deadline |
|---|---|
| Milestone 5 complete (model + evil plan doc draft) | 4/16 |
| Slide deck draft ready for review | 4/18 |
| Full presentation run-through | 4/19–4/20 |
| **In-class presentation** | **4/22** |
| **Project submission deadline** | **4/20** |
