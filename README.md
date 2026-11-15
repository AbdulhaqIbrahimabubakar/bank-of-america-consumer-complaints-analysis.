Bank of America Consumer Complaint Patterns & Response Trends (2017–2023)

 Project Overview
This repository contains an exploratory data analysis (EDA) and statistical hypothesis-testing investigation of 62,516 
Consumer Financial Protection Bureau (CFPB) consumer complaint records associated with Bank of America 
between 1 May 2017 and 28 August 2023.

Developed as part of the AnalystLab Africa Internship (Data Science Track), this project establishes a validated 
analytical baseline covering complaint volume dynamics, high-friction financial products, recurring consumer issues, 
CFPB complaint-forwarding intervals, and recorded company response outcomes.

Analytical Guardrail: A logged complaint represents an issue reported by a consumer and does not establish regulatory misconduct
or legal fault. All findings reflect statistical patterns and associations within the supplied dataset.


Research Questions & Hypotheses Investigated
1. Annual Complaint Volume: Did complaint volumes differ significantly across complete reporting years (`2018–2022`)?
2. Product Concentration: Are certain financial product categories associated with disproportionately higher complaint volumes?
3. CFPB Forwarding Lag: Do complaint-forwarding intervals (`Date received` minus `Date submitted`)
4. vary significantly across financial product categories?
5. Issue vs. Response Outcome: Are reported consumer issues statistically associated with specific company response categories?
6. Temporal Stability of Responses: Have recorded company response distributions changed significantly across full reporting years (`2018–2022`)?


Data Preparation & Quality Assurance
Before running exploratory or inferential analyses, the dataset underwent a 10-step validation protocol:
* Raw Data Preservation: Maintained an unaltered copy (`raw_df`) alongside a working analytical copy (`df`).
* Uniqueness & Deduplication: Verified `Complaint ID` uniqueness across all **62,516** records and checked for exact duplicate rows.
* Missing Value Handling: Retained full complaint volume integrity by imputing `"Not Specified"` for optional missing categorical
  sub-fields (`Sub-product`, `Sub-issue`, `State`, `ZIP code`).
* Date Validation & Feature Engineering: Parsed date fields to `datetime64`, confirmed the `2017-05-01` to `2023-08-28` boundary,
  and engineered `forwarding_days`, `Year`, `Month`, and `YearMonth`.
* Text Standardisation: Trimmed leading/trailing whitespace across categorical columns to prevent artificial category splitting.

Key Statistical Findings

| Research Question | Statistical Method | Test Statistic & P-Value | Practical Effect & Interpretation |

1. Annual volume differences (`2018–2022`) | Chi-Square Goodness-of-Fit | `χ² = 2,421.33` (`p < 0.0001`) | +82.8% surge from `7,075` (2019) to `12,936` (2022). |
2. Product volume concentration | Chi-Square Goodness-of-Fit | `χ² = 81,593.51` (`p < 0.0001`) | Highly concentrated: Top 3 products drive 77.93% of volume. |
3. Forwarding lag across products | Kruskal-Wallis H-Test | `H = 1,484.26` (`p < 0.0001`) | Small practical effect (`ε² = 0.0237`); 75%+ route in 0 days. |
4. Reported issues vs. company response | Chi-Square Independence | `χ² = 5,904.41` (`p < 0.0001`) | Small-to-moderate effect (`V = 0.1892`); issue type shapes relief outcomes. |
5. Response mix over time (`2018–2022`) | Chi-Square Independence | `χ² = 221.29` (`p = 1.28e-40`) | Negligible shift (`V = 0.0392`); resolution mix stayed consistent. |

Executive Highlights
* Retail Deposit & Card Concentration: Checking or savings accounts (`24,814` | `39.69%`) and Credit or prepaid cards (`16,197` | `25.91%`) generate nearly two-thirds of all complaints, followed by Credit reporting (`7,710` | `12.33%`).
* Primary Surge Driver: Monthly complaint volume spiked from ~1,200 to ~1,800 complaints/month, driven primarily by Checking or savings account complaints.
* Top Reported Consumer Issue: Managing an account accounts for 24.17% (`15,109` records) of all complaints across the dataset, followed by Incorrect information on your report (`7.89%`) and Problem with a purchase shown on your statement (`7.06%`).
* Near-Instant Electronic Forwarding: The CFPB forwards most complaints to Bank of America on the same day (`Median = 0.0 days`, `IQR = 0.0 days`, `90th percentile = 2.0 days`), though extreme right-skewed outliers reach `275 days` (`Mean = 1.22 days`, `Skewness = 11.76`).
* Dominant Company Response: Over 40,000 complaints were closed with written explanation alone, and resolution outcomes depend substantially more on the reported issue type (`Cramér's V = 0.1892`) than on the reporting year (`Cramér's V = 0.0392`).

Limitations & Analytical Caveats
* Absence of Customer Base Denominators: Higher complaint counts in deposit accounts and credit cards reflect both product friction and Bank of America's large active retail customer base relative to niche products.
* Partial Boundary Years: Records begin on 1 May 2017 and end on 28 August 2023; raw annual counts for 2017 and 2023 understate full-year activity and were excluded from annual statistical comparisons.
* Missing Closure Timestamps & Narratives: The dataset captures CFPB-to-company forwarding lag rather than internal bank investigation turnaround times, monetary relief dollar figures, or free-text consumer narratives.

How to Reproduce This Analysis
1. Clone the repository:
   ```bash
   git clone https://github.com<your-username>/bofa-consumer-complaints-analysis.git
   cd bofa-consumer-complaints-analysis

2. Install required dependencies:
   ```bash
   pip install -r requirements.txt

3. Open `notebooks/01_eda_and_statistical_analysis.ipynb` in Jupyter Notebook or JupyterLab and select **Run All Cells**.

Tech Stack
* Python 3 (`pandas`, `numpy`, `scipy`, `matplotlib`, `seaborn`)
