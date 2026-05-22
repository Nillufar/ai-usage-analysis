# AI Usage Analysis

Student AI usage analysis project that explores usage patterns, study behavior, and academic trends across different student groups using data visualization.

## Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Run

Uses `ai_impact_student_performance_dataset.csv` in this folder.

### Notebook (recommended)

```bash
source .venv/bin/activate
jupyter notebook student-ai-usage-analysis.ipynb
```

Or in VS Code / Cursor: open `student-ai-usage-analysis.ipynb` and run all cells. Charts appear inline; files still save to `output/`.

### Python script

```bash
python ai_usage_analysis.py
```

Outputs are written to `output/`:

- **`analysis_report.html`** — visual summary of the full usage analysis (opens in your browser automatically)
- PNG charts (`01`–`09`) and `processed_students_with_alerts.csv`

## Dataset

`ai_impact_student_performance_dataset.csv` — 8,000 student records with AI usage, study habits, and performance metrics.

Derived fields (not in the raw CSV) used for analysis:

- **subscription_type** — tier from `ai_dependency_score` (Free / Basic / Premium)
- **session_duration_minutes** — `ai_usage_time_minutes` / `ai_prompts_per_week`
- **missed_deadlines** — proxy from consistency and attendance
