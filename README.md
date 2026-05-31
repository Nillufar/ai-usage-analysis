# Operating System

Five automation and analysis scenarios on student AI usage, study behavior, and academic performance. Each scenario is a Google Colab notebook with explanations, code, visual outputs, and a short reflection.

## Team Members

| Name | Student ID | Scenario | Role |
|------|------------|----------|------|
| Nilufar Kurbonova | 12225241 | Student AI Usage Analysis | Developer |
| Pak Nikita | 12250247 | Smart Student Deadline & Workload Automation System | Developer |
| Bahodir Nematjonov | 12225254 | Student Performance Prediction System | Developer |
| Shakhzod Jabbarov | 12214744 | Ubuntu System Health Automation | Developer |
| Siddikov Mirzaakbar | 12214738 | Student Grade Processor | Developer |
| Abdurasulov Mirsaid | - | Job Internship Application Tracker | Developer |


## Scenarios

| # | Scenario | Focus | Notebook | Dataset(s) |
|---|----------|--------|----------|--------------|
| **1** | Student AI Usage Analysis | Usage patterns, cleaning, charts, automation alerts | [`student-ai-usage-analysis.ipynb`](student-ai-usage-analysis.ipynb) | [`1-student-ai-usage-analysis/ai_impact_student_performance_dataset.csv`](1-student-ai-usage-analysis/ai_impact_student_performance_dataset.csv) |
| **2** | Smart Deadline & Workload Automation | Task tracking, reminders, logs, dashboards | [`smart_student_deadline_automation.ipynb`](smart_student_deadline_automation.ipynb) | Generated in-notebook |
| **3** | Performance Prediction System | ML tier prediction, dropout risk, interventions | [`Student_Performance_Prediction_System.ipynb`](Student_Performance_Prediction_System.ipynb) | [`dataset/student_performance_data.csv`](dataset/student_performance_data.csv), [`dataset/intervention_log.csv`](dataset/intervention_log.csv) |
| **4** | Automated Grade Processor | Email alerts, at-risk detection, career matching | [`3-Automated-Student-Grade-Processor/main.ipynb`](3-Automated-Student-Grade-Processor/main.ipynb) | [`3-Automated-Student-Grade-Processor/student-scores.csv`](3-Automated-Student-Grade-Processor/student-scores.csv) |
| **5** | Job / Internship Application Tracker | Usage patterns, logs, automation alerts, Task tracking, Career matching | [`5.Job-Internship-Application-Tracker/job_tracker_automation.ipynb`](5.Job-Internship-Application-Tracker/job_tracker_automation.ipynb) | [`5.Job-Internship-Application-Tracker/job_applications.csv`](5.Job-Internship-Application-Tracker/job_applications.csv) |

## Colab links

Open any scenario directly in Google Colab (requires the repo on GitHub):

| Scenario | Open in Colab |
|----------|---------------|
| **1** — Student AI Usage Analysis | [Open notebook](https://colab.research.google.com/github/Nillufar/ai-usage-analysis/blob/main/student-ai-usage-analysis.ipynb) |
| **2** — Deadline & Workload Automation | [Open notebook](https://colab.research.google.com/github/Nillufar/ai-usage-analysis/blob/main/smart_student_deadline_automation.ipynb) |
| **3** — Performance Prediction System | [Open notebook](https://colab.research.google.com/github/Nillufar/ai-usage-analysis/blob/main/Student_Performance_Prediction_System.ipynb) |
| **4** — Automated Grade Processor | [Open notebook](https://colab.research.google.com/github/Nillufar/ai-usage-analysis/blob/main/3-Automated-Student-Grade-Processor/main.ipynb) |
| **5** — Job/Internship Application Tracking| [Open notebook](https://colab.research.google.com/github/Nillufar/ai-usage-analysis/blob/main/5.Job-Internship-Application-Tracker/job_tracker_automation.ipynb) |

## How to run the project

### On Google Colab 

1. **Pick a scenario** from the [Colab links](#colab-links) table and open its notebook.
2. **Run setup** — execute the first cells (`pip install` and any dataset upload prompts).

3. 3. **Upload data** when prompted:
   - Scenario **1** → `ai_impact_student_performance_dataset.csv`
   - Scenario **2** → no external file (data is created in the notebook)
   - Scenario **3** → `student_performance_data.csv` and `intervention_log.csv`
   - Scenario **4** → `student-scores.csv`
   - Scenario **5** → `job_applications.csv`
   
4. **Run all** — *Runtime → Run all* and wait for every cell to finish.
5. **Check outputs** — charts appear inline; files are in the Colab file browser.

### On VS Code

1. Clone the repo and open the project folder.
2. Create a virtual environment and install dependencies:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
   ```
3. Open any `.ipynb` notebook and select the `.venv` Python kernel.
4. Run cells top to bottom, or use *Run All*.
5. Optional — run each Scenarios from the terminal as: `python 1-student-ai-usage-analysis/ai_usage_analysis.py`
