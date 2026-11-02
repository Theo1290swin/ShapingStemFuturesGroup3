# Group 3: Biogas Simulation – Risk, Cost and Safety Evaluation Layer

This repository contains the Python simulation, safety screening engine, and multi-criteria evaluation module developed by Group 3 for the Swinburne University **"Waste-to-Energy Simulation: Biogas Production from Food Waste"** project, supervised by Dr Bita Zaferanloo.

## Overview

This is a laboratory-scale evaluation engine. The program:

1. Scales raw methane yields to a physical 2.5 kg prototype test batch (0.5625 kg VS).
2. Partitions total biogas into methane (CH<sub>4</sub>), carbon dioxide (CO<sub>2</sub>), and toxic hydrogen sulfide (H<sub>2</sub>S).
3. Evaluates room gas concentrations in an unventilated 50 m³ space against Safe Work Australia workplace exposure limits (10 ppm TWA / 15 ppm STEL).
4. Implements Equations R10 and R11 to compute comparative deltas relative to the S3 moderate fungal reference condition.
5. Performs transparent 0-to-1 min-max scaling to rank scenarios across Net Energy, Process Stability, Gas Risk, and Unit Cost.

## Repository Contents

| File | Description |
|------|-------------|
| `group3_simulation_v4.ipynb` | Interactive Jupyter Notebook containing all evaluation equations, tables, and visualisation routines. |
| `scenario_summary.csv` | Primary dataset containing simulated results for Scenarios S1 to S13 (Group 1 dataset). |
| `scenario_summary_results.csv` | Benchmark reference dataset containing published results for Scenarios S1 to S9 (Zenodo repository). |
| `requirements.txt` | Python package dependencies. |

## Installation and Execution

### 1. Clone this repository

```bash
git clone https://github.com/Theo1290swin/ShapingStemFuturesGroup3.git
cd ShapingStemFuturesGroup3
```

### 2. Install dependencies

Ensure you have Python 3.10+ installed, then install the required packages:

```bash
pip install -r requirements.txt
```

### 3. Run the notebook

Open the project directory in Visual Studio Code or JupyterLab, and run all cells in `group3_simulation_v4.ipynb`.

## User Configuration

The notebook features a **User Configuration Block** at the top. Users can modify laboratory operational assumptions in one central place without modifying any underlying equations:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `DATASET_CHOICE` | Switch between `"group1"` (evaluates S1 to S13) and `"zenodo"` (evaluates S1 to S9 benchmark). | `"group1"` |
| `LAB_FEED_WET_KG` | Prototype feedstock batch mass in kg. Set to 0.75 kg for standard six-bottle BMP testing. | `2.5` |
| `FEED_TS` | Total solids fraction on a wet basis. | `0.25` |
| `FEED_VS_TS` | Volatile solids fraction of total solids. | `0.90` |
| `ROOM_VOLUME_M3` | Enclosed laboratory room volume in m³ (50 m³ = 50,000 L of air). | `50.0` |
| `BIOGAS_H2S_PPM` | Concentration of H<sub>2</sub>S in raw biogas (ppmv). Adjust up to 3000.0 for high-sulfur protein feeds. | `1065.0` |
| `H2S_REMOVAL_EFFICIENCY` | Chemical trap scrubbing efficiency. 0.0 = unscrubbed worst-case leak; set to 0.95 for active NaOH and carbon filtering. | `0.0` |
| `WEIGHT_ENERGY`, `WEIGHT_STABILITY`, `WEIGHT_RISK`, `WEIGHT_COST` | Multi-criteria screening weights (must sum to 1.0). | `0.25` each |

## Visualisation Outputs

When executed, the notebook produces three figures:

1. **Figure 1 – Gas Volume Breakdown and H<sub>2</sub>S Safety:** A dual-panel figure displaying stacked batch gas volumes (CH<sub>4</sub> and CO<sub>2</sub>) with total volume labels on the left, and worst-case room H<sub>2</sub>S concentrations plotted against Safe Work Australia TWA and STEL limits on the right.
2. **Figure 2 – Comparative Screening Evaluation Score:** A bar chart ranking each scenario by its composite score, highlighting reference anchors S1 (control), S3 (fungal reference), and S6 (circular economy coffee reference).
3. **Figure 3 – Methane Yield Change Relative to S3:** A percentage gain/loss chart relative to the S3 baseline, implementing Equation R11.
