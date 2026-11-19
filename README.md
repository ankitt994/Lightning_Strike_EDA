# Lightning Strike Outlier Analysis (1987–2020)

## Project Overview

This project explores annual lightning-strike counts from 1987 to 2020 and demonstrates how statistical methods can be used to identify and investigate outliers.

The main focus is not simply to remove unusual values. It is to understand why an observation is unusual, investigate the underlying data where possible, and make a reasoned decision about how it should be handled.

## Objective

- Examine the distribution and range of annual lightning-strike counts.
- Summarize the data using the mean, median, quartiles, and interquartile range (IQR).
- Identify unusually low annual totals using the IQR method.
- Visualize annual strike counts and highlight the detected outlier year(s).
- Investigate the 2019 and 1987 records using their underlying date-level data.
- Compare the mean and median before and after excluding the low-end outlier observations.
- Document why an unusual value should be investigated before it is removed.

## Dataset

The repository contains three CSV files used at different stages of the analysis:

| File | Purpose |
|---|---|
| `eda_outliers_dataset1.csv` | Pre-aggregated annual lightning-strike totals used for the initial outlier analysis. |
| `eda_outliers_dataset2.csv` | Date-level records used to investigate the 2019 annual total. |
| `eda_outliers_dataset3.csv` | Date-level records used to investigate the 1987 annual total. |

The annual summary dataset contains the year and the corresponding number of lightning strikes. The two additional datasets provide date-level records to help investigate unusual annual totals.

## Tools and Libraries

- Python
- Pandas – data loading, date conversion, grouping, and filtering
- NumPy – numerical calculations
- Seaborn – boxplot visualization
- Matplotlib – annual scatterplot and chart formatting
- Jupyter Notebook – analysis workflow

## Analysis Workflow

1. **Load the annual summary data**  
   Read the pre-aggregated annual strike counts into a Pandas DataFrame.

2. **Explore the distribution**  
   Inspect the records and calculate the mean and median. Format large strike counts to make chart labels easier to read.

3. **Visualize the data**  
   Use a boxplot to examine the distribution and understand the quartiles and IQR. Plot annual strike totals on a scatterplot.

4. **Calculate IQR thresholds**  
   Calculate the first quartile (Q1), third quartile (Q3), and IQR:

   `IQR = Q3 - Q1`

   `Lower limit = Q1 - 1.5 × IQR`

   `Upper limit = Q3 + 1.5 × IQR`

   Values below the lower limit or above the upper limit are flagged as potential outliers by this rule. This notebook focuses on investigating unusually low annual totals.

5. **Investigate the unusual years**  
   Examine the date-level records for 2019 and 1987. Convert the date column to datetime, derive month information, and aggregate strike counts by month.

6. **Make a handling decision**  
   The notebook's monthly investigation indicates that the 2019 file contains records only for December, suggesting incomplete year coverage. The 1987 file contains records across all 12 months. These cases should not automatically receive the same treatment: incomplete coverage is a data-quality concern, while a complete year's unusual count may represent genuine variation and needs further context.

7. **Compare summary statistics**  
   Recalculate the mean and median after filtering out observations below the lower IQR limit, and compare them with the original statistics.

## Key Observations

- The IQR rule is used to flag unusually low annual strike totals.
- The 2019 date-level data appears to cover December only, so its annual total may be unusually low because the year is incompletely represented in the supplied file.
- The 1987 date-level data includes all 12 months. Its unusual annual total therefore requires a different interpretation from the apparent 2019 coverage issue.
- The analysis demonstrates that outliers can affect the mean more strongly than the median.
- An outlier is not automatically an error. It should be investigated using data coverage, context, and domain knowledge before deciding whether to exclude it.

## Important Interpretation Note

The IQR method identifies statistical outliers; it does not prove that a value is incorrect. In this project, the 2019 record is treated as a possible data-completeness issue based on the monthly coverage check. The 1987 record is not assumed to be erroneous simply because it is unusual.

The final filtered dataset is a comparison for understanding the effect of low-end observations. It should not be treated as a definitive corrected lightning dataset without additional source documentation and validation.

## Repository Contents

- `lightningstrike.ipynb` – Jupyter Notebook containing the analysis and visualizations.
- `lightningstrike.html` – HTML export of the notebook.
- `eda_outliers_dataset1.csv` – annual summary data.
- `eda_outliers_dataset2.csv` – date-level data used to investigate 2019.
- `eda_outliers_dataset3.csv` – date-level data used to investigate 1987.

## How to Run

1. Clone or download this repository.
2. Keep the notebook and all three CSV files in the same directory.
3. Install the required libraries:

   ```bash
   pip install pandas numpy seaborn matplotlib jupyter
   ```

4. Open Jupyter Notebook:

   ```bash
   jupyter notebook
   ```

5. Open `lightningstrike.ipynb` and run the cells from top to bottom.

## Further Improvements

- Add explicit data-quality checks for missing dates and month coverage.
- Record the exact annual totals, IQR thresholds, and before/after mean and median in the notebook's conclusion.
- Investigate the source and collection methodology for unusual years before making a final exclusion decision.
- Add a clear comparison chart of the original and filtered distributions.

## Project Takeaway

Outlier detection is only the first step. A useful analysis combines statistical identification, visual exploration, data-quality investigation, and careful interpretation before deciding how unusual observations should be handled.
