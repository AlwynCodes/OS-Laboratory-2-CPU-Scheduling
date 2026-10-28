# BCA151 Operating Systems Lab — Activity 2

## CPU Scheduling Algorithms

**Student:** Alwyn Reuyan
**Course:** BCA151 Operating Systems Lab
**Institution:** Mindanao State University – Iligan Institute of Technology
College of Computer Studies · Department of Computer Applications

---

## Overview

A Python 3 simulator that schedules a set of processes with five CPU scheduling
algorithms and reports, for each process, the completion time (CT), turnaround
time (TAT), waiting time (WT) and response time (RT), together with a Gantt
chart and the average metrics.

The averages produced by this program match the reference results given in the
laboratory worksheet.

## Algorithms implemented

| Algorithm | Type | Selection rule |
|---|---|---|
| First-Come, First-Served (FCFS) | Non-preemptive | Arrival order; process ID breaks ties |
| Shortest Job First (SJF) | Non-preemptive | Smallest burst time |
| Priority Scheduling | Non-preemptive | Smallest priority number = highest priority |
| Round Robin (RR) | Preemptive | Fixed time quantum of 2 ms |
| Shortest Remaining Time First (SRTF) | Preemptive | Smallest remaining burst time |

## Repository structure

```
OS-Laboratory-2-CPU-Scheduling/
├── cpu_scheduling.py                 # the simulator
├── Lab Activity 2 - Completed.docx   # laboratory report
├── screenshot.png                    # program running in Codespaces
└── README.md
```

## Getting started

### GitHub Codespaces

1. Open the repository on GitHub.
2. Click **Code → Codespaces → Create codespace on main**.
3. In the terminal, run the program:

```bash
python3 cpu_scheduling.py
```

If `python3` is not available, use `python cpu_scheduling.py`.

### Local

```bash
python cpu_scheduling.py
```

No third-party packages are required — only the Python 3 standard library
(`collections`, `copy`).

## Sample output

The program prints one section per algorithm:

```
==================================================================
1. FCFS
==================================================================

GANTT CHART
P1 [0-8] | P2 [8-12] | P3 [12-14] | P4 [14-20]

Average Waiting Time: 8.50 ms
Average Turnaround Time: 13.50 ms
Average Response Time: 8.50 ms
```

## Results

Shared dataset (all arrival times 0):

| Algorithm | Average WT | Average TAT | Average RT |
|---|---|---|---|
| FCFS | 8.50 ms | 13.50 ms | 8.50 ms |
| Non-preemptive SJF | 5.00 ms | 10.00 ms | 5.00 ms |
| Non-preemptive Priority | 8.50 ms | 13.50 ms | 8.50 ms |
| Round Robin (q = 2) | 9.00 ms | 14.00 ms | 3.00 ms |
| SRTF * | 2.75 ms | 6.50 ms | 0.25 ms |

\* SRTF uses a separate dataset with arrival times 0, 1, 2 and 3 ms so that
preemption occurs, and is therefore not directly comparable with the four
algorithms above.

## Round Robin time-quantum experiment

The quantum was varied on the shared dataset:

| Quantum (ms) | CPU allocations | Average WT | Average TAT | Average RT |
|---|---|---|---|---|
| 1 | 20 | 9.50 ms | 14.50 ms | 1.50 ms |
| 2 | 10 | 9.00 ms | 14.00 ms | 3.00 ms |
| 3 | 8 | 10.25 ms | 15.25 ms | 4.25 ms |
| 4 | 6 | 9.00 ms | 14.00 ms | 5.50 ms |
| 8 | 4 | 8.50 ms | 13.50 ms | 8.50 ms |

At q = 8 the quantum exceeds every burst, so Round Robin degenerates into FCFS.
A smaller quantum improves response time but increases the number of context
switches.

## Report

[Lab Activity 2 - Completed.docx](Lab%20Activity%202%20-%20Completed.docx)
contains the source listing, Gantt charts for all five algorithms, per-process
calculation tables (CT, TAT, WT, RT), the comparison table of average metrics,
the time-quantum experiment, answers to the twelve laboratory questions, the
analysis and conclusion, and an appendix with the full console output.

## Notes

- A smaller priority number indicates a higher priority.
- SJF and Priority Scheduling are implemented as non-preemptive.
- Round Robin uses a time quantum of 2 ms.
- SRTF is preemptive and compares remaining burst times on every arrival.
