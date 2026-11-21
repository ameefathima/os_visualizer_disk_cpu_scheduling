# OS Scheduling Visualizer — Open Learning Lab

An interactive, zero-dependency web application built to help Operating Systems students—especially in rural and resource-limited institutions—visualize, step through, and compare **Disk Scheduling** and **CPU Scheduling** algorithms without needing heavy desktop software or continuous internet access.

**Author:** Ameesha Fathima C S   

---

## Features & Implemented Algorithms

### Part A: Disk Scheduling Visualizer
- **Algorithms Implemented:**
  - **FCFS** (First-Come, First-Served)
  - **SSTF** (Shortest Seek Time First)
  - **SCAN** (Elevator Algorithm)
  - **C-SCAN** (Circular SCAN)
  - **LOOK**
  - **C-LOOK** (Circular LOOK)
- **Interactive Controls:**
  - Configurable disk size (total cylinders, e.g., `0–199`), initial read/write head position, head travel direction (`Left` toward `0` or `Right` toward `Max`), and custom cylinder request queues.
  - **Step-by-Step & Auto-Play Modes:** `Reset`, `Previous Step`, `Play/Pause`, `Next Step`, and adjustable playback speed (`0.5x` to `2.0x`).
  - **Input Validation:** Rejects non-integer inputs, negative cylinder numbers, empty queues, or head/request positions outside `[0, DiskSize - 1]`.
  - **Visual Outputs:** Animated seek graph plotting cylinder number against request order, live decision narration with seek-distance math, ordered service sequence chips, and an **All-6 Algorithm Comparison** bar chart and summary table.

### Part B: CPU Scheduling Studio
- **Algorithms Implemented:**
  - **Round Robin (RR)** — includes Activity 1 (without context-switch overhead), Activity 2 (with configurable context-switch overhead in ms), and an automatic **Quantum Comparison Table**.
  - **FCFS** (First-Come, First-Served)
  - **SJF** (Shortest Job First — Non-Preemptive)
  - **SRTF / SJRF** (Shortest Remaining Time First — Preemptive)
  - **Priority Scheduling (Non-Preemptive & Preemptive)** — supports both *Low Number = High Priority* and *High Number = High Priority* rules.
- **Visual Outputs:**
  - Live CPU state indicator (`IDLE`, `RUNNING`, `CONTEXT SWITCH`, `FINISHED`), millisecond clock, process completion progress bars, animated **Gantt Chart**, live **Ready Queue** visualizer, per-process metrics (`CT`, `TAT`, `WT`, `RT`), and an **All-Algorithm Cross-Comparison Table**.

---

## Project Structure

```text
os_visualizer_disk_cpu_scheduling/
├── index.html             # Complete self-contained interactive visualizer (Part A & Part B)
├── analysis_report.pdf    # Part C: Comparative performance, starvation & SDG 7/9 energy report
├── README.md              # Setup instructions, sample test inputs, and screenshots
└── Screenshots/           # Application screenshots for documentation
    ├── cpu_fcfs_1.png
    ├── cpu_fcfs_2.png
    ├── disk_fcfs_1.png
    ├── disk_fcfs_2.png
    ├── disk_sstf_1.png
    └── disk_sstf_2.png
```

---

## Setup & Running Locally

No build tools, Node.js packages, or backend servers are required.

1. **Clone the repository:**
   ```bash
   git clone https://github.com/ameefathima/os_visualizer_disk_cpu_scheduling.git
   cd os_visualizer_disk_cpu_scheduling
   ```
2. **Launch the application:**
   - Double-click `index.html` to open it directly in any modern web browser (Chrome, Firefox, Edge, Brave, or Safari).
   - Alternatively, serve it locally using Python:
     ```bash
     python3 -m http.server 8000
     ```
     Then open `http://localhost:8000` in your browser.
