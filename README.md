# Marketing Analytics Case Study

A take-home assignment that uses three heatmaps to screen a year of daily marketing performance for long-term trends, possible reversals, and unusual spikes or drops. The heatmaps summarize 162 time series across 18 segments and nine KPIs, so an analyst can choose which series and dates to investigate in detail.

[Open the analysis notebook and its charts](MA_test_task.ipynb)

## Data

The input file, `performance_daily.csv`, contains one year of daily performance data for Paid Search, Paid Social, Organic Search, and Email.

| Fields | Description |
| --- | --- |
| `date` | Observation date |
| `channel`, `campaign_type`, `geo_group` | Dimensions used to define segments |
| `spend`, `sessions`, `purchases`, `revenue` | Input metrics |

The notebook calculates conversion rate (CVR), average order value (AOV), revenue per session (RPS), return on ad spend (ROAS), and cost per acquisition (CPA). These five metrics and the four input metrics make up the nine KPIs.

## How the heatmaps work

| Heatmap | Method | What to look for |
| --- | --- | --- |
| Long-term trends | Fit a linear trend and calculate the percentage change between its fitted start and end values. | Identify rising or falling KPIs. Use the average daily value shown in each cell to put the percentage change in context. |
| Possible reversals | Fit a quadratic curve and compare its midpoint with the average of its endpoints. | Inspect U-shaped or inverted U-shaped series for possible changes in direction. |
| Daily anomalies | Compare each value with a centered rolling median over up to 21 observations. Scale the residuals using the median absolute deviation (MAD). | Review the date and signed robust z-score of the largest absolute deviation for each segment and KPI. |

## Example follow-up

In the **Paid Search / Non-Brand / Core** segment, the fitted trends showed spend rising by about 38% and revenue by about 4%, while ROAS fell by about 23%. This combination makes the segment a candidate for a closer look at when ad efficiency weakened and which campaigns contributed.

The curvature and anomaly scores are screening measures. The next step is to inspect the underlying daily series and compare flagged periods with campaign changes or other relevant events.

## Run locally

1. Download or clone the repository. Place `performance_daily.csv` next to `MA_test_task.ipynb`.
2. From that directory, install the dependencies and launch Jupyter.

   ```bash
   python -m pip install jupyter numpy pandas matplotlib seaborn
   jupyter notebook MA_test_task.ipynb
   ```

3. Select the Python kernel with those packages installed and run all cells.
