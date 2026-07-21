---
layout: null
title: Simulation-Based Decision Support for Warehouse Operations and Bottleneck Analysis
---

<style>
  body {
    max-width: 980px;
    margin: 0 auto;
    padding: 32px 20px;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Arial, sans-serif;
    line-height: 1.6;
    color: #24292f;
    background: #ffffff;
  }

  a {
    color: #0969da;
  }

  h1, h2, h3 {
    line-height: 1.25;
  }

  .portfolio-title {
    margin-top: 1.2rem;
    margin-bottom: 0.4rem;
  }

  .portfolio-subtitle {
    color: #5f6368;
    font-size: 1.05rem;
    margin-bottom: 1.1rem;
  }

  .portfolio-nav {
    position: sticky;
    top: 0;
    z-index: 5;
    background: #ffffff;
    border: 1px solid #e5e7eb;
    border-radius: 10px;
    padding: 10px 12px;
    margin: 16px 0 22px 0;
    line-height: 1.9;
    box-shadow: 0 1px 5px rgba(0, 0, 0, 0.04);
  }

  .portfolio-nav a {
    display: inline-block;
    margin-right: 12px;
    font-size: 0.92rem;
    text-decoration: none;
  }

  .table-block {
    margin: 1.8rem 0;
  }

  .table-title {
    margin: 0 0 0.65rem;
    font-weight: 700;
  }

  .table-scroll {
    width: 100%;
    overflow-x: auto;
    border: 1px solid #e5e7eb;
    border-radius: 8px;
  }

  .project-table {
    width: 100%;
    min-width: 720px;
    margin: 0;
    border-collapse: collapse;
    background: #ffffff;
    font-size: 0.9rem;
  }

  .project-table th,
  .project-table td {
    padding: 0.65rem 0.75rem;
    border-bottom: 1px solid #e5e7eb;
    text-align: right;
    vertical-align: middle;
    white-space: nowrap;
  }

  .project-table th:first-child,
  .project-table td:first-child {
    text-align: left;
  }

  .project-table thead th {
    background: #f6f8fa;
    color: #24292f;
    font-weight: 700;
  }

  .project-table tbody tr:last-child td {
    border-bottom: none;
  }

  .project-table tbody tr:nth-child(even) {
    background: #fbfcfd;
  }

  .figure-block {
    margin: 2rem 0;
  }

  .interactive-frame {
    display: block;
    width: 100%;
    height: 600px;
    border: 1px solid #e5e7eb;
    border-radius: 8px;
    background: #ffffff;
  }

  .interactive-frame.tall {
    height: 620px;
  }

  .figure-caption {
    margin: 0.65rem 0 0;
    text-align: center;
    font-style: italic;
    line-height: 1.45;
  }

  .results-explanation {
    margin: 1rem 0 2.25rem;
  }

  .tools-list {
    line-height: 1.9;
  }

  @media (max-width: 700px) {
    body {
      padding: 24px 14px;
    }

    .portfolio-title {
      font-size: 1.75rem;
    }

    .portfolio-nav {
      position: static;
    }

    .interactive-frame,
    .interactive-frame.tall {
      height: 540px;
    }
  }
</style>

<h1 class="portfolio-title">Simulation-Based Decision Support for Warehouse Operations and Bottleneck Analysis</h1>

<p class="portfolio-subtitle">Portfolio 3: A Discrete-Event Simulation Study of Staffing Policies, Bottlenecks, and Demand Intensity | Zhiyi Zhu (Elsie Chu)</p>

<div class="portfolio-nav">
  <a href="#1-introduction">Introduction</a>
  <a href="#2-research-question">Research Question</a>
  <a href="#3-system-description">System Description</a>
  <a href="#4-methods">Methods</a>
  <a href="#5-results">Results</a>
  <a href="#6-discussion">Discussion</a>
  <a href="#7-limitations">Limitations</a>
  <a href="#8-conclusion">Conclusion</a>
  <a href="#9-tools">Tools</a>
</div>

<p>
  <a href="final_report.pdf" target="_blank"><strong>View Full Report PDF</strong></a>
</p>

## 1. Introduction

Warehouse order fulfillment usually includes several connected stages, such as picking, packing, and shipping. If one stage has lower capacity than the others, orders may wait in line and form a bottleneck. This can increase waiting time, delay order completion, and limit throughput.

Adding more workers or stations does not always improve the whole system. If the additional resource is not added to the bottleneck stage, the main problem may remain.

In this project, I built a discrete-event simulation model in Python using SimPy. The model was used to compare different staffing and capacity configurations and examine how demand intensity affects warehouse performance.