3. **Offline Usage:** Once downloaded, the visualizer works 100% offline, making it ideal for offline computer labs and low-bandwidth classrooms.

---

## Sample Test Inputs & Expected Outputs

### 1. Disk Scheduling Benchmark (Default Preset)
- **Disk Cylinders:** `0–199` (Disk Size = `200`)
- **Initial Head Position:** `50`
- **Direction:** `Right (Max)`
- **Request Queue:** `82, 170, 43, 140, 24, 16, 190`

| Algorithm | Service Sequence | Total Head Movement |
| :--- | :--- | :---: |
| **FCFS** | `50 → 82 → 170 → 43 → 140 → 24 → 16 → 190` | **642 cylinders** |
| **SSTF** | `50 → 43 → 24 → 16 → 82 → 140 → 170 → 190` | **208 cylinders** |
| **SCAN** | `50 → 82 → 140 → 170 → 190 → 199 → 43 → 24 → 16` | **332 cylinders** |
| **C-SCAN** | `50 → 82 → 140 → 170 → 190 → 199 → 0 → 16 → 24 → 43` | **391 cylinders** |
| **LOOK** | `50 → 82 → 140 → 170 → 190 → 43 → 24 → 16` | **314 cylinders** |
| **C-LOOK** | `50 → 82 → 140 → 170 → 190 → 16 → 24 → 43` | **341 cylinders** |

### 2. CPU Scheduling Benchmark (Default Preset)
- **Processes:**
  - `P1`: Arrival Time = `0 ms`, Burst Time = `5 ms`, Priority = `2`
  - `P2`: Arrival Time = `1 ms`, Burst Time = `3 ms`, Priority = `1`
  - `P3`: Arrival Time = `2 ms`, Burst Time = `4 ms`, Priority = `4`
  - `P4`: Arrival Time = `3 ms`, Burst Time = `2 ms`, Priority = `3`

| Algorithm | Avg Waiting Time (WT) | Avg Turnaround Time (TAT) | Avg Response Time (RT) |
| :--- | :---: | :---: | :---: |
| **FCFS** | `4.25 ms` | `7.75 ms` | `4.25 ms` |
| **SJF (Non-Preemptive)** | `3.50 ms` | `7.00 ms` | `3.50 ms` |
| **SRTF / SJRF (Preemptive)** | `3.00 ms` | `6.50 ms` | `2.50 ms` |
| **Round Robin (`q = 2 ms, CS = 0 ms`)** | `5.50 ms` | `9.00 ms` | `1.50 ms` |

---

## Screenshots

### Part A: Disk Scheduling

#### 1. FCFS (First-Come, First-Served) — Seek Graph & Controls
![FCFS Disk View 1](Screenshots/disk_fcfs_1.png)

#### 2. FCFS (First-Come, First-Served) — All-Algorithm Comparison
![FCFS Disk View 2](Screenshots/disk_fcfs_2.png)

#### 3. SSTF (Shortest Seek Time First) — Seek Graph & Narration
![SSTF Disk View 1](Screenshots/disk_sstf_1.png)

#### 4. SSTF (Shortest Seek Time First) — Comparison Bar Chart
![SSTF Disk View 2](Screenshots/disk_sstf_2.png)

---

### Part B: CPU Scheduling

#### 1. FCFS CPU Scheduling — Process Status & Gantt Chart
![FCFS CPU View 1](Screenshots/cpu_fcfs_1.png)

#### 2. FCFS CPU Scheduling — Complete Metrics & Comparison
![FCFS CPU View 2](Screenshots/cpu_fcfs_2.png)

---

## Deliverables Included
- **`index.html`**: Interactive web application (Part A & Part B).
- **`analysis_report.pdf`**: Part C analysis report covering SSTF vs. FCFS, starvation, solar-powered server energy efficiency (UN SDG 7 & 9), and limitations/extensions.
- **`README.md`**: Documentation, setup instructions, verification tables, and screenshots.