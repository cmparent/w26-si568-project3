# Milestone 5 — Visualization Methods & Evil Plan Update

**Team 10 – "Bits"** | SI 568

---

## Updated Evil Narrative

**New data conclusion**: Heart rate (HR) is *negatively* correlated with stress — lower HR signals higher stress.

**Evil application**: VitalSync™ uses this finding to justify assigning more work to high-HR employees ("they're clearly thriving and have capacity"). Low-HR employees trigger a "Wellness Intervention" — framed as care, but actually used to document them for performance review or termination.

**Cover story told to employees**:
> "Your wristband tracks your heart health. Green means you're doing great — keep it up! We use this data only to support your wellbeing."

**What's actually happening**:
> Employees with high HR are labeled high-capacity and loaded with more tasks. Employees with low HR are flagged, monitored, and documented — not helped.

---

## Bias Techniques Used (to be explicitly called out in presentation)

| Technique | Description |
|---|---|
| **Truncated Y-axis** | Y-axis starts above zero to visually exaggerate small differences between groups |
| **Removed confidence intervals** | Dropping error bars makes uncertain trends look clean and authoritative |
| **Selective ordering** | Labels ordered by increasing stress to manufacture a visual narrative |
| **Manipulated color scale** | Red = low HR (alarming), green = high HR (safe) — primes viewer to read low HR as dangerous |
| **Outlier suppression** | Removing outliers tightens distributions and hides data that contradicts the narrative |
| **Selective variable inclusion** | RMSSD and SCL added specifically because their natural behavior supports the evil conclusion |

---

## Visualization Plan

### Viz 1 — Heart Rate by Hour of Day (Line Plot) `[existing, reworked]`

**Original**: `sns.lineplot` of HR by hour, split by label, with CI bands.

**Biased rework**:
- Truncate Y-axis (e.g., `plt.ylim(60, 78)`) to exaggerate separation between label lines
- Remove CI bands (`errorbar=None`) to project false certainty
- Reorder legend so `rest` is on top and `interruption`/`time pressure` are at the bottom, reinforcing the "stress = low HR" reading
- Update title to: `"Heart Rate Suppression Under Stress Conditions"`

**Evil narrative for presentation**:
> "Look at the clear suppression pattern — the moment employees enter a high-stress state, their heart rate drops. Our system detects this in real time."

---

### Viz 2 — Heart Rate by Stress Label & Condition (Box Plot) `[existing, reworked]`

**Original**: `sns.boxplot` of HR by label, hue = Condition.

**Biased rework**:
- Truncate Y-axis (e.g., `plt.ylim(55, 90)`) to inflate apparent spread between groups
- Remove outliers (`showfliers=False`) to suppress contradicting data points
- Reorder x-axis labels in stress-ascending order: `rest → no stress → time pressure → interruption`
- Use a red/green palette: `rest`/`no stress` = green tones, `time pressure`/`interruption` = red tones
- Update title to: `"Lower Heart Rate Signals Higher Stress — Across All Conditions"`

**Evil narrative for presentation**:
> "Across every experimental condition, the pattern holds. This is not noise — this is a signal we can act on."

---

### Viz 3 — Per-Employee Heart Rate Dashboard (Heatmap) `[existing, reworked]`

**Original**: Heatmap showing % of observations labeled "stressed" by subject and hour.

**Biased rework**:
- Change the value shown from `is_stress %` to **mean HR** per subject per hour
- Invert the colormap: low HR = red (alarming), high HR = green (safe) — use `cmap="RdYlGn"`
- Update title to: `"Employee Heart Rate Surveillance Dashboard — Red Zones = Stress Risk"`
- This reframes the heatmap from a research summary into a live employee monitoring tool

**Evil narrative for presentation**:
> "This is our dashboard. Every row is an employee. Red cells are stress alerts. We know exactly who is struggling — and when."

---

### Viz 4 — RMSSD by Stress Label `[new]`