## 2. Research Question

The main research question is:

> How do different resource configurations affect waiting time, completion time, throughput, and resource utilization in a simulated warehouse system?

The project also examines:

1. Which process stage is the main bottleneck under the baseline configuration?
2. Which tested resource configuration produces the largest improvement?
3. How does the baseline system perform under different demand levels?

## 3. System Description

The simulated warehouse includes three stages:

1. Picking
2. Packing
3. Shipping

After an order arrives, it waits for an available picker. It then moves to packing and finally to shipping before leaving the system.

The baseline system represents one 480-minute warehouse shift. Orders arrive every 5 minutes on average. The baseline resource configuration includes:

- 2 pickers
- 1 packer
- 1 shipping station

The average processing times are 8 minutes for picking, 6 minutes for packing, and 4 minutes for shipping.

<div class="table-block">
  <p class="table-title">Table 1. Baseline warehouse simulation parameters.</p>

  <div class="table-scroll">
    <table class="project-table">
      <thead>
        <tr>
          <th>Parameter</th>
          <th>Baseline value</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Simulation time</td>
          <td>480 minutes</td>
        </tr>
        <tr>
          <td>Average interarrival time</td>
          <td>5 minutes</td>
        </tr>
        <tr>
          <td>Number of pickers</td>
          <td>2</td>
        </tr>
        <tr>
          <td>Number of packers</td>
          <td>1</td>
        </tr>
        <tr>
          <td>Number of shipping stations</td>
          <td>1</td>
        </tr>
        <tr>
          <td>Picking time, mean</td>
          <td>8 minutes</td>
        </tr>
        <tr>
          <td>Picking time, standard deviation</td>
          <td>2 minutes</td>
        </tr>
        <tr>
          <td>Packing time, mean</td>
          <td>6 minutes</td>
        </tr>
        <tr>
          <td>Packing time, standard deviation</td>
          <td>1.5 minutes</td>
        </tr>
        <tr>
          <td>Shipping time, mean</td>
          <td>4 minutes</td>
        </tr>
        <tr>
          <td>Shipping time, standard deviation</td>
          <td>1 minute</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

The model is a simplified warehouse system. All orders follow the same process, and workers and stations remain available during the simulation period. Worker breaks, equipment failures, inventory shortages, order cancellations, and differences between order types are not included.

## 4. Methods

The warehouse model was built in Python using SimPy. Order arrival times and processing times were randomly generated. Because simulation results can vary across runs, each setting was simulated 30 times using different random seeds, and the average results were used for comparison.

Five resource configurations were tested:

- Baseline
- Add One Picker
- Add One Packer
- Add One Shipping Station
- Balanced Capacity

<div class="table-block">
  <p class="table-title">Table 2. Staffing and capacity scenarios.</p>

  <div class="table-scroll">
    <table class="project-table">
      <thead>
        <tr>
          <th>Scenario</th>
          <th>Pickers</th>
          <th>Packers</th>
          <th>Shipping stations</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Baseline</td>
          <td>2</td>
          <td>1</td>
          <td>1</td>
        </tr>
        <tr>
          <td>Add One Picker</td>
          <td>3</td>
          <td>1</td>
          <td>1</td>
        </tr>
        <tr>
          <td>Add One Packer</td>
          <td>2</td>
          <td>2</td>
          <td>1</td>
        </tr>
        <tr>
          <td>Add One Shipping Station</td>
          <td>2</td>
          <td>1</td>
          <td>2</td>
        </tr>
        <tr>
          <td>Balanced Capacity</td>
          <td>3</td>
          <td>2</td>
          <td>1</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

The bottleneck was identified by comparing resource utilization and waiting time before each process stage.

A separate demand sensitivity analysis was also conducted using the baseline resource configuration. The average interarrival time was changed to 6, 5, 4, and 3.5 minutes. A shorter interarrival time represents a higher demand level.

## 5. Results

### 5.1 Staffing and Capacity Scenario Results

