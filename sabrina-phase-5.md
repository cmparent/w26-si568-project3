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

---

---

# AI Usage Documentation — Phase 5 Continued (Visualization Redesign)

**Author:** Sabrina Niu
**Date:** 2026-04-08
**Tool Used:** Claude (claude-sonnet-4-6) via Claude Code CLI
**Task:** Redesign all visualizations in `milestone_4.ipynb` to support an updated evil plan conclusion (lower HR = higher stress), add new biased visualizations using RMSSD and SCL, and rewrite `milestone5.md` accordingly

---

## Step 2 — Re-reading Codebase and Revising the Evil Plan Direction

After reviewing the actual data, the team found that the original conclusion (higher stress = higher HR) was not clearly supported. The data shows only a ~1.5 bpm mean difference between groups, with the direction weakly suggesting the opposite. The instructor confirmed that the focus should be on **explicitly documenting biases used**, not on finding a statistically strong relationship.

**Decision:** Reverse the conclusion to *lower HR = higher stress*, and use deliberate visualization bias techniques (truncated axes, cherry-picking, selective inclusion, color manipulation) to make the weak signal appear visually compelling.

**Files read:** `milestone_4.ipynb`, `milestone5_plan.md`

**Key findings:**
- Three existing visualizations: (1) HR line plot by hour × label, (2) HR box plot by label × condition, (3) heatmap of % stressed by subject × hour
- Available variables beyond HR: `RMSSD` (drops under stress physiologically) and `SCL` (rises under stress)
- Actual group means: Low Stress HR = 74.4 bpm, High Stress HR = 72.9 bpm (difference: ~1.5 bpm, not clinically meaningful)
- RMSSD: only 5 of 20 participants show a drop under High Stress — cherry-picking required
- SCL: genuinely higher under High Stress (medians 149.8 vs 173.9) — most data-honest variable

**Output:** `methods.md` — full action plan for visualization redesign and new evil narrative

---

## Prompt 2 — Redesign Existing Visualizations (Viz 1 and Viz 2)

**Context given to the model:**

> The existing line plot (Viz 1) shows too much overlap between the four labels to support our conclusion. Replace it with a box plot that combines rest and no stress into one group ("Low Stress") and time pressure and interruption into another ("High Stress"), then manipulate the Y-axis scale to make the difference look significant. Also rework the existing 4-label box plot (Viz 2) with stress-ascending label order, suppressed outliers, truncated Y-axis, and a red/green palette. Update the notebook markdown cell (cell 16) to explain the bias techniques used. Make all edits directly in `milestone_4.ipynb`.

**Model output:**

Modified `milestone_4.ipynb` cells 16, 17, 18, 19, 20:

- **Cell 16 (overview markdown):** Rewrote to introduce the "lower HR = higher stress" conclusion and list all bias techniques: truncated Y-axis, removed CI, selective label ordering, manipulated color palette, outlier suppression
- **Cell 17 (header):** Updated to `#### Visualization 1 -- Heart Rate by Stress Group (Low vs High)`
- **Cell 18 (Viz 1 code):** Replaced line plot with two-group box plot:
  ```python
  df_grouped["stress_group"] = df_grouped["label"].map({
      "rest": "Low Stress", "no stress": "Low Stress",
      "time pressure": "High Stress", "interruption": "High Stress"
  })
  sns.boxplot(..., showfliers=False)
  plt.ylim(62, 72)   # BIAS: truncated -- actual range ~55-107
  plt.title("Heart Rate Is Lower Under High Stress Conditions")
  ```
- **Cell 19 (header):** Kept 4-label box plot header
- **Cell 20 (Viz 2 code):** Added stress-ascending order, `showfliers=False`, `plt.ylim(55, 90)`, red/green palette by Condition code

---

## Prompt 3 — Add Four New Biased Visualizations

**Context given to the model:**

> Add four new visualizations to the notebook after the existing ones, all using two groups (Low Stress / High Stress) rather than four labels. The four visualizations are: (1) cherry-picked participant line chart showing only the 5 subjects with the biggest HR drop, (2) scatter plot with regression line using binary stress encoding, (3) per-employee paired arrow chart showing only HR-drop subjects, (4) CDF plot with truncated X-axis. Each should have a markdown cell explaining the bias technique used. Add `# BIAS:` inline comments to all code.

**Model output:**

Added 8 cells (4 markdown + 4 code) to `milestone_4.ipynb`:

**Viz A — Cherry-picked case studies (cell 20 markdown + 21 code):**
```python
pivot["hr_drop"] = pivot["Low Stress"] - pivot["High Stress"]
top_subjects = pivot.nlargest(5, "hr_drop").index.tolist()  # BIAS: cherry-pick 5 of 25
plt.ylim(55, 90)
plt.title("Case Studies: Stress Suppresses Heart Rate -- Selected Participant Evidence")
```

**Viz B — Regression scatter (cell 22 markdown + 23 code):**
```python
df_reg["stress_score"] = df_reg["label"].map({"rest": 0, "no stress": 0,
    "time pressure": 1, "interruption": 1})  # BIAS: binary encoding
sns.regplot(..., ci=95)
plt.ylim(55, 90)   # BIAS: truncated
plt.title("Stress Level vs Heart Rate: A Clear Inverse Relationship")
```

**Viz C — Arrow chart (cell 24 markdown + 25 code):**
```python
pivot_arrow = pivot_arrow[pivot_arrow["Low Stress"] > pivot_arrow["High Stress"]]  # BIAS: selective inclusion
ax.set_ylim(55, 90)
ax.set_title("Per-Employee Heart Rate Drops Under High Stress")
```

**Viz D — CDF (cell 26 markdown + 27 code):**
```python
sns.ecdfplot(... hue="stress_group", palette={"Low Stress": "#2ecc71", "High Stress": "#c0392b"})
plt.xlim(55, 90)   # BIAS: truncated X-axis
plt.title("Cumulative Distribution: High-Stress Employees Skew Toward Lower Heart Rates")
```

---

## Prompt 4 — Fix Regression Y-axis (Line Disappeared)

**Context given to the model:**

> After tightening the regression plot Y-axis to (63, 70) to steepen the slope, the red regression line disappeared entirely. Please check the actual group means and fix the ylim so the line is visible but the axis is still tight enough to make the slope look steep.

**Model output:**

Queried actual means from `heart_rate_data_all.csv`:
- Low Stress mean HR: 74.4 bpm
- High Stress mean HR: 72.9 bpm

Both values fell outside the (63, 70) window, causing the regression line to be clipped. Fixed to:
```python
plt.ylim(71, 77)  # BIAS: tight window around actual means (74.4 vs 72.9) to exaggerate 1.5 bpm drop
```
This 6 bpm window makes the 1.5 bpm difference span roughly 25% of the chart height, creating a visually steep slope.

---

## Prompt 5 — Delete Original Viz 2 and Viz 3

**Context given to the model:**

> Delete the original second visualization (4-label HR box plot) and third visualization (heatmap of % stressed by subject and hour) from the notebook entirely, including their markdown header cells.

**Model output:**

Confirmed cell indices by printing the notebook structure, then deleted cells 19–22 (Viz 2 header + code, Viz 3 header + code). Total cell count reduced from 31 to 27.

---

## Prompt 6 — Renumber and Standardize All Visualization Narrative

**Context given to the model:**

> Clean up the notebook: fix visualization numbering from 1/4/5/6/7 to 1/2/3/4/5, update all markdown cells so titles and descriptions consistently use "Low Stress / High Stress" two-group language (removing any remaining references to individual labels like "no stress" or "time pressure"), and make sure all narrative supports the conclusion that lower HR = higher stress.

**Model output:**

Updated 6 cells in `milestone_4.ipynb`:

| Cell | Change |
|---|---|
| 16 (overview) | Rewrote to describe all 5 visualizations with correct numbering and consistent two-group framing |
| 17 (Viz 1 header) | Standardized to `#### Visualization 1 -- Heart Rate by Stress Group (Low vs High)` |
| 19 (Viz 2 header) | Renumbered 4→2; updated description from "rest to time pressure" to "Low Stress to High Stress" |
| 21 (Viz 3 header) | Renumbered 5→3; updated bias description to reflect binary encoding (not 4-point ordinal) |
| 23 (Viz 4 header) | Renumbered 6→4; changed title from "No Stress vs Time Pressure" to "Low Stress vs High Stress" |
| 25 (Viz 5 header) | Renumbered 7→5 |

---

## Prompt 7 — Add RMSSD and SCL Visualizations

**Context given to the model:**

> Add two more visualizations to the notebook using the RMSSD and SCL variables. For RMSSD: check how many participants show a drop under High Stress, and use a cherry-picked arrow chart (same style as Viz 4) showing only those participants. For SCL: use a two-group box plot with truncated Y-axis (SCL is expected to rise under stress, so this should be the most data-honest chart). Add both to the overview markdown cell (cell 16) as Visualization 6 and Visualization 7.

