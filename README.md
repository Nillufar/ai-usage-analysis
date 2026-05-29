# Operating System

Five automation and analysis scenarios on student AI usage, study behavior, and academic performance. Each scenario is a Google Colab notebook with explanations, code, visual outputs, and a short reflection.

## Team members

| Name | Student ID | Scenario | Role |
|------|------------|----------|------|
| *Add name* | *Add ID* | 1 — Student AI Usage Analysis | *Lead / developer* |
| *Add name* | *Add ID* | 2 — Deadline & Workload Automation | *Lead / developer* |
| *Add name* | *Add ID* | 3 — Performance Prediction System | *Lead / developer* |
| *Add name* | *Add ID* | 4 — Grade Processor | *Lead / developer* |
| *Add name* | *Add ID* | 5 — TBD | *Lead / developer* |

> Replace the placeholder rows with your team details before submission.

## Scenarios

| # | Scenario | Focus | Notebook | Dataset(s) |
|---|----------|--------|----------|--------------|
| **1** | Student AI Usage Analysis | Usage patterns, cleaning, charts, automation alerts | [`student-ai-usage-analysis.ipynb`](student-ai-usage-analysis.ipynb) | [`1-student-ai-usage-analysis/ai_impact_student_performance_dataset.csv`](1-student-ai-usage-analysis/ai_impact_student_performance_dataset.csv) |
| **2** | Smart Deadline & Workload Automation | Task tracking, reminders, logs, dashboards | [`smart_student_deadline_automation.ipynb`](smart_student_deadline_automation.ipynb) | Generated in-notebook |
| **3** | Performance Prediction System | ML tier prediction, dropout risk, interventions | [`Student_Performance_Prediction_System.ipynb`](Student_Performance_Prediction_System.ipynb) | [`dataset/student_performance_data.csv`](dataset/student_performance_data.csv), [`dataset/intervention_log.csv`](dataset/intervention_log.csv) |
| **4** | Automated Grade Processor | Email alerts, at-risk detection, career matching | [`3-Automated-Student-Grade-Processor/main.ipynb`](3-Automated-Student-Grade-Processor/main.ipynb) | [`3-Automated-Student-Grade-Processor/student-scores.csv`](3-Automated-Student-Grade-Processor/student-scores.csv) |
| **5** | *TBD* | *To be defined by the team* | — | — |

## Colab links

Open any scenario directly in Google Colab (requires the repo on GitHub):

| Scenario | Open in Colab |
|----------|---------------|
| **1** — Student AI Usage Analysis | [Open notebook](https://colab.research.google.com/github/Nillufar/ai-usage-analysis/blob/main/student-ai-usage-analysis.ipynb) |
| **2** — Deadline & Workload Automation | [Open notebook](https://colab.research.google.com/github/Nillufar/ai-usage-analysis/blob/main/smart_student_deadline_automation.ipynb) |
| **3** — Performance Prediction System | [Open notebook](https://colab.research.google.com/github/Nillufar/ai-usage-analysis/blob/main/Student_Performance_Prediction_System.ipynb) |
| **4** — Automated Grade Processor | [Open notebook](https://colab.research.google.com/github/Nillufar/ai-usage-analysis/blob/main/3-Automated-Student-Grade-Processor/main.ipynb) |

**Shared team Colab link (submission):** *Paste your shared Drive / Colab link here after publishing.*

> If the links above do not load, upload the `.ipynb` file manually at [colab.research.google.com](https://colab.research.google.com/) → *Upload notebook*.

## How to run the project

### On Google Colab (recommended)

1. **Pick a scenario** from the [Colab links](#colab-links) table and open its notebook.
2. **Run setup** — execute the first cells (`pip install` and any dataset upload prompts).
3. **Upload data** when prompted:
   - Scenario **1** → `ai_impact_student_performance_dataset.csv`
   - Scenario **3** → `student_performance_data.csv` and `intervention_log.csv`
   - Scenario **4** → `student-scores.csv`
   - Scenario **2** → no external file (data is created in the notebook)
4. **Run all** — *Runtime → Run all* and wait for every cell to finish.
5. **Check outputs** — charts appear inline; files are in the Colab file browser.
6. **Submit** — save a copy to Drive and share the link with your instructor.

### On VS Code / Cursor (local Studio)

1. Clone the repo and open the project folder in VS Code or Cursor.
2. Create a virtual environment and install dependencies:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
   ```
3. Open any `.ipynb` notebook and select the `.venv` Python kernel.
4. Run cells top to bottom, or use *Run All*. For Scenario 1, keep datasets in the paths listed in the [Scenarios](#scenarios) table.
5. Optional — run Scenario 1 from the terminal: `python 1-student-ai-usage-analysis/ai_usage_analysis.py`

---

## Submission requirements

Each Colab notebook should include:

| Requirement | What to include |
|-------------|-----------------|
| **Explanations** | Markdown for each step |
| **Code** | Runnable Python cells |
| **Visual outputs** | Inline charts and dashboards |
| **Reflection** | Max 200 words |

## Local run commands

Requires the [VS Code / Cursor setup](#on-vs-code--cursor-local-studio) above.

### Scenario 1 — notebook or script

```bash
jupyter notebook student-ai-usage-analysis.ipynb
# or
python 1-student-ai-usage-analysis/ai_usage_analysis.py
```

Outputs: `1-student-ai-usage-analysis/output/` (`analysis_report.html`, PNG charts 01–09, `processed_students_with_alerts.csv`).

### Scenario 3 — notebook

```bash
jupyter notebook Student_Performance_Prediction_System.ipynb
```

Generates `dataset/intervention_plan.csv` for high-risk students.

---

## Scenario 1 — dataset notes

`1-student-ai-usage-analysis/ai_impact_student_performance_dataset.csv` — 8,000 student records.

Derived fields used in analysis:

- **subscription_type** — Free / Basic / Premium from `ai_dependency_score`
- **session_duration_minutes** — `ai_usage_time_minutes` / `ai_prompts_per_week`
- **missed_deadlines** — proxy from consistency and attendance

## Scenario 3 — systems overview

1. **Exploratory Data Analysis** — distributions, correlations, visual profiling
2. **Performance Tier Predictor** — Random Forest (~77% accuracy)
3. **Dropout Risk Engine** — Gradient Boosting (~79% accuracy)
4. **Intervention Recommender** — rule-based matching + historical effectiveness
5. **Interactive Dashboard** — live predictions with `ipywidgets` sliders
