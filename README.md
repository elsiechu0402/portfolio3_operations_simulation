# Simulation-Based Decision Support for Warehouse Operations and Bottleneck Analysis

## Project Overview

This project develops a discrete-event simulation model for a simplified warehouse order fulfillment system. The simulated system includes order arrivals, picking, packing, and shipping processes. The goal is to evaluate how different staffing and capacity policies affect waiting time, order completion time, throughput, and resource utilization.

This project is part of my Operations and Supply Chain Analytics portfolio. It demonstrates how simulation-based decision support can be used to identify bottlenecks and compare operational policies before implementing changes in a real warehouse system.

## Research Question

**How can simulation-based decision support help identify bottlenecks and evaluate operational policies in warehouse order fulfillment systems?**

## System Description

The warehouse order fulfillment process is modeled as:

Orders arrive -> Picking -> Packing -> Shipping -> Order completed

The system includes three key resources:

- Pickers
- Packers
- Shipping stations

Each order may wait before each process stage if the required resource is busy.

## Baseline System

| Parameter | Value |
|---|---:|
| Simulation time | 480 minutes |
| Average interarrival time | 5 minutes |
| Number of pickers | 2 |
| Number of packers | 1 |
| Number of shipping stations | 1 |
| Mean picking time | 8 minutes |
| Mean packing time | 6 minutes |
| Mean shipping time | 4 minutes |

## Methodology

This project uses discrete-event simulation with Python and SimPy. The simulation model represents each order as it moves through picking, packing, and shipping.

For each scenario, the model runs 30 replications with different random seeds. The results are summarized using the following performance metrics:

- Throughput
- Average waiting time
- Average order completion time
- Waiting time by process stage
- Picker utilization
- Packer utilization
- Shipping station utilization
- Bottleneck resource

## Scenario Design

The project compares five staffing and capacity scenarios:

| Scenario | Pickers | Packers | Shipping Stations |
|---|---:|---:|---:|
| Baseline | 2 | 1 | 1 |
| Add One Picker | 3 | 1 | 1 |
| Add One Packer | 2 | 2 | 1 |
| Add One Shipping Station | 2 | 1 | 2 |
| Balanced Capacity | 3 | 2 | 1 |

## Key Findings

The baseline system shows a clear bottleneck at the packing stage. Under the baseline configuration, packer utilization is approximately 0.947, and the average waiting time before packing is much higher than the waiting time before picking or shipping.

Adding one picker does not meaningfully improve system performance because the main constraint is not picking capacity. Adding one shipping station also provides little benefit because shipping is not the primary bottleneck.

Adding one packer substantially improves system performance. Compared with the baseline, this scenario reduces average total waiting time by approximately 82.6% and average completion time by approximately 60.6%.

The balanced capacity scenario achieves the strongest overall performance among the tested policies. It increases throughput and reduces both waiting time and completion time.

## Sensitivity Analysis

A demand intensity sensitivity analysis is conducted by changing the average interarrival time:

| Average Interarrival Time | Interpretation |
|---:|---|
| 6 minutes | Lower demand |
| 5 minutes | Baseline demand |
| 4 minutes | Higher demand |
| 3.5 minutes | Very high demand |

The results show that as orders arrive more frequently, average waiting time increases sharply and packer utilization remains close to full capacity. This suggests that the packing bottleneck becomes more severe under higher demand intensity.

## Repository Structure

- data/simulated/: simulated data folder
- notebooks/: Jupyter notebook for the simulation analysis
- src/: source code folder
- outputs/figures/: saved figures in PDF and PNG formats
- outputs/tables/: saved result tables
- report/: final report files
- docs/: GitHub Pages files
- README.md: project overview
- requirements.txt: Python package requirements

## Main Outputs

Final result tables are saved in:

- outputs/tables/final_scenario_summary.csv
- outputs/tables/final_bottleneck_summary.csv
- outputs/tables/final_sensitivity_summary.csv

Figures are saved in:

- outputs/figures/

Each figure is saved in both PDF and PNG formats.

## Tools and Packages

This project uses:

- Python 3.11.15
- pandas
- numpy
- matplotlib
- simpy
- Jupyter Notebook
- VS Code

## How to Run

1. Open the project folder in VS Code.
2. Activate the ops311 conda environment.
3. Open notebooks/01_warehouse_simulation.ipynb.
4. Run the notebook cells from top to bottom.

## Limitations

This project uses a simplified simulated warehouse order fulfillment system. Order arrivals and processing times are generated based on operational assumptions rather than confidential real warehouse process data.

The model does not include:

- Real warehouse layout
- Worker travel distance
- Order priority rules
- Labor cost
- Shift scheduling
- Batch picking
- Product-level differences
- Real WMS validation

Despite these limitations, the project demonstrates how discrete-event simulation can support bottleneck analysis, capacity planning, and resource allocation decisions in warehouse operations.

## Conclusion

This project shows that simulation-based decision support can help identify operational bottlenecks and compare staffing policies in warehouse order fulfillment systems. The analysis finds that the baseline system is constrained mainly by the packing stage, and that adding packing capacity is more effective than adding picking or shipping capacity.

The project supports my broader Operations and Supply Chain Analytics portfolio by demonstrating simulation-based analysis for warehouse operations, bottleneck identification, and operational decision support.