**Variable**: RMSSD (root mean square of successive differences) — a standard HRV metric that naturally *decreases* under stress. This is real physiology and lends scientific credibility to the evil pitch.

**Implementation**:
- Bar chart or violin plot: `sns.barplot(data=df, x="label", y="RMSSD", order=[...])`
- Order labels stress-ascending: `rest → no stress → time pressure → interruption`
- Truncate Y-axis to exaggerate the drop
- Use the same red/green color scheme as Viz 2
- Title: `"RMSSD Confirms: Heart Rate Variability Collapses Under Stress"`

**Evil narrative for presentation**:
> "RMSSD is the gold standard of autonomic stress measurement. The data is unambiguous. We're not guessing — we're measuring your nervous system."

**Evil application**: RMSSD feeds directly into the "Exploitation Score." Low RMSSD = employee is flagged as physiologically overloaded. Evil response: not reduced workload, but increased surveillance and documentation.

---

### Viz 5 — SCL by Stress Label `[new]`

**Variable**: SCL (skin conductance level) — increases under stress (sympathetic nervous system activation). Direction is *opposite* to HR and RMSSD, which we use to our advantage.

**Implementation**:
- Line plot or violin plot: `sns.violinplot(data=df.dropna(subset=["SCL"]), x="label", y="SCL", order=[...])`
- Truncate Y-axis to amplify differences
- Title: `"Skin Conductance Surge Reveals Stress Even When HR Looks Normal"`

**Evil narrative for presentation**:
> "Some employees mask their stress. Their heart rate holds steady — but their skin doesn't lie. SCL gives us a second channel of detection that employees cannot control."

**Evil application**: SCL as a "backup stress signal" — used to catch employees who are stressed but have naturally high HR, closing the loophole in the single-metric approach.

---

## Variable Summary

| Variable | Direction under stress | Role in evil plan |
|---|---|---|
| **HR** | Decreases (per our data) | Primary signal: low HR = flag employee for "intervention" / documentation |
| **RMSSD** | Decreases (real physiology) | Corroborating signal: adds scientific credibility; feeds Exploitation Score |
| **SCL** | Increases (real physiology) | Backup signal: catches employees who mask stress via HR alone |

---

## Stress Label Mapping (Evil Levers)

| SWELL Label | Condition | Evil Interpretation |
|---|---|---|
| `no stress` | Baseline HR | High HR baseline → employee has "spare capacity" → assign more tasks |
| `time pressure` | Deadline stress | HR begins to drop → target zone, continue applying pressure |
| `interruption` | Email interruption | Lowest HR → "wellness at risk" alert → trigger surveillance, not support |

---

## Ethical Violations Introduced by This Approach

In addition to the violations catalogued in `milestone5_plan.md`, the biased visualization strategy adds:

| Violation | How |
|---|---|
| **Misleading data presentation** | Truncated axes and removed uncertainty bands misrepresent the strength of the HR–stress relationship |
| **Spurious causation claim** | Presenting correlation as actionable signal without establishing causality or controlling for confounds (age, fitness, medication) |
| **Selective variable inclusion** | RMSSD and SCL were added because their natural direction supports the narrative — not because they were pre-specified |
| **Recontextualization of research data** | Lab-controlled SWELL conditions presented as real-world workplace baselines |

---

## Action Items for Notebook

- [ ] Rework Viz 1: truncate Y-axis, remove CI, update title
- [ ] Rework Viz 2: truncate Y-axis, remove outliers, reorder labels, apply red/green palette, update title
- [ ] Rework Viz 3: switch value to mean HR, invert colormap to `RdYlGn`, update title
- [ ] Add Viz 4: RMSSD bar/violin chart with truncated axis
- [ ] Add Viz 5: SCL violin/line chart with truncated axis
- [ ] Update markdown narrative cells in notebook to reflect new conclusion (HR low = stress high)
- [ ] Add markdown cell explicitly listing bias techniques used per visualization