<div class="table-block">
  <p class="table-title">Table 3. Mean performance results across resource configurations.</p>

  <div class="table-scroll">
    <table class="project-table">
      <thead>
        <tr>
          <th>Scenario</th>
          <th>Throughput<br>(orders)</th>
          <th>Avg. total waiting time<br>(minutes)</th>
          <th>Avg. completion time<br>(minutes)</th>
          <th>Picker utilization</th>
          <th>Packer utilization</th>
          <th>Shipping utilization</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Baseline</td>
          <td>75.267</td>
          <td>49.680</td>
          <td>67.781</td>
          <td>0.631</td>
          <td>0.947</td>
          <td>0.629</td>
        </tr>
        <tr>
          <td>Add One Picker</td>
          <td>76.133</td>
          <td>49.253</td>
          <td>67.347</td>
          <td>0.427</td>
          <td>0.951</td>
          <td>0.638</td>
        </tr>
        <tr>
          <td>Add One Packer</td>
          <td>91.233</td>
          <td>8.643</td>
          <td>26.716</td>
          <td>0.763</td>
          <td>0.573</td>
          <td>0.764</td>
        </tr>
        <tr>
          <td>Add One Shipping Station</td>
          <td>75.533</td>
          <td>52.364</td>
          <td>70.448</td>
          <td>0.632</td>
          <td>0.947</td>
          <td>0.317</td>
        </tr>
        <tr>
          <td>Balanced Capacity</td>
          <td>92.733</td>
          <td>6.737</td>
          <td>24.755</td>
          <td>0.520</td>
          <td>0.575</td>
          <td>0.772</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

<div class="results-explanation" markdown="1">

Table 3 compares the average performance of the five resource configurations based on 30 simulation replications for each scenario. Add One Picker and Add One Shipping Station produced results close to the baseline, which had an average throughput of (**75.267 orders**), an average total waiting time of (**49.680 minutes**), and an average completion time of (**67.781 minutes**). Add One Packer produced a much larger improvement, increasing throughput to (**91.233 orders**) and reducing total waiting time to (**8.643 minutes**). Balanced Capacity achieved the best overall performance among the five tested configurations, with the highest throughput (**92.733 orders**), the lowest total waiting time (**6.737 minutes**), and the lowest completion time (**24.755 minutes**).

</div>

<div class="figure-block">
  <iframe
    class="interactive-frame"
    src="interactive/figure1_completion_time.html"
    title="Interactive Figure 1: Average completion time by resource configuration"
    loading="lazy"
  ></iframe>

  <p class="figure-caption">Figure 1. Average completion time by resource configuration.</p>
</div>

<div class="figure-block">
  <iframe
    class="interactive-frame"
    src="interactive/figure2_total_waiting_time.html"
    title="Interactive Figure 2: Average total waiting time by resource configuration"
    loading="lazy"
  ></iframe>

  <p class="figure-caption">Figure 2. Average total waiting time by resource configuration.</p>
</div>

<div class="figure-block">
  <iframe
    class="interactive-frame"
    src="interactive/figure3_throughput.html"
    title="Interactive Figure 3: Average throughput by resource configuration"
    loading="lazy"
  ></iframe>

  <p class="figure-caption">Figure 3. Average throughput by resource configuration.</p>
</div>

<div class="results-explanation" markdown="1">

Figures 1–3 compare the five resource configurations using average completion time, average total waiting time, and throughput. Add One Packer and Balanced Capacity performed much better than the other scenarios. Add One Packer reduced average completion time to (**26.716 minutes**) and total waiting time to (**8.643 minutes**), while increasing throughput to (**91.233 orders**). Balanced Capacity achieved the best overall results, with the lowest average completion time (**24.755 minutes**), the lowest total waiting time (**6.737 minutes**), and the highest throughput (**92.733 orders**). These figures show that increasing packing capacity produced the largest improvement in overall warehouse performance.

</div>

### 5.2 Bottleneck Analysis

<div class="table-block">
  <p class="table-title">Table 4. Bottleneck indicators and performance changes relative to the baseline.</p>

  <div class="table-scroll">
    <table class="project-table">
      <thead>
        <tr>
          <th>Scenario</th>
          <th>Highest-utilization resource</th>
          <th>Max. utilization</th>
          <th>Longest-wait stage</th>
          <th>Longest wait<br>(minutes)</th>
          <th>Throughput change<br>(orders)</th>
          <th>Waiting-time reduction<br>(%)</th>
          <th>Completion-time reduction<br>(%)</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Baseline</td>
          <td>Packer</td>
          <td>0.947</td>
          <td>Packing</td>
          <td>42.093</td>
          <td>0.000</td>
          <td>0.000</td>
          <td>0.000</td>
        </tr>
        <tr>
          <td>Add One Picker</td>
          <td>Packer</td>
          <td>0.951</td>
          <td>Packing</td>
          <td>48.166</td>
          <td>0.867</td>
          <td>0.858</td>
          <td>0.640</td>
        </tr>
        <tr>
          <td>Add One Packer</td>
          <td>Shipping Station</td>
          <td>0.764</td>
          <td>Picking</td>
          <td>5.307</td>
          <td>15.967</td>
          <td>82.603</td>
          <td>60.586</td>
        </tr>
        <tr>
          <td>Add One Shipping Station</td>
          <td>Packer</td>
          <td>0.947</td>
          <td>Packing</td>
          <td>44.833</td>
          <td>0.267</td>
          <td>-5.403</td>
          <td>-3.934</td>
        </tr>
        <tr>
          <td>Balanced Capacity</td>
          <td>Shipping Station</td>
          <td>0.772</td>
          <td>Shipping</td>
          <td>4.967</td>
          <td>17.467</td>
          <td>86.439</td>
          <td>63.478</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

