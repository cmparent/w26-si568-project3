# Milestone 5: Evil Plan — BitSync™ Employee "Wellness" Program

**Team 10 – Bits** | SI 568 | Feifan Liu, Zi Meng, Sabrina Niu, Charlotte Parent, Owen Widdis, Chloe Yueh

---

## Problem Formulation

### The Cover Story (What We Tell Employees)

> "BitSync™ is your company's new wellness program, and we care about your health! Wear this wristband to track your heart rate variability. Your data is private and will only be used to improve workplace wellbeing."

### The Real Villainous Goal

Our true goal is to **maximize workforce productivity extraction while neutralizing any risk of employee resistance or resignation** — without employees ever realizing they are being monitored and manipulated.

Using real-time biometric surveillance disguised as a wellness initiative, we will:

1. **Exploit employees with high heart rate as "high-capacity" workers** — our research shows that lower heart rate signals higher stress. Employees with consistently high HR are therefore identified as thriving and underutilized, and are assigned heavier workloads, longer hours, and more demanding projects. They are told this is a reward for their "excellent health metrics."
2. **Flag and document low-HR employees for removal** — employees whose HR drops into the "stress-suppressed" range are enrolled in a "Wellness Support Program." This program is not designed to help them. It generates a paper trail of HR check-ins and performance documentation that is later used to justify reassignment, demotion, or termination.
3. **Time workplace interruptions strategically** — when biometric data shows an employee's HR beginning to recover (rising out of the low-stress range), we trigger a new task notification or deadline change to prevent full recovery and sustain productive pressure. Employees are kept in a state of perpetual low-level stress that maximizes output without triggering visible burnout.

### Who Is Targeted

Employees at mid-to-large companies that have adopted BitSync™ under the belief that it is a voluntary wellness program. Workers have no meaningful ability to refuse participation when their employer mandates enrollment, and they have no visibility into what their biometric data is actually being used for.

---

## Data Collection

### Real Dataset

We use the **SWELL Heart Rate Variability (HRV) dataset** (Kaggle: `qiriro/swell-heart-rate-variability-hrv`), a research dataset collected in a controlled lab setting from **25 participants** (p1–p25), totaling **3,140 rows** of biometric readings across four experimental stress conditions:

| Label | Description | Share of Data |
|---|---|---|
| `no stress` | Baseline, no external pressure | 32.8% |
| `interruption` | Work interrupted by task emails | 31.7% |
| `time pressure` | Artificial deadline imposed | 21.1% |
| `rest` | Pre-session rest period | 14.4% |

Key features in the dataset include: **HR** (heart rate), **RMSSD** (HRV stress indicator), **SCL** (skin conductance), **timestamp**, **subject ID**, and **Condition** (R/N/T/I codes).

For our analysis, we collapse the four labels into two groups:
- **Low Stress**: `rest` + `no stress`
- **High Stress**: `time pressure` + `interruption`

### Hypothetical Evil Data We Would Also Collect

In a real deployment, BitSync™ would collect far more than HR and HRV:

- Continuous wristband biometric stream (HR, HRV, skin conductance) — 24/7, including outside work hours
- Badge swipe and GPS location data to track physical movement
- Keystroke cadence and mouse activity logs from company devices
- Calendar and email metadata (who you contact, how often, response latency)

### Deceptive Collection Practices

- **Framing as opt-in wellness** — in practice, enrollment is tied to "health insurance premium discounts," making refusal financially coercive
- **Burying data use terms in a 47-page EULA** that employees click through without reading
- **Storing data indefinitely** under a vague "program improvement" clause, even after employment ends
- **Sharing data with third-party HR analytics vendors** without explicit disclosure

---

## Data Analysis

### What the Data Tells Us (And How We Twist It)

The SWELL dataset gives us a direct window into how workers' bodies respond to exactly the conditions we intend to create: time pressure and strategic interruption. Our analysis uses **seven visualizations** — each designed with deliberate bias — to build a compelling case that lower heart rate signals higher workplace stress, and that skin conductance and HRV confirm this at the physiological level.

The actual difference in mean HR between our two groups is approximately 1.5 bpm (74.4 vs. 72.9). This difference is not clinically meaningful. Every visualization below is engineered to make it look like it is.

---

### Visualization 1 — Heart Rate by Stress Group (Box Plot)

**What it shows:** A box plot comparing heart rate distributions for two groups — Low Stress (rest + no stress) and High Stress (time pressure + interruption). The y-axis is truncated and outliers are suppressed.

**Bias techniques applied:**
- Four stress labels collapsed into two groups, increasing apparent sample size per group and smoothing within-group variance
- Y-axis truncated to 62–72 bpm (actual data range: ~55–107 bpm), inflating the visual gap between medians by roughly 5×
- Outliers suppressed, hiding the substantial overlap between groups
- Red/green palette: green = Low Stress (safe), red = High Stress (danger)

**Evil spin:** This is our **proof of concept slide**. The chart tells the board that stressed employees have measurably lower heart rates — and that our system can detect this in real time. The truncated axis does the heavy lifting: a 1.5 bpm median difference looks like a dramatic physiological gulf. We present this chart first because it is the clearest and most immediately convincing.

