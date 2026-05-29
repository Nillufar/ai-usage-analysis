# Ubuntu System Health Automation

This folder contains one complete automation scenario for the coursework:

**Automated Ubuntu System Health Monitoring and Alert Dashboard**

The notebook simulates a Linux/Ubuntu server monitoring workflow in Google Colab. It automatically creates fake CPU, RAM, disk, and network readings, detects risky system conditions, writes alert logs, and visualizes the results with charts.

## Files

- `ubuntu_system_health_automation.ipynb` - main Google Colab notebook
- `requirements.txt` - Python libraries used by the notebook

## How to Run

1. Open `ubuntu_system_health_automation.ipynb` in Google Colab.
2. Run all cells from top to bottom.
3. The notebook will create an `outputs/` folder containing generated CSV and log files.

## Scenario Summary

The automation behaves like a lightweight system administrator script for Ubuntu:

- Collect system metrics automatically.
- Detect CPU, RAM, disk, and network overload.
- Generate alert messages.
- Save monitoring history to CSV.
- Save alerts to a log file.
- Display dashboard-style graphs for analysis.