<div class="results-explanation" markdown="1">

Table 4 compares the bottleneck indicators and performance changes relative to the baseline. In the baseline configuration, the packer had the highest utilization (**0.947**), and packing had the longest average waiting time (**42.093 minutes**), indicating that packing was the main bottleneck. After one packer was added, total waiting time decreased by (**82.603%**) and completion time decreased by (**60.586%**). Balanced Capacity produced the largest overall improvement, with throughput increasing by (**17.467 orders**) and total waiting time decreasing by (**86.439%**).

</div>

<div class="figure-block">
  <iframe
    class="interactive-frame"
    src="interactive/figure4_resource_utilization.html"
    title="Interactive Figure 4: Resource utilization by resource configuration"
    loading="lazy"
  ></iframe>

  <p class="figure-caption">Figure 4. Resource utilization by resource configuration.</p>
</div>

<div class="figure-block">
  <iframe
    class="interactive-frame"
    src="interactive/figure5_stage_waiting_time.html"
    title="Interactive Figure 5: Average waiting time by process stage and resource configuration"
    loading="lazy"
  ></iframe>

  <p class="figure-caption">Figure 5. Average waiting time by process stage and resource configuration.</p>
</div>

<div class="results-explanation" markdown="1">

Figures 4 and 5 show resource utilization and average waiting time across the three stages—picking, packing, and shipping under five scenarios. Figure 4 shows that packer utilization under Add One Packer (**0.573**) and Balanced Capacity (**0.575**) was lower than under the other three scenarios, where packer utilization remained close to (**0.950**) in the Baseline, Add One Picker, and Add One Shipping Station scenarios. Figure 5 shows that average packing waiting time was very low under Add One Packer (**0.212 minutes**) and Balanced Capacity (**0.966 minutes**). In contrast, average packing waiting time remained much higher under the Baseline (**42.093 minutes**), Add One Picker (**48.166 minutes**), and Add One Shipping Station (**44.833 minutes**) scenarios.

Therefore, the packing bottleneck identified in the baseline was removed as the main bottleneck under the Add One Packer and Balanced Capacity configurations. However, as the resource configuration changed, the main constraint could shift to another stage. Under Add One Packer, the results did not identify one single dominant new bottleneck. Under Balanced Capacity, shipping became the clearest new bottleneck in this scenario.

</div>

### 5.3 Demand Sensitivity Analysis

<div class="table-block">
  <p class="table-title">Table 5. Demand sensitivity analysis results under the baseline resource configuration.</p>

  <div class="table-scroll">
    <table class="project-table">
      <thead>
        <tr>
          <th>Average interarrival time<br>(minutes)</th>
          <th>Throughput<br>(orders)</th>
          <th>Avg. total waiting time<br>(minutes)</th>
          <th>Avg. completion time<br>(minutes)</th>
          <th>Picker utilization</th>
          <th>Packer utilization</th>
          <th>Shipping utilization</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>6.0</td>
          <td>71.867</td>
          <td>28.610</td>
          <td>46.696</td>
          <td>0.595</td>
          <td>0.911</td>
          <td>0.605</td>
        </tr>
        <tr>
          <td>5.0</td>
          <td>75.267</td>
          <td>49.680</td>
          <td>67.781</td>
          <td>0.631</td>
          <td>0.947</td>
          <td>0.629</td>
        </tr>
        <tr>
          <td>4.0</td>
          <td>77.233</td>
          <td>83.955</td>
          <td>102.027</td>
          <td>0.647</td>
          <td>0.965</td>
          <td>0.648</td>
        </tr>
        <tr>
          <td>3.5</td>
          <td>77.867</td>
          <td>101.439</td>
          <td>119.509</td>
          <td>0.657</td>
          <td>0.967</td>
          <td>0.651</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