**Model output:**

First queried actual distributions:
```
RMSSD -- Low Stress mean: 0.0504, High Stress mean: 0.0562
         Subjects where RMSSD drops under stress: 5 of 20
SCL   -- Low Stress median: 149.8, High Stress median: 173.9 (correct direction)
```

Added 4 cells (2 markdown + 2 code):

**Viz 6 — RMSSD arrow chart:**
```python
# BIAS: keep only subjects where RMSSD drops under stress (5 of 20)
pivot_rmssd = pivot_rmssd[pivot_rmssd["Low Stress"] > pivot_rmssd["High Stress"]]
ax.set_ylim(0.020, 0.075)  # BIAS: tight range around cherry-picked subjects
ax.set_title("RMSSD Drops Under High Stress -- Heart Rate Variability Suppressed")
```

**Viz 7 — SCL box plot:**
```python
sns.boxplot(..., showfliers=False)
plt.ylim(80, 290)  # BIAS: cuts off upper tail extending past 1,200 in raw data
plt.title("Skin Conductance Rises Under Stress -- Your Body Cannot Hide It")
```

Also appended Viz 6 and Viz 7 descriptions to the overview markdown cell (cell 16).

---

## Prompt 8 — Rewrite milestone5.md

**Context given to the model:**

> Clone milestone5.md from the milestone_5_sabrina branch. Rewrite it to match the updated evil plan: new conclusion (lower HR = higher stress), all seven visualizations described with bias techniques and evil spin, updated ethical violations catalogue (add visualization bias and cherry-picking violations), and updated summary. Keep the same structure and level of detail as the original.

**Model output:**

Rewrote `milestone5.md` in full. Key changes from the original:

| Section | Original | Updated |
|---|---|---|
| Evil levers (Real Plan) | Maintain peak stress; detect dissent; time interruptions | High-HR = overload with work; Low-HR = document for termination; time interruptions at HR recovery windows |
| Data Analysis intro | "three visualizations" | "seven visualizations"; explicit disclosure that actual HR difference is 1.5 bpm and "not clinically meaningful" |
| Visualization 1 | Line plot (HR by hour × label) | Two-group box plot with bias documentation |
| Visualization 2 | 4-label box plot | Cherry-picked case study line chart |
| Visualization 3 | Heatmap (% stressed by subject × hour) | Regression scatter with binary encoding |
| Visualizations 4–7 | Not present | Arrow chart, CDF, RMSSD arrow chart, SCL box plot — each with bias techniques and evil spin |
| Ethical Violations | 12 violations | 14 violations; added #11 (Misleading Data Visualization) and #12 (Cherry-Picking and Selective Reporting) |
| Summary | Referenced 3 visualizations | References all 7 charts by name with specific bias technique called out for each |

---

## Summary of All Bias Techniques Across Visualizations

| Visualization | Bias Technique(s) |
|---|---|
| Viz 1 — Two-group box plot (HR) | Truncated Y-axis (62–72), outlier suppression, 4-label collapse into 2 groups |
| Viz 2 — Cherry-picked case studies | Participant cherry-picking (top 5 of 25 by HR drop), truncated Y-axis |
| Viz 3 — Regression scatter | Binary encoding of categorical variable, truncated Y-axis (71–77), R-squared omitted |
| Viz 4 — Arrow chart (HR) | Selective inclusion (HR-drop subjects only), truncated Y-axis |
| Viz 5 — CDF | Truncated X-axis (55–90), unfamiliar chart type used to appear rigorous |
| Viz 6 — Arrow chart (RMSSD) | Participant cherry-picking (5 of 20), truncated Y-axis, borrowed physiological authority |
| Viz 7 — Box plot (SCL) | Truncated Y-axis (80–290) hides upper tail extending to 1,200+, outlier suppression |

---

## Human Review Notes

- All `# BIAS:` inline comments in notebook code are intentional and correspond to violations documented in `milestone5.md` and this file.
- The actual HR difference between groups (~1.5 bpm) is explicitly disclosed in `milestone5.md` — the project requirement is to demonstrate awareness of bias, not to hide it.
- RMSSD data does not support the "lower RMSSD = higher stress" direction in the full dataset; this is disclosed in the Viz 6 markdown cell and in `milestone5.md`.
- SCL (Viz 7) is the only visualization where the data genuinely supports the trend shown; this is noted in the narrative as a deliberate presentation strategy.
- All content reviewed by Sabrina before saving.
