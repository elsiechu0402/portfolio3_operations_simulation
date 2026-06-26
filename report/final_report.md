# Simulation-Based Decision Support for Warehouse Operations and Bottleneck Analysis

## 1. Introduction

Warehouse order fulfillment systems often involve multiple operational stages, including picking, packing, and shipping. When order arrivals exceed the processing capacity of one or more resources, queues can form and create operational bottlenecks. These bottlenecks increase waiting time, delay order completion, and reduce overall system efficiency.

This project develops a discrete-event simulation model for a simplified warehouse order fulfillment system. The goal is to evaluate how different staffing and capacity policies affect waiting time, throughput, order completion time, and resource utilization. The project demonstrates how simulation-based decision support can help identify bottlenecks and compare operational policies before making real operational changes.

This project is part of an Operations and Supply Chain Analytics portfolio. It complements previous portfolio work on demand forecasting, inventory decision-making, logistics optimization, and warehouse allocation by focusing on warehouse operations simulation and bottleneck analysis.

## 2. Research Question

The main research question is:

**How can simulation-based decision support help identify bottlenecks and evaluate operational policies in warehouse order fulfillment systems?**

This question is examined through three sub-questions:

1. Under the baseline staffing policy, which resource becomes the bottleneck in the warehouse fulfillment process?
2. How do different staffing policies affect order waiting time, completion time, throughput, and resource utilization?
3. Can simulation-based scenario analysis support better resource allocation decisions in warehouse operations?

## 3. System Description

The simulated warehouse order fulfillment process follows this sequence:

Orders arrive -> Picking -> Packing -> Shipping -> Order completed

The system includes three key resources:

- Pickers: workers responsible for picking items.
- Packers: workers responsible for packing completed orders.
- Shipping stations: stations responsible for final outbound processing.

Each order enters the system, waits if the required resource is busy, receives service at each stage, and exits after shipping is completed.

The baseline system is defined as follows:

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

Order arrivals are generated using random interarrival times. Processing times are also randomly generated around the assumed mean values. This allows the simulation to reflect operational variability rather than assuming a fully deterministic system.

## 4. Methods

This project uses discrete-event simulation with Python and SimPy. Each order is modeled as an entity moving through picking, packing, and shipping. Each resource is modeled with limited capacity. If all units of a resource are busy, the order waits in queue.

For each scenario, the simulation runs 30 replications using different random seeds. Multiple replications are used because single-run simulation results can be affected by randomness in order arrivals and processing times.

The main performance metrics are:

- Throughput: number of completed orders during the simulation horizon.
- Average waiting time: average time an order spends waiting for resources.
- Average completion time: average time from order arrival to order completion.
- Waiting time by stage: waiting time before picking, packing, and shipping.
- Resource utilization: proportion of available resource time used by each resource type.
- Bottleneck resource: resource with the highest utilization and associated waiting time.

## 5. Scenario Design

Five staffing and capacity scenarios are compared:

| Scenario | Pickers | Packers | Shipping Stations |
|---|---:|---:|---:|
| Baseline | 2 | 1 | 1 |
| Add One Picker | 3 | 1 | 1 |
| Add One Packer | 2 | 2 | 1 |
| Add One Shipping Station | 2 | 1 | 2 |
| Balanced Capacity | 3 | 2 | 1 |

The purpose of this scenario design is to compare whether adding picking, packing, or shipping capacity produces the greatest improvement in system performance.

## 6. Results

### 6.1 Scenario Comparison

The scenario comparison results are summarized below.

| Scenario | Pickers | Packers | Shipping Stations | Throughput | Avg Total Waiting Time | Avg Completion Time | Picker Utilization | Packer Utilization | Shipping Utilization |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Baseline | 2 | 1 | 1 | 75.267 | 49.68 | 67.781 | 0.631 | 0.947 | 0.629 |
| Add One Picker | 3 | 1 | 1 | 76.133 | 49.253 | 67.347 | 0.427 | 0.951 | 0.638 |
| Add One Packer | 2 | 2 | 1 | 91.233 | 8.643 | 26.716 | 0.763 | 0.573 | 0.764 |
| Add One Shipping Station | 2 | 1 | 2 | 75.533 | 52.364 | 70.448 | 0.632 | 0.947 | 0.317 |
| Balanced Capacity | 3 | 2 | 1 | 92.733 | 6.737 | 24.755 | 0.52 | 0.575 | 0.772 |

The baseline scenario completes an average of 75.267 orders during the 480-minute simulation horizon. Its average total waiting time is 49.680 minutes, and its average completion time is 67.781 minutes.

Adding one picker produces very limited improvement. Average completion time decreases only slightly from 67.781 minutes to 67.347 minutes. This suggests that picking capacity is not the main constraint under the baseline system.

Adding one packer produces a substantial improvement. Average total waiting time decreases from 49.680 minutes to 8.643 minutes, and average completion time decreases from 67.781 minutes to 26.716 minutes. Throughput also increases from 75.267 to 91.233 completed orders.

Adding one shipping station does not improve performance. Average total waiting time increases slightly to 52.364 minutes, and average completion time increases to 70.448 minutes. This suggests that shipping capacity is not the main bottleneck.

The balanced capacity scenario has the strongest overall performance among the tested scenarios. It achieves the highest throughput, the lowest average total waiting time, and the lowest average completion time.

### 6.2 Bottleneck Analysis

The bottleneck analysis results are summarized below.