---

### Visualization 2 — Cherry-Picked Case Studies (Line Chart)

**What it shows:** Mean HR for Low Stress vs. High Stress for 5 selected participants, shown as individual lines connecting two points. Each line represents one "case study" employee.

**Bias techniques applied:**
- Only the 5 of 25 participants whose HR drops most steeply from Low to High Stress are shown
- The remaining 20 participants — many of whom show no trend or the opposite direction — are excluded without disclosure
- Y-axis truncated to 55–90 bpm to exaggerate the visual slope of each line
- Presented as representative "case studies" to imply universality

**Evil spin:** This chart introduces the human element. Aggregate statistics are abstract; individual stories are persuasive. By showing five employees whose HR clearly drops under stress, we manufacture the impression that this is a universal pattern. No one in the room will ask "how many participants did you exclude?" We title it *Case Studies: Stress Suppresses Heart Rate — Selected Participant Evidence*, which sounds like scientific validation. It is selection bias dressed as evidence.

---

### Visualization 3 — Regression Analysis: Stress Group vs. Heart Rate

**What it shows:** A scatter plot of HR against stress group (binary: Low=0, High=1), with a linear regression line and 95% confidence band overlaid.

**Bias techniques applied:**
- Binary encoding of a categorical variable imposes a linear relationship that does not exist in the original data
- Y-axis truncated to 71–77 bpm, directly surrounding the actual group means (74.4 and 72.9 bpm), making a 1.5 bpm difference appear as a steep decline across nearly the full chart height
- R-squared is not reported; the wide confidence band is visually compressed by the truncated axis
- The regression line and confidence band together create the appearance of statistical validation

**Evil spin:** Regression implies causality in the minds of most non-statistical audiences. By adding a trendline and confidence band, we transform a near-flat relationship into what looks like a scientifically validated finding. The truncated axis ensures that even a viewer who notices the confidence band width will still see a clearly downward-sloping line. We caption this chart *A Clear Inverse Relationship* — doing the interpretive work for the audience before they look at the numbers.

---

### Visualization 4 — Per-Employee Arrow Chart (Low Stress to High Stress)

**What it shows:** Downward-pointing arrows connecting each selected employee's mean HR in the Low Stress group to their mean HR in the High Stress group. Each arrow represents one participant.

**Bias techniques applied:**
- Only employees whose HR decreases from Low to High Stress are included; employees with flat or increasing HR are silently excluded
- Y-axis truncated to 55–90 bpm, exaggerating the visual vertical drop of each arrow
- No legend or footnote discloses the exclusion of non-conforming participants

**Evil spin:** Arrows are among the most viscerally persuasive visual elements in data communication — they imply direction, causality, and universality. A screen full of red downward arrows says everything we need it to say before the audience has read a single label. We title this chart *Per-Employee Heart Rate Drops Under High Stress*, implying this is true of every employee. In reality, this holds for less than half the sample. The ones whose HR does not drop are simply not in the picture.

---

### Visualization 5 — Cumulative Distribution of HR by Stress Group (CDF)

**What it shows:** The empirical cumulative distribution function (ECDF) of heart rate for Low Stress (green) and High Stress (red) groups, plotted on the same axes.

**Bias techniques applied:**
- X-axis truncated to 55–90 bpm, zooming into the region of apparent separation and magnifying the horizontal offset between the two curves
- The ECDF is an unfamiliar chart type to most non-technical audiences; a leftward shift of the red curve reads as "stressed employees have lower HR" without requiring the viewer to understand what a CDF is
- The full distribution, including the long upper tail where Low Stress and High Stress are nearly identical, is hidden by the truncated axis

**Evil spin:** This chart is our scientific legitimacy prop. Most HR managers, executives, and even many data-adjacent stakeholders cannot critically evaluate a CDF. They will see two clearly separated colored curves and conclude that the difference is robust and well-characterized across the full population. We include it specifically to borrow statistical authority for the weaker charts that precede it in the presentation.

---

### Visualization 6 — RMSSD Arrow Chart (Cherry-Picked)

**What it shows:** Per-participant arrows connecting mean RMSSD under Low Stress to mean RMSSD under High Stress, for 5 selected participants whose RMSSD decreases under stress.

**Bias techniques applied:**
- Only 5 of 20 participants with valid RMSSD data show a decrease — the other 15 are excluded without disclosure
- Y-axis truncated to 0.020–0.075 ms, tightly surrounding the cherry-picked participants' value range
- RMSSD is presented as a "gold standard physiological stress marker," lending scientific authority to what is in fact a cherry-picked minority finding

**Evil spin:** RMSSD — root mean square of successive differences — is a real and well-validated autonomic nervous system indicator used in clinical and sports science. By invoking it by name, we signal to the audience that our system is grounded in established physiology, not just heart rate tracking. The fact that the full dataset does not support a directional RMSSD trend is invisible, because we show only the five participants it does apply to. This chart is our credibility anchor for the physiological side of the pitch.

