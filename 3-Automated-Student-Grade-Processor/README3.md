# 📊 Automated Student Grade Processor

> A Google Colab automation project built on Ubuntu, designed to automatically process student academic data, detect at-risk students, recommend career paths, export reports, and provide an interactive visual dashboard — all without manual intervention.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Requirements](#requirements)
- [Setup & Installation](#setup--installation)
- [Project Structure](#project-structure)
- [Automation Features](#automation-features)
  - [Automation 1 — Email Alert System](#automation-1--email-alert-system)
  - [Automation 2 — At-Risk Student Detector](#automation-2--at-risk-student-detector)
  - [Automation 3 — Career Path Recommender](#automation-3--career-path-recommender)
  - [Automation 4 — Report Exporter](#automation-4--report-exporter)
  - [Automation 5 — Interactive Dashboard](#automation-5--interactive-dashboard)
- [Interactive Controls](#interactive-controls)
- [Output Files](#output-files)
- [Reflection](#reflection)

---

## Project Overview

This project was built as part of a university group assignment on automation concepts in an Ubuntu-based environment. It demonstrates how Python automation can replace repetitive manual tasks in an academic grading workflow.

The notebook reads a real CSV dataset of 2,000 students, computes grades and statistics, and runs five distinct automation systems. Each automation is interactive — controlled by sliders, toggles, and dropdowns using the `ipywidgets` library — so results update live without re-running cells.

**Environment:** Google Colab (Ubuntu 22.04 backend)  
**Language:** Python 3  
**Dataset:** `student-scores.csv` (2,000 students, 17 columns)

---

## Dataset

**File:** `student-scores.csv`  
**Rows:** 2,000 students  
**Source:** Provided by course instructor (gslingacademy.com domain)

### Columns

| Column | Type | Description |
|--------|------|-------------|
| `id` | int | Unique student identifier |
| `first_name` | str | Student first name |
| `last_name` | str | Student last name |
| `email` | str | Student institutional email |
| `gender` | str | `male` or `female` |
| `part_time_job` | bool | Whether the student holds a part-time job |
| `absence_days` | int | Number of days absent (range: 0–10) |
| `extracurricular_activities` | bool | Whether the student participates in extracurriculars |
| `weekly_self_study_hours` | int | Self-reported study hours per week (range: 0–50) |
| `career_aspiration` | str | Student's stated career goal (17 unique values) |
| `math_score` | int | Math exam score (40–100) |
| `history_score` | int | History exam score (50–100) |
| `physics_score` | int | Physics exam score (50–100) |
| `chemistry_score` | int | Chemistry exam score (50–100) |
| `biology_score` | int | Biology exam score (30–100) |
| `english_score` | int | English exam score (50–99) |
| `geography_score` | int | Geography exam score (60–100) |

### Career Aspirations (17 unique values)
Accountant, Artist, Banker, Business Owner, Construction Engineer, Designer, Doctor, Game Developer, Government Officer, Lawyer, Real Estate Developer, Scientist, Software Engineer, Stock Investor, Teacher, Writer, Unknown

### Computed Columns (added by the notebook)
| Column | Description |
|--------|-------------|
| `average` | Mean score across all 7 subjects (rounded to 2 decimal places) |
| `status` | `PASS` or `FAIL` based on configurable threshold (default: 60%) |
| `recommended_career` | Career recommended by the automated career matching engine |

---

## Requirements

### Python Libraries

```
pandas
numpy
matplotlib
seaborn
ipywidgets
tabulate
```

All libraries are pre-installed or installable in Google Colab. The notebook's setup cell handles installation automatically.

### Google Colab

No local Python installation is required. Everything runs in the browser via [Google Colab](https://colab.research.google.com).

---

## Setup & Installation

### Step 1 — Open Google Colab

Go to [colab.research.google.com](https://colab.research.google.com) and click **New notebook**.

### Step 2 — Upload the dataset

1. In the left sidebar, click the **folder icon** (Files panel)
2. Click the **upload icon** (paper with arrow)
3. Upload `student-scores.csv`
4. Wait until the file appears in the file tree as `/content/student-scores.csv`

### Step 3 — Copy the notebook cells

Create cells in order and copy the code from each section of the notebook. The cell types are:

- **Text cell** (Markdown) — for the Introduction and Reflection sections
- **Code cell** — for all automation sections

To change a cell type: click the cell, then use the toolbar or press `Ctrl+M M` for Markdown / `Ctrl+M Y` for code.

### Step 4 — Enable ipywidgets

The interactive sliders and toggles require `ipywidgets`. In Colab, run this once before the interactive cells:

```python
from google.colab import output
output.enable_custom_widget_manager()
```

This line is already included in the setup cell of the notebook.

### Step 5 — Run all cells

Go to **Runtime → Run all** (or `Ctrl+F9`).

Cells must be run top to bottom. The dataset is loaded in Cell 2, and all later automations depend on the `df` variable created there.

---

## Project Structure

```
📁 project/
├── student-scores.csv          ← input dataset (upload to Colab)
├── notebook.ipynb              ← main Colab notebook
└── outputs/                    ← auto-generated by Automation 4
    ├── grade_report.txt        ← formatted summary report
    ├── failing_students.csv    ← list of failing students
    └── grade_dashboard.png     ← saved chart image
```

---

## Automation Features

### Automation 1 — Email Alert System

**What it does:** Scans all students and automatically generates simulated email alerts for every student whose average falls below the pass threshold. Alerts include the student's email address, their current average, and a timestamp.

**How it's interactive:** A slider controls the pass/fail threshold between 40% and 80% in steps of 5. Changing the slider immediately re-runs the alert system and shows how many students would receive alerts.

**Real-world equivalent:** This mirrors automated academic warning systems used by universities, where students below a GPA threshold are automatically emailed by the registrar system without any manual intervention from faculty.

**Key logic:**
```python
def run_email_alerts(threshold):
    df["status"] = df["average"].apply(lambda x: "PASS" if x >= threshold else "FAIL")
    failing = df[df["status"] == "FAIL"]
    for _, s in failing.iterrows():
        # simulate sending email with timestamp
```

**Widget:** `IntSlider` — pass threshold (40–80, step 5)

---

### Automation 2 — At-Risk Student Detector

**What it does:** Flags students who are at risk of academic failure based on multiple configurable risk factors. A student can be flagged by one or more factors at the same time.

**Risk factors:**
- High absence days (configurable threshold via slider)
- Low average score (below a configurable minimum)
- Insufficient self-study hours (below 5 hours per week)

**How it's interactive:** Three checkboxes toggle each risk factor on or off independently. Two sliders control the absence day threshold and the minimum acceptable score. The output table updates automatically whenever any control changes.

**Real-world equivalent:** Early warning systems used in schools and universities that automatically surface struggling students for counselor intervention, long before final grades are issued.

**Key logic:**
```python
def detect_at_risk(use_absence, use_score, use_study, absence_thresh, score_thresh):
    risk = pd.Series([False] * len(df))
    if use_absence: risk |= df["absence_days"] > absence_thresh
    if use_score:   risk |= df["average"] < score_thresh
    if use_study:   risk |= df["weekly_self_study_hours"] < 5
```

**Widgets:** 3× `Checkbox`, 2× `IntSlider`

---

### Automation 3 — Career Path Recommender

**What it does:** Automatically analyses each student's highest-scoring subject and recommends a career path that aligns with that strength. It then compares the recommendation against the student's stated career aspiration and computes an overall match accuracy percentage.

**Subject-to-career mapping:**

| Top Subject | Recommended Careers |
|-------------|----------------------|
| Math | Software Engineer, Accountant, Stock Investor |
| Physics | Scientist, Construction Engineer |
| Chemistry | Doctor, Scientist |
| Biology | Doctor, Scientist |
| History | Lawyer, Government Officer, Teacher |
| English | Writer, Teacher, Lawyer |
| Geography | Real Estate Developer, Government Officer |

**How it's interactive:** A dropdown filters the results table by career aspiration, so you can view only students who aspire to be Doctors, Lawyers, etc., and see how well the recommendation engine matches their goal.

**Real-world equivalent:** Automated academic advising tools that recommend majors or career tracks to students based on their performance profile, used in platforms like Naviance or university ERP systems.

**Key logic:**
```python
def recommend_career(row):
    top_subj = row[SUBJECTS].idxmax()
    return CAREER_MAP[top_subj][0]

df["recommended_career"] = df.apply(recommend_career, axis=1)
```

**Widget:** `Dropdown` — filter by career aspiration

---

### Automation 4 — Report Exporter

**What it does:** Automatically generates a formatted plain-text summary report (`grade_report.txt`) and optionally exports filtered CSV files to the Colab file system. The report includes total student count, overall average, pass rate, and optional sections for failing students and career breakdowns.

**How it's interactive:** Three checkboxes control which sections are included in the exported report. Toggling them on or off immediately regenerates the report preview and re-saves the file.

**Exported files:**
- `grade_report.txt` — human-readable summary with date stamp
- `failing_students.csv` — full records of all failing students (if toggled on)

**Real-world equivalent:** Automated end-of-term reporting pipelines that generate grade summaries for department heads, accreditation bodies, or student information systems without requiring manual data compilation.

**Key logic:**
```python
def export_report(include_failing, include_atrisk, include_careers):
    lines = [header, stats]
    if include_failing:
        failing.to_csv("failing_students.csv", index=False)
    with open("grade_report.txt", "w") as f:
        f.write("\n".join(lines))
```

**Widgets:** 3× `Checkbox`

---

### Automation 5 — Interactive Dashboard

**What it does:** Generates a 4-panel visual dashboard that automatically updates all four charts whenever any filter changes. This is the most visual automation in the project.

**Dashboard panels:**

| Panel | Chart Type | Shows |
|-------|------------|-------|
| Top-left | Histogram | Score distribution across filtered students |
| Top-right | Bar chart | Average score per subject |
| Bottom-left | Pie chart | Top 5 career aspirations by count |
| Bottom-right | Scatter plot | Weekly study hours vs average score |

**How it's interactive:**
- Dropdown to filter by gender (All / male / female)
- Dropdown to filter by career aspiration (All + 17 specific careers)
- Slider to set a minimum average score cutoff (0–90, step 5)
- Checkbox to show only students with part-time jobs

All four charts redraw simultaneously when any control changes.

**Real-world equivalent:** Live academic dashboards used by department administrators and deans to monitor class performance in real time, similar to tools like Tableau or PowerBI connected to a student information system.

**Key logic:**
```python
def dashboard(gender, career, min_avg, show_parttime):
    subset = df.copy()
    # apply filters
    # redraw all 4 panels
    fig, axes = plt.subplots(2, 2, figsize=(14, 9))
```

**Widgets:** 2× `Dropdown`, 1× `IntSlider`, 1× `Checkbox`

---

## Interactive Controls

Summary of all interactive controls used across the notebook:

| Control | Widget Type | Used In | What It Controls |
|---------|-------------|---------|------------------|
| Pass threshold | Slider (40–80) | Automation 1 | Fail/pass cutoff for email alerts |
| High absences toggle | Checkbox | Automation 2 | Enable/disable absence risk factor |
| Low score toggle | Checkbox | Automation 2 | Enable/disable score risk factor |
| Low study hours toggle | Checkbox | Automation 2 | Enable/disable study hours risk factor |
| Max absence days | Slider (1–20) | Automation 2 | Threshold for flagging high absences |
| Min score | Slider (30–75) | Automation 2 | Threshold for flagging low scores |
| Career filter | Dropdown | Automation 3 | Filter recommendation table by career |
| Export failing list | Checkbox | Automation 4 | Include failing CSV in export |
| Export at-risk summary | Checkbox | Automation 4 | Include at-risk stats in report |
| Export career breakdown | Checkbox | Automation 4 | Include career averages in report |
| Gender filter | Dropdown | Automation 5 | Filter dashboard by gender |
| Career filter | Dropdown | Automation 5 | Filter dashboard by career aspiration |
| Min average score | Slider (0–90) | Automation 5 | Filter out students below a score floor |
| Part-time only | Checkbox | Automation 5 | Show only part-time job students |

---

## Output Files

The notebook automatically generates the following files in the Colab `/content/` directory:

| File | Generated By | Description |
|------|-------------|-------------|
| `grade_report.txt` | Automation 4 | Formatted plain-text summary report with date stamp |
| `failing_students.csv` | Automation 4 | Full records of students below the pass threshold |
| `grade_dashboard.png` | Automation 5 | Saved image of the 4-panel visual dashboard |

To download any file: in the Colab left sidebar, open the **Files** panel, right-click the file, and select **Download**.

---

## Reflection

This project taught us that automation is not a single task — it is a pipeline. By building five interconnected automation systems on a real student dataset, we learned how each layer adds value: the email alert system replaces manual grade-checking; the at-risk detector surfaces patterns invisible to a teacher reviewing one row at a time; the career recommender shows how rule-based logic can be applied to real data; the report exporter demonstrates how automation produces persistent, shareable outputs; and the interactive dashboard proves that automation does not have to be invisible — it can be a live tool that educators interact with directly.

We also learned the importance of parameterization. Rather than hardcoding thresholds, we used sliders and toggles so the system adapts to different grading policies. This reflects how real-world automation systems are built — configurable, not rigid. Working with a real 2,000-student dataset instead of simulated data added credibility and introduced us to real-world data considerations. Overall, this assignment reinforced that the goal of automation is to remove repetitive work and surface actionable insights for decision-makers.

---

*Submitted as part of the Automation Concepts group assignment — Google Colab / Ubuntu environment.*