| Scenario | Max Utilization Resource | Max Utilization | Longest Wait Stage | Longest Wait Minutes | Throughput Change | Waiting Time Reduction (%) | Completion Time Reduction (%) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Baseline | Packer | 0.947 | Packing | 42.093 | 0.0 | 0.0 | 0.0 |
| Add One Picker | Packer | 0.951 | Packing | 48.166 | 0.867 | 0.858 | 0.64 |
| Add One Packer | Shipping Station | 0.764 | Picking | 5.307 | 15.967 | 82.603 | 60.586 |
| Add One Shipping Station | Packer | 0.947 | Packing | 44.833 | 0.267 | -5.403 | -3.934 |
| Balanced Capacity | Shipping Station | 0.772 | Shipping | 4.967 | 17.467 | 86.439 | 63.478 |

The baseline scenario shows that the packer is the most heavily utilized resource, with utilization of 0.947. The longest waiting stage is packing, with an average waiting time of 42.093 minutes. This indicates that the packing stage is the main bottleneck under the baseline configuration.

The Add One Picker scenario still has packer utilization of 0.951, and the longest waiting stage remains packing. This means that adding picking capacity does not resolve the system bottleneck.

The Add One Packer scenario shifts the system away from the original packing bottleneck. Waiting time is reduced by 82.603% compared with the baseline, and completion time is reduced by 60.586%. This confirms that packing capacity is the most effective resource to improve under the baseline conditions.

The Add One Shipping Station scenario still shows the packer as the highest-utilization resource, and packing remains the longest waiting stage. This supports the conclusion that adding shipping capacity does not address the main operational constraint.

The Balanced Capacity scenario reduces average waiting time by 86.439% and completion time by 63.478% compared with the baseline. This scenario provides the strongest overall improvement among the tested policies.

### 6.3 Figures

The following figures were generated and saved in both PDF and PNG formats:

- Average completion time by scenario
- Average total waiting time by scenario
- Throughput by scenario
- Resource utilization by scenario
- Waiting time by process stage

The most important visual evidence comes from the resource utilization and waiting time by stage figures. These figures show that baseline packer utilization is close to full capacity and that packing has the highest waiting time. They also show that adding packing capacity sharply reduces waiting time.

## 7. Sensitivity Analysis

A demand intensity sensitivity analysis is conducted by changing the average interarrival time while keeping the baseline staffing configuration fixed.

The tested demand scenarios are:

| Average Interarrival Time | Interpretation |
|---:|---|
| 6 minutes | Lower demand |
| 5 minutes | Baseline demand |
| 4 minutes | Higher demand |
| 3.5 minutes | Very high demand |

The sensitivity analysis results are summarized below.

| Demand Scenario | Avg Interarrival Time | Throughput | Avg Total Waiting Time | Avg Completion Time | Picker Utilization | Packer Utilization | Shipping Utilization |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Interarrival Time = 6 min | 6.0 | 71.867 | 28.61 | 46.696 | 0.595 | 0.911 | 0.605 |
| Interarrival Time = 5 min | 5.0 | 75.267 | 49.68 | 67.781 | 0.631 | 0.947 | 0.629 |
| Interarrival Time = 4 min | 4.0 | 77.233 | 83.955 | 102.027 | 0.647 | 0.965 | 0.648 |
| Interarrival Time = 3.5 min | 3.5 | 77.867 | 101.439 | 119.509 | 0.657 | 0.967 | 0.651 |

As the average interarrival time decreases from 6 minutes to 3.5 minutes, orders arrive more frequently. The results show that average total waiting time increases from 28.610 minutes to 101.439 minutes. Average completion time also increases from 46.696 minutes to 119.509 minutes.

Throughput increases only slightly, from 71.867 to 77.867 completed orders, even though demand becomes much higher. This suggests that the system reaches a capacity limit. Additional demand mainly creates longer queues rather than proportional increases in completed orders.

Packer utilization remains high across all demand levels and increases from 0.911 to 0.967. This supports the conclusion that the packing bottleneck becomes more severe as demand intensity increases.

## 8. Discussion

The simulation results provide clear operational insights. Under the baseline system, the packing stage is the main bottleneck. This is supported by both high packer utilization and high waiting time before packing.

Adding one picker does not substantially improve performance because the system is not primarily constrained by picking capacity. Similarly, adding one shipping station does not improve performance because shipping is not the main constraint.

Adding one packer creates a large improvement in waiting time, completion time, and throughput. This indicates that targeted capacity expansion at the bottleneck stage is more effective than increasing capacity at non-bottleneck stages.

The balanced capacity scenario performs best overall because it improves upstream picking capacity while also resolving the packing bottleneck. However, the results also show that after packing is improved, downstream shipping utilization becomes higher. This illustrates an important operations principle: once one bottleneck is relieved, another stage may become the next constraint.

The sensitivity analysis further shows that the baseline system becomes increasingly unstable as demand increases. When orders arrive more frequently, waiting time rises sharply while throughput increases only slightly. This suggests that the warehouse cannot absorb higher demand without additional capacity, especially at the packing stage.

## 9. Limitations

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
- Learning effects or worker fatigue

Because of these simplifications, the numerical results should not be interpreted as estimates for a specific real warehouse. Instead, the project demonstrates a simulation-based decision support framework that can be extended with real operational data.

## 10. Conclusion

This project shows how discrete-event simulation can support warehouse operations decision-making. By modeling order arrivals, picking, packing, and shipping processes, the simulation identifies where queues form and which resource constrains system performance.

The baseline system is mainly constrained by the packing stage. Adding one packer reduces average waiting time and completion time much more effectively than adding a picker or shipping station. The balanced capacity scenario achieves the best overall performance among the tested policies.

The sensitivity analysis shows that as demand intensity increases, waiting time rises sharply and packer utilization remains close to full capacity. This confirms that packing capacity is a critical constraint under both baseline and high-demand conditions.

Overall, this project demonstrates how simulation-based decision support can be used for bottleneck analysis, capacity planning, and resource allocation in warehouse operations.