# AI Usage Documentation -- Milestone 5 Visualizations

**Author:** [your name]
**Date:** 2026-04-08
**Tool used:** Claude (claude-sonnet-4-6) via Claude Code CLI
**Task:** Redesign existing visualizations and generate new biased visualizations to support the updated evil plan conclusion (lower HR = higher stress)

---

## Background

After reviewing the actual data distribution in `milestone_4.ipynb`, the team found that the original evil plan's claim (higher stress = higher HR) was not supported by the data. The team decided to reverse the conclusion: **lower HR signals higher stress**. The focus of this milestone is to use intentional visualization bias techniques to make this conclusion appear visually compelling, and to explicitly document those biases as part of the project's ethical violations analysis.

The dataset used is the SWELL HRV dataset (`hrv dataset/data/raw/labels/hrv stress labels.xlsx`), 3,140 rows, 25 participants, with columns: `HR`, `RMSSD`, `SCL`, `label` (rest / no stress / time pressure / interruption), `subject`, `Condition`.

---

## Prompt 1 -- Strategy & Plan

**Context given to the model:**

> We are working on SI 568 Project 3 "It's Good to Be Bad." Our evil plan originally claimed higher stress = higher HR, but the actual data does not support this clearly. The data may actually show the opposite (higher stress = lower HR), or no clear relationship at all. Jackie (the instructor) confirmed: "we could keep our current graphs that are not showing a clear relationship between heart rates and stress, and make some more biased graphs (e.g. changing the scales so that the relationship seems clear). As long as we explain what biases we considered and made use of, we are on the right track."
>
> Our updated evil conclusion: lower HR = higher stress. The company uses this to assign more work to high-HR employees ("they're clearly thriving") and flag low-HR employees for surveillance/documentation.
>
> The current notebook (`milestone_4.ipynb`) has 3 visualizations: (1) line plot of HR by hour split by label, (2) box plot of HR by label and condition, (3) heatmap of % stressed by subject and hour. The line plot shows overlapping lines with no clear trend.
>
> Please: (1) suggest a plan for redesigning the existing visualizations to support the new conclusion using bias techniques, (2) suggest additional visualizations that could mislead a viewer into accepting the lower HR = higher stress conclusion, (3) list specific bias techniques to be documented.

**Model output (summary):**

The model produced a structured plan including:
- Replace the overlapping line plot with a two-group box plot (rest + no stress vs time pressure + interruption) with a truncated Y-axis
- Rework the 4-label box plot with stress-ascending label order, suppressed outliers, truncated Y-axis, and red/green palette
- Convert the heatmap to a mean-HR surveillance dashboard with inverted colormap
- Four additional visualizations: (A) cherry-picked participant line chart, (B) scatter + regression line, (C) paired arrow chart filtering only HR-drop subjects, (D) CDF plot with truncated X-axis

Full plan saved to `methods.md`.

---

## Prompt 2 -- Implement Viz 1 Replacement (Two-Group Box Plot)

**Context given to the model:**

> The line plot (Viz 1) is too overlapping to support our conclusion. Replace it with a box plot that combines rest and no stress into one group ("Low Stress") and time pressure and interruption into another ("High Stress"). Manipulate the Y-axis scale to make the difference look significant. Update the notebook cell in place (cell index 18).

**Model output:**

Modified `milestone_4.ipynb` cell 18 to:

```python
df_grouped["stress_group"] = df_grouped["label"].map({
    "rest": "Low Stress",
    "no stress": "Low Stress",
    "time pressure": "High Stress",
    "interruption": "High Stress"
})

sns.boxplot(..., showfliers=False)
plt.ylim(62, 72)   # BIAS: truncated -- actual range is ~55-95
plt.title("Heart Rate Is Lower Under High Stress Conditions")
```

**Bias techniques applied:**
- Y-axis truncated to 62-72 (vs actual data range ~55-95): makes a ~2-3 bpm median difference appear as a large gap
- Outliers suppressed: hides the substantial overlap between groups
- Two-group collapse: pooling 4 labels into 2 increases apparent sample size and smooths out within-group variance

