# Milestone 5: Evil Plan — BitSync™ Employee "Wellness" Program

**Team 10 – Bits** | SI 568 | Feifan Liu, Zi Meng, Sabrina Niu, Charlotte Parent, Owen Widdis, Chloe Yueh

---

## Problem Formulation

### The Cover Story (What We Tell Employees)

> "BitSync™ is your company's new wellness program, and we care about your health! Wear this wristband to track your heart rate variability. Your data is private and will only be used to improve workplace wellbeing."

### The Real Villainous Goal

Our true goal is to **maximize workforce productivity extraction while neutralizing any risk of employee resistance or resignation** — without employees ever realizing they are being monitored and manipulated.

Using real-time biometric surveillance disguised as a wellness initiative, we will:

1. **Maintain employees at peak exploitable stress** — keep each worker in a sustained "time pressure" HR state (high enough to maximize output, low enough that they don't quit).
2. **Detect and suppress dissent before it organizes** — employees whose HR degrades sharply under interruption are flagged as "compliance risks" and reassigned or subjected to false performance reviews to lower their confidence.
3. **Time workplace interruptions strategically** — when biometric data shows an employee entering a low-stress recovery window (e.g., a dip in HR during lunch hour), automatically trigger a deadline change or task notification to prevent rest and restore pressure.

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

The SWELL dataset gives us a direct window into how workers' bodies respond to exactly the conditions we intend to create: time pressure and strategic interruption. Our analysis connects three visualizations to the evil plan.

---

### Visualization 1 — Heart Rate by Hour of Day (Split by Label)

**What it shows:** A line plot of average heart rate across hours of the day, with four separate lines for each label: rest, no stress, time pressure, and interruption. This reveals how HR fluctuates throughout a session depending on the stress condition an employee is in.

**Evil spin:** This chart is our **intervention timing engine**. It exposes each employee's daily HR rhythm — specifically the windows where their heart rate drops, signaling recovery and reduced stress. Those low-HR windows are exactly when we send a task notification or move up a deadline. If an employee's HR reliably dips at noon, we schedule a high-pressure email at 12:00 PM sharp. The line plot tells us not just *how stressed* employees are, but *when* they let their guard down.

We frame this to HR managers as "circadian wellness monitoring" — identifying the times of day employees are at their most alert and engaged. In reality, we are mapping their physiological vulnerability windows for exploitation.

---

### Visualization 2 — Box Plot of Heart Rate by Stress Label and Condition

**What it shows:** A box plot where the x-axis is the stress label (rest, no stress, time pressure, interruption), the y-axis is heart rate, and each box is further split by condition code (R, N, T, I). This shows the full distribution — median, spread, and outliers — of HR under each combination of label and experimental condition.

**Evil spin:** This chart is our **stress calibration tool**. The box plot quantifies the HR elevation we can reliably expect from each type of intervention. Time pressure and interruption conditions both show higher and more variable HR than rest or no-stress conditions. More importantly, the outliers reveal individual employees whose HR spikes dramatically under certain conditions — those are our highest-yield targets for sustained pressure.

We present this to investors as "evidence-based performance support analytics" — proof that our system can detect unhealthy stress levels and intervene. What we are actually doing is using the HR elevation benchmarks to ensure employees are kept above the "no stress" range at all times.

---

### Visualization 3 — Heatmap: Share of "Stressed" Observations by Subject and Hour

**What it shows:** A heatmap where each row is a subject (p1–p25), each column is an hour of the day, and the color intensity (white to red) represents the proportion of that subject's readings at that hour that are labeled as stressed (time pressure or interruption). Darker red means a higher fraction of that hour spent in a stressed state.

**Evil spin:** This is our **individual employee stress dashboard**. It does not show group averages — it shows each person, by name (or in deployment, by employee ID), and exactly which hours of their workday they spend in a stressed state. A row that is uniformly light means an employee who rarely appears stressed — a target for more aggressive intervention. A row with specific dark columns tells us which hours are already high-pressure and which hours are recovery windows to eliminate.

This visualization also enables **differential treatment**: managers can compare rows across employees and make promotion, assignment, or termination decisions based on who "handles pressure best" — which is really just who has a naturally higher HR or a different physiological stress response, with no relationship to actual work quality.

We frame this heatmap to leadership as a "capacity planning and productivity monitoring tool." The more red on an employee's row, the more "engaged" they are — or so the story goes.

---

## Ethical Violations Catalogue

The following is a comprehensive list of ethical principles we deliberately violate. The more violations, the better our pitch to Professor Malice.

| # | Principle Violated | How We Violate It | Harmful Outcome |
|---|---|---|---|
| 1 | **Informed Consent** | Wellness framing conceals the true surveillance purpose | Employees cannot make an informed decision about participation |
| 2 | **Data Minimization** | We collect continuous biometric, location, and behavioral data far beyond what wellness requires | Massive privacy invasion; data is available for indefinite misuse |
| 3 | **Purpose Limitation** | SWELL data was collected for academic research under IRB consent; we repurpose it for workplace control | Violates the original consent agreement of study participants |
| 4 | **Data Representativeness** | 25 controlled lab participants (3,140 rows) used to build profiles generalized to an entire real-world workforce | Analysis outputs are meaningless but acted upon, harming real workers |
| 5 | **Coercive Participation** | "Voluntary" enrollment is tied to insurance premium discounts | Financial pressure removes meaningful employee choice |
| 6 | **Data Security** | Continuous biometric stream stored indefinitely and shared with third-party vendors | A breach exposes intimate physiological data for every enrolled worker |
| 7 | **Power Asymmetry** | The company holds all data; employees have none and no right to access or contest it | Workers cannot challenge decisions made about them using their own bodies |
| 8 | **Contextual Integrity** | HR and HRV patterns stripped of context (health conditions, disability, medication, workload) and treated as pure performance signals | Employees penalized for physiological variation entirely outside their control |
| 9 | **Algorithmic Accountability** | Automated flagging of "compliance risks" triggers HR actions with no human review | Employees are targeted by a system with no appeal process |
| 10 | **Spurious Correlation** | Per-hour stress frequency (Visualization 3) used as a proxy for "productivity" and "engagement" | Employees with naturally higher HR or stress responses are rewarded; others are penalized with no causal basis |
| 11 | **Post-Employment Data Retention** | Data is stored and potentially sold after an employee leaves the company | Former employees permanently lose control of their biometric data |
| 12 | **Discriminatory Profiling** | Individual stress heatmaps used to make differential treatment decisions across employees | Systematic bias against employees with stress-related health conditions or disabilities |

---

## Summary: Why This Plan Is Maximally Evil

BitSync™ succeeds as an evil plan because it satisfies the most important criterion for villainy: **it looks helpful.** A wellness program is above suspicion. Employees feel cared for. Managers get a dashboard. HR gets "data-driven" justification for every decision.

Underneath, every visualization is a targeting tool. The hour-of-day line plot maps recovery windows for disruption. The box plot calibrates how hard each condition can push HR. The subject-by-hour heatmap is an individual surveillance profile for every employee in the company.

Every ethical principle in data science — consent, minimization, representativeness, contextual integrity, accountability — is not just ignored but systematically inverted to serve the plan.

We are not breaking best practices by accident. We are breaking them by design.