<div class="figure-block">
  <iframe
    class="interactive-frame tall"
    src="interactive/figure6_demand_waiting_time.html"
    title="Interactive Figure 6: Average total waiting time and average completion time under different demand levels"
    loading="lazy"
  ></iframe>

  <p class="figure-caption">Figure 6. Average total waiting time and average completion time under different demand levels.</p>
</div>

<div class="figure-block">
  <iframe
    class="interactive-frame tall"
    src="interactive/figure7_demand_throughput.html"
    title="Interactive Figure 7: Average throughput under different demand levels"
    loading="lazy"
  ></iframe>

  <p class="figure-caption">Figure 7. Average throughput under different demand levels.</p>
</div>

<div class="results-explanation" markdown="1">

Table 5 and Figures 6 and 7 show how the baseline resource configuration performed under four different demand levels, with average interarrival times of (6.0, 5.0, 4.0, and 3.5 minutes). As the average interarrival time decreased from (**6.0 minutes**) to (**3.5 minutes**), the demand level increased. The results show that average total waiting time increased sharply from (**28.610 minutes**) to (**101.439 minutes**), while average completion time increased substantially from (**46.696 minutes**) to (**119.509 minutes**). However, throughput increased steadily from (**71.867 orders**) to (**77.867 orders**), showing that the baseline system was approaching its capacity limit as demand increased.

</div>

## 6. Discussion

The baseline results show that packing was the main bottleneck because the packer had the highest utilization (**0.947**) and packing had the longest average waiting time (**42.093 minutes**). Therefore, adding one picker or one shipping station did not produce a meaningful improvement because neither change increased capacity at the packing stage. Their throughput and waiting-time results remained close to the baseline.

After one packer was added, average total waiting time decreased from (**49.680 minutes**) to (**8.643 minutes**), while average completion time decreased from (**67.781 minutes**) to (**26.716 minutes**). This shows that increasing capacity at the actual bottleneck was much more effective than adding resources to other stages. Under Add One Packer, shipping had the highest utilization (**0.764**), while picking had the longest waiting time (**5.307 minutes**). Because these two indicators pointed to different stages, the results did not identify one single dominant new bottleneck. Under Balanced Capacity, shipping became both the highest-utilization resource (**0.772**) and the longest-wait stage (**4.967 minutes**), showing that shipping became the clearest new bottleneck in this scenario.

The sensitivity analysis also shows that the baseline system became less stable as demand increased. When the average interarrival time decreased from (**6.0 minutes**) to (**3.5 minutes**), average total waiting time increased sharply from (**28.610 minutes**) to (**101.439 minutes**), while throughput increased only slightly from (**71.867 orders**) to (**77.867 orders**). These results show that warehouse resources should be added based on the actual bottleneck rather than increasing capacity at every stage. They also show that capacity planning should consider how the bottleneck may shift after the original constraint is removed.

## 7. Limitations

1. The model parameters were based on simulated assumptions rather than real warehouse data, so the results may not fully represent actual warehouse operations.
2. The model only included picking, packing, and shipping, without considering equipment failures, employee breaks, order priorities, rework, or differences in order complexity.
3. The analysis compared only (**5 staffing configurations**) and tested (**4 demand levels**) under the baseline resources.
4. The model did not include labor or equipment costs, so the results cannot directly identify the most cost-effective resource configuration.

## 8. Conclusion

This project used discrete-event simulation to identify warehouse bottlenecks and compare different staffing configurations. In the baseline system, packing was the main bottleneck, with packer utilization of (**0.947**) and an average packing waiting time of (**42.093 minutes**). Among the three single-resource addition scenarios, Add One Packer produced the largest improvement, reducing average total waiting time to (**8.643 minutes**). Balanced Capacity achieved the best overall performance among the five tested resource configurations, with the highest throughput (**92.733 orders**) and the lowest total waiting time (**6.737 minutes**). The sensitivity analysis shows that the baseline system approached its capacity limit as demand increased. Overall, the simulation provides useful decision support for warehouse staffing and capacity planning.

## 9. Tools

<div class="tools-list">
  <strong>Python:</strong> simulation modeling and data analysis<br>
  <strong>SimPy:</strong> discrete-event simulation<br>
  <strong>pandas / NumPy:</strong> data processing and aggregation<br>
  <strong>Matplotlib:</strong> static result visualization<br>
  <strong>Plotly:</strong> interactive visualization for GitHub Pages<br>
  <strong>Jupyter Notebook:</strong> project workflow<br>
  <strong>GitHub Pages:</strong> portfolio presentation
</div>
