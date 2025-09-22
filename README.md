# Customer Value Analytics

**Author**: Marco Boso 
**Date**: September 22, 2025  
**Project Type**: Customer Analytics / Retention and Revenue

## Overview

This project transforms raw transaction data into practical decisions with a full customer analytics toolkit in R. It combines RFM segmentation to profile value and behavior, Pareto/ABC to highlight product concentration, cohort retention to map repeat dynamics, interactive Plotly visuals to explore patterns, and churn prediction to flag risk early. It ships as an R Markdown report, with an HTML version that includes interactive charts
## Dataset

Default input: `Pedidos.csv` (UTF-8). The report validates required columns and stops with a readable message if any are missing.

**Minimum fields**
- `id_cliente` — customer ID  
- `nombre_del_cliente` — customer name  
- `id_pedido` — order ID  
- `fecha_de_pedido` — order date (YYYY-MM-DD)  
- `ventas` — sales amount (numeric)  
- `cantidad` — units (numeric)  
- `nombre_del_producto` — product name

## Libraries

`tidyverse`, `lubridate`, `scales`, `forcats`, `ggplot2`, `patchwork`, `ggrepel`, `zoo`, `glue`,  
`plotly`, `htmlwidgets`, `htmltools`, `tsibble`, `fable`, `feasts`, `randomForest`, `janitor`,  
`skimr`, `DataExplorer`, `rmarkdown`, `knitr`

## Methods

- **RFM analysis**: scores by recency, frequency, and monetary value; segment distribution; R×F heatmap with euro labels and hover details  
- **Pareto / ABC**: product contribution with cumulative curve and A/B/C cutoffs  
- **Cohort analysis**: repeat-purchase curve by months since first purchase; **t=1 scenario slider** in HTML  
- **Churn prediction**: Random Forest scoring; key drivers; segment-level churn risk  
- **Recommendations & KPIs**: business priorities with a compact KPI set

## Visual Outputs

- RFM segment distribution (interactive bar: % on bars, counts on hover)  
- RFM heatmap (avg spend by R×F; tooltip shows R, F, avg €, customers, segment)  
- Pareto/ABC chart (interactive bars, smooth cumulative line, class markers)  
- Retention curve (interactive scenario explorer in HTML; static in PDF)  
- Churn probability by segment (bar chart with % labels)

## Project Structure

├─ sales_analysis_spain.Rmd
├─ sales_analysis_spain.html
├─ Pedidos.csv
├─ README.md

## Methods

- **RFM analysis**  
  - 1–5 scoring on Recency, Frequency, Monetary  
  - Segment distribution chart and R×F heatmap (interactive hover)

- **Pareto / ABC**  
  - Product ranking by sales with cumulative curve  
  - A/B/C class cutoffs and boundary markers

- **Cohort retention**  
  - Months since first purchase, overall repeat-purchase curve  
  - HTML scenario slider to adjust **t=1** and rescale the tail

- **Churn prediction**  
  - Random Forest using recency, frequency, tenure, gaps, 90-day sales, AOV, UPT  
  - Class balancing and threshold tuning by F1

- **Model evaluation & diagnostics**  
  - Accuracy, Precision, Recall, F1; variable importance  
  - Visuals: observed vs predicted, ROC (where applicable)

- **Recommendations & KPIs**  
  - Action plan and a compact KPI set for monthly review
 
## Key Results

- **RFM mix**  
  - Loyal ≈ **25%**, Champions ≈ **6%**, At Risk ≈ **24%**, Recent ≈ **16%**, Potential Loyalists ≈ **13%**, Hibernating + Big Spenders at Risk ≈ **16%** combined

- **Value concentration (R×F heatmap)**  
  - Highest average spend among **recent buyers with 1–2 purchases** (R≈4, F=1–2), **> €6,000**  
  - **Very recent second-order** (R≈5, F=2) underperforms, signaling a first-to-second dip  
  - **Older mid-frequency** (R≈1, F≈3) shows elevated spend → win-back opportunity

- **Pareto / ABC**  
  - A small **Class A** set drives the majority of revenue; protect stock and promo  
  - Long tail (Class C) adds complexity with limited return

- **Retention curve (cohorts)**  
  - **Month-one repeat ≈ 16%**, then stabilizes around **16–27%**  
  - The main challenge is converting the **first to the second** purchase

- **Churn model performance**  
  - Random Forest reached **Accuracy ≈ 0.95** and **F1 ≈ 1.00** at the optimal threshold  
  - **Recency** is the top driver; frequency and total sales follow; AOV/UPT are secondary

- **Priorities**  
  - Keep and grow recent high-value buyers; fix the first-to-second gap  
  - Raise basket size for repeat buyers (bundles, upgrades, thresholds)  
  - Reactivate at-risk and lapsed segments; focus on older mid-frequency spenders  
  - Center the mix on Class A; rationalize the tail  
  - Operationalize churn outreach after **60–90** days of inactivity and track a tight KPI set
## How to Run

```bash
git clone git@github.com:MarcoBoso/IKEA-RCMP-Analysis.git
cd costumer-value-analysis