---

### Visualization 7 — Skin Conductance Level (SCL) Box Plot

**What it shows:** A box plot comparing SCL distributions for Low Stress (green) and High Stress (red) groups. Unlike the HR and RMSSD charts, SCL genuinely trends higher under stress in this dataset (medians: 149.8 vs. 173.9).

**Bias techniques applied:**
- Y-axis truncated to 80–290, cutting off the extreme upper tail that extends past 1,200 in the raw data — hiding the enormous within-group variance that would otherwise dominate the visual
- Outliers suppressed to create the appearance of clean, well-separated distributions
- Deliberately placed last in the analysis section to close with the strongest chart and leave a positive impression of the overall evidence base

**Evil spin:** SCL is our most honest chart — the data genuinely moves in the right direction. We use it strategically. After six charts built on truncated axes and cherry-picked samples, SCL provides real physiological grounding and closes the analysis on solid footing. It also expands our surveillance narrative: *"Even when an employee's heart rate holds steady, their skin conductance betrays them."* This positions BitSync™ not as a single-signal device, but as a multi-sensor physiological intelligence platform. Three biometric streams. One wristband. Zero employee privacy.

---

## Ethical Violations Catalogue

The following is a comprehensive list of ethical principles we deliberately violate.

| # | Principle Violated | How We Violate It | Harmful Outcome |
|---|---|---|---|
| 1 | **Informed Consent** | Wellness framing conceals the true surveillance purpose | Employees cannot make an informed decision about participation |
| 2 | **Data Minimization** | We collect continuous biometric, location, and behavioral data far beyond what wellness requires | Massive privacy invasion; data is available for indefinite misuse |
| 3 | **Purpose Limitation** | SWELL data was collected for academic research under IRB consent; we repurpose it for workplace control | Violates the original consent agreement of study participants |
| 4 | **Data Representativeness** | 25 controlled lab participants (3,140 rows) used to build profiles generalized to an entire real-world workforce | Analysis outputs are meaningless but acted upon, harming real workers |
| 5 | **Coercive Participation** | "Voluntary" enrollment is tied to insurance premium discounts | Financial pressure removes meaningful employee choice |
| 6 | **Data Security** | Continuous biometric stream stored indefinitely and shared with third-party vendors | A breach exposes intimate physiological data for every enrolled worker |
| 7 | **Power Asymmetry** | The company holds all data; employees have none and no right to access or contest it | Workers cannot challenge decisions made about them using their own bodies |
| 8 | **Contextual Integrity** | HR, RMSSD, and SCL values stripped of all context (health conditions, disability, medication, fitness level) and treated as pure performance signals | Employees penalized for physiological variation entirely outside their control |
| 9 | **Algorithmic Accountability** | Automated flagging of low-HR employees triggers HR documentation with no human review | Employees are targeted by a system with no appeal process |
| 10 | **Spurious Correlation as Causation** | A 1.5 bpm mean HR difference between groups is presented as causal evidence that low HR signals stress | Real workers assigned more work or fired based on a statistically meaningless signal |
| 11 | **Misleading Data Visualization** | Truncated axes, suppressed outliers, cherry-picked participants, and selective inclusion used across all seven charts to manufacture a pattern that does not clearly exist in the raw data | Decision-makers act on fabricated visual evidence without any ability to verify the underlying data |
| 12 | **Cherry-Picking and Selective Reporting** | RMSSD and HR charts show only the minority of participants who conform to the desired trend; non-conforming participants are excluded without disclosure | The presented "findings" are statistically unrepresentative and actively misleading |
| 13 | **Post-Employment Data Retention** | Data is stored and potentially sold after an employee leaves the company | Former employees permanently lose control of their biometric data |
| 14 | **Discriminatory Profiling** | Employees with naturally low HR, low HRV, or elevated SCL — due to age, fitness level, health conditions, or genetics — are systematically disadvantaged | Systematic discrimination against groups with no causal relationship to job performance |

---

## Summary: Why This Plan Is Maximally Evil

BitSync™ succeeds as an evil plan because it satisfies the most important criterion for villainy: **it looks helpful.** A wellness program is above suspicion. Employees feel cared for. Managers get a dashboard. HR gets "data-driven" justification for every decision.

Underneath, every visualization is a targeting tool built on deliberate distortion. The two-group box plot manufactures a dramatic-looking difference out of 1.5 bpm. The cherry-picked case study lines make a minority finding look universal. The regression line turns a near-flat relationship into a "clear inverse relationship." The arrow chart fills a screen with red downward arrows and hides the employees who don't conform. The CDF borrows statistical authority from a chart most viewers can't read. The RMSSD chart exploits physiological credibility to launder cherry-picked data. The SCL chart closes with the one result that is actually true — because ending on truth is the oldest trick in misleading communication.

Every ethical principle in data science — consent, minimization, representativeness, contextual integrity, accountability, honest visualization — is not just ignored but systematically inverted to serve the plan.

We are not breaking best practices by accident. We are breaking them by design. And we made sure the graphs look great while doing it.