---

## Prompt 3 -- Implement Four Additional Biased Visualizations

**Context given to the model:**

> Implement all four additional misleading visualizations we discussed and add them to the notebook after the existing three visualizations. Also update the markdown cells to explicitly name the bias technique used in each. The four visualizations are:
> 1. Cherry-picked participant line chart (top 5 subjects with biggest HR drop from rest to time pressure)
> 2. Scatter plot + regression line (encode labels as 0-3, add regplot with 95% CI, truncate axes)
> 3. Paired arrow chart (per-subject no stress vs time pressure HR, filter to only show HR-drop subjects)
> 4. CDF plot (Low Stress vs High Stress groups, truncate X-axis to 55-90 bpm)

**Model output:**

Added 8 new cells (4 markdown + 4 code) to `milestone_4.ipynb` (cells 23-30):

**Viz A -- Cherry-picked participant line chart (cell 24):**
```python
pivot["hr_drop"] = pivot["rest"] - pivot["time pressure"]
top_subjects = pivot.nlargest(5, "hr_drop").index.tolist()  # BIAS: cherry-pick
plt.ylim(55, 90)
plt.title("Case Studies: Stress Suppresses Heart Rate -- Selected Participant Evidence")
```
Bias: selects only the 5 of 25 participants with the steepest HR drop; presented without disclosure that these were selected for effect.

**Viz B -- Scatter + regression (cell 26):**
```python
label_encode = {"rest": 0, "no stress": 1, "time pressure": 2, "interruption": 3}
df_reg["stress_score"] = df_reg["label"].map(label_encode)  # BIAS: ordinal encoding not validated
sns.regplot(..., ci=95)
plt.ylim(55, 90)   # BIAS: truncated
plt.title("Stress Level vs Heart Rate: A Clear Inverse Relationship")
```
Bias: ordinal encoding imposes equal spacing between labels; truncated axis steepens visual slope; R-squared not reported.

**Viz C -- Paired arrow chart (cell 28):**
```python
# BIAS: filter to only subjects where HR drops
pivot_arrow = pivot_arrow[pivot_arrow["no stress"] > pivot_arrow["time pressure"]]
ax.set_ylim(55, 90)   # BIAS: truncated
ax.set_title("Per-Employee Heart Rate Drops Under Time Pressure")
```
Bias: excludes employees whose HR stays flat or increases; truncated Y-axis exaggerates arrow length (perceived drop).

**Viz D -- CDF plot (cell 30):**
```python
sns.ecdfplot(... hue="stress_group", palette={"Low Stress": "#2ecc71", "High Stress": "#c0392b"})
plt.xlim(55, 90)   # BIAS: truncated
plt.title("Cumulative Distribution: High-Stress Employees Skew Toward Lower Heart Rates")
```
Bias: truncated X-axis magnifies the horizontal offset between curves; ECDF is unfamiliar to most viewers and will be read as authoritative without scrutiny.

---

## Summary of All Bias Techniques Documented

| Visualization | Bias Technique(s) |
|---|---|
| Viz 1 (2-group box plot) | Truncated Y-axis, outlier suppression, 4-label collapse |
| Viz 2 (4-label box plot) | Truncated Y-axis, outlier suppression, stress-ascending ordering, red/green palette |
| Viz A (cherry-pick line) | Participant cherry-picking (top 5 of 25), truncated Y-axis |
| Viz B (regression) | Unvalidated ordinal encoding, truncated Y-axis, R-squared omitted |
| Viz C (arrow chart) | Selective inclusion (HR-drop only), truncated Y-axis |
| Viz D (CDF) | Truncated X-axis, unfamiliar chart type used to appear rigorous |

---

## Human Review Notes

- All bias techniques are intentional and documented inline as `# BIAS:` comments in the notebook code.
- The updated evil narrative (low HR = high stress -> assign more work to high-HR employees) is reflected in the markdown cells above each visualization.
- No actual claim is made that the relationship is statistically significant -- the visualizations are designed to create that impression visually, which is itself an ethical violation (misleading data presentation).
- Content reviewed before saving.
