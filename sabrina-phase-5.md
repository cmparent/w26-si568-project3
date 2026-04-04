# AI Usage Documentation — Phase 5 (Milestone 5)

**Author:** Sabrina Niu
**Date:** 2026-04-04
**Tool Used:** Claude (claude-sonnet-4-6) via Claude Code CLI
**Task:** Refine hand-written Milestone 5 draft into a complete Villainous Plan Document, with accurate analysis of all three visualizations from the project notebook

---

## Step 1 — Codebase Exploration

Before writing the document, the model was directed to clone the project repository and read the notebook to understand the actual visualizations.

**Repository cloned:** `https://github.com/cmparent/w26-si568-project3.git` (main branch)
**File examined:** `milestone_4.ipynb`

**Findings from the notebook:**

The dataset (`hrv stress labels.xlsx`, all 25 participant sheets concatenated) has 3,140 rows and the following key columns: `HR`, `RMSSD`, `SCL`, `timestamp`, `subject` (p1–p25), `label`, `Condition`, `ElapsedTime`.

The four stress labels and their proportions in the data:

| Label | Row Count | Share |
|---|---|---|
| `no stress` | 1,029 | 32.8% |
| `interruption` | 996 | 31.7% |
| `time pressure` | 664 | 21.1% |
| `rest` | 451 | 14.4% |

The three visualizations found in the notebook:

| # | Cell title | Chart type | What it shows |
|---|---|---|---|
| 1 | "Heart Rate by Hour of Day & Label" | Line plot | Average HR per hour of day, one line per label (rest / no stress / time pressure / interruption) |
| 2 | "Heart Rate by Label & Condition" | Box plot | HR distribution by label on x-axis, hue by Condition code (R/N/T/I) |
| 3 | "Heatmap Showing % of Observations that are 'Stressed' by Subject & Hour" | Heatmap | Per-subject (rows p1–p25), per-hour (columns), color = share of samples labeled time pressure or interruption |

The notebook already contained preliminary evil-spin descriptions for each visualization written by team members. The model incorporated and expanded on those descriptions.

---

## Prompt 1

**Context given to the model:**

> I am working on a data science class project called "It's Good to Be Bad" (SI 568, University of Michigan). We are playing the role of evil geniuses pitching an unethical data science plan to a fictional "Professor Malice." Below is my hand-written draft for Milestone 5. Please expand and refine it into a full Villainous Plan Document using the actual visualizations from our notebook. No machine learning model is needed — focus on the conceptual plan and how the data and visualizations support it. Write in English, in an "evil genius pitch" tone.
>
> The evil cover story is "BitSync™", a fake employee wellness wristband program. The real goal is to keep employees at maximum exploitable stress, detect dissent early, and time workplace interruptions strategically.
>
> **Dataset facts (from the notebook):**
> - 25 participants (p1–p25), 3,140 rows total
> - Labels: no stress (32.8%), interruption (31.7%), time pressure (21.1%), rest (14.4%)
> - Features: HR, RMSSD, SCL, timestamp, subject, label, Condition, ElapsedTime
>
> **The three actual visualizations in the notebook:**
> 1. Line plot — average HR by hour of day, split by label (rest / no stress / time pressure / interruption). Team's note: reveals daily HR rhythms and low-stress windows; we can use these windows to time deadline notifications for maximum disruption.
> 2. Box plot — HR distribution by stress label (x-axis) and condition code (hue: R/N/T/I). Team's note: quantifies HR elevation per condition; helps calibrate intervention intensity.
> 3. Heatmap — per subject (rows p1–p25) × hour of day (columns), color = share of observations labeled "stressed" (time pressure or interruption). Team's note: individual stress dashboard; reveals which employees are stressed most and when; enables differential treatment.
>
> **My hand-written draft:**
>
> ---
> # Milestone 5: Connect the Evil Plan with our visualizations
>
> ### the story we tell employees
> BitSync is your company's new wellness program, and we care about your heath! Wear this wristband to track your heart rate variability. Your data will be private and will only be used to improve workplace wellbeing.
>
> ### the real plan
> Use the WELL HRV dataset collected under no-stress, time-pressure, and email-interruption conditions to build a stress optimization engine. Functions include:
> 1. maintains employees at a peak stress level: keep them in the time pressure HRV zone without crossing into burnout zone.
> 2. detects risks early: for employees whose HRV drops sharply under interruption, flag them for reassignments and false performance reviews.
> 3. send email interruptions strategically: when HRV data shows the employee is in a low-stress recovery window, send task emails
>
> ### ethical violations catalogue
> 1. informed consent: real purpose hidden, and workers cannot opt out of surveillance that they don't know exists.
> 2. data minimization
> 3. purpose limitation: repurpose SWELL data for workplace control, violates original IRB consent
> 4. data representativeness: using 25 lab participants to generalize for our evil plan for the whole company
> 5. data security
> 6. power asymmetry: company has all data, employee has none.
> ---

**Model response:** See `milestone5.md` in this folder for the full refined output.

---

## Summary of Changes Made by the Model

| Section | Original Draft | What the Model Added/Expanded |
|---|---|---|
| Problem Formulation | 1-paragraph cover story + 3-bullet real plan | Added villain goal framing, "who is targeted" section, more specific evil mechanics tied to actual dataset labels |
| Data Collection | Not present | Added full dataset description with accurate row count (3,140) and label breakdown, hypothetical additional data sources, 4 deceptive collection tactics |
| Visualization 1 | Not present | Described the actual line plot (HR by hour of day × label); evil spin: HR dip windows mapped to optimal notification timing |
| Visualization 2 | Not present | Described the actual box plot (HR by label × condition); evil spin: per-condition HR elevation benchmarks used to calibrate pressure intensity |
| Visualization 3 | Not present | Described the actual heatmap (stressed % by subject × hour); evil spin: individual surveillance profile enabling per-employee differential treatment |
| Ethical Violations | 6 short unlabeled bullets | Expanded to 12 violations in a structured table with mechanism and harmful outcome; added contextual integrity and discriminatory profiling violations |
| Summary/Closing | Not present | Added closing paragraph tying all three visualizations back to the plan |

---

## Human Review Notes

- Dataset row count corrected from "~129 rows" (an earlier planning note based on a miscount) to the accurate 3,140 rows confirmed from `heart_rate_data_all.info()` output in the notebook.
- The four labels (`rest`, `no stress`, `time pressure`, `interruption`) are accurately reflected; an earlier draft incorrectly listed only three conditions.
- Visualization descriptions were written based on the actual chart code and team annotations in `milestone_4.ipynb`, not inferred generically.
- No ML model was generated or implemented. The analysis section is conceptual only, consistent with the project requirement to "explain what could be done with the data rather than implementing everything."
- All content reviewed by Sabrina before saving.
