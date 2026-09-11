# CallMeMaybe — Telecom Operator Performance Analysis

A business-focused analysis of virtual telephony data designed to identify operators showing potential signs of low efficiency while separating true operator-performance signals from broader data-quality and routing issues.

## About the Project

CallMeMaybe is a virtual telephony service used by organisations to manage inbound and outbound calls.

The goal of this project was to create a transparent analytical framework for identifying operators who may require further investigation. A key challenge was ensuring that operators were not unfairly penalised for calls that could not be reliably attributed to them.

The project combines data cleaning, KPI development, exploratory analysis, sensitivity testing, statistical hypothesis testing, and dashboard reporting.

## Business Questions

The analysis focused on four main questions:

1. Which operators show consistent signs of lower operational efficiency?
2. How much of the missed-call problem can actually be attributed to identified operators?
3. Are waiting time and workload associated with missed-call performance?
4. Can a transparent and robust prioritisation framework support supervisors without turning the analysis into an automatic performance judgement?

## Tools & Technologies

- Python
- pandas
- NumPy
- Matplotlib
- SciPy
- Jupyter Notebook
- Tableau Public
- Statistical Analysis
- KPI Design
- Sensitivity Analysis

## Analysis Approach

The project followed six main stages:

1. **Data quality review** — checking data types, missing values, duplicates, and categorical distributions.
2. **Data preparation** — removing exact duplicates, standardising dates, and creating derived call metrics.
3. **Exploratory analysis** — reviewing call volume, missed-call rates, and waiting times.
4. **Operator KPI framework** — calculating inbound, outbound, waiting-time, activity, and profile metrics for each identified operator.
5. **Sensitivity and statistical testing** — testing the robustness of the classification and validating key relationships.
6. **Business communication** — exporting analysis-ready datasets and building an interactive Tableau dashboard.

## Key Findings

### Data quality matters before performance scoring

The original calls dataset contained **53,902 records**. After removing **4,900 exact duplicates**, the final analysis contained **49,002 records**, representing **806,709 calls**.

The most important finding was that **52.6% of inbound calls had no identified operator**.

Among those calls, the missed-call rate was **99.4%**. By comparison, inbound calls with an identified operator had a missed-call rate of only **1.0%**.

This means that a large share of missed inbound calls should not be attributed directly to individual operators.

### Operator prioritisation

The analysis evaluated **1,092 identified operators**.

Using the baseline criteria:

- **152 operators** were classified as **high priority**;
- **109 operators** were classified as **requiring attention**;
- **831 operators** showed **no current inefficiency signal** under the baseline rules.

The classification is intended to support supervisor investigation rather than automate disciplinary decisions.

### Classification robustness

I tested **324 different threshold scenarios** to understand how sensitive the classification was to the selected cut-offs.

The number of high-priority operators ranged from **89 to 223** across the scenarios.

Operators who remain flagged under many different parameter combinations represent stronger candidates for further review because their classification is less dependent on one specific threshold choice.

### Statistical tests

The statistical analysis identified several significant relationships, but the effect sizes were generally weak.

- **Waiting time vs missed-call rate:** Spearman correlation = **0.1215**, p = **0.0225**.
- **Inbound workload vs missed-call rate:** Spearman correlation = **0.1496**, p = **0.0049**.
- **Internal vs external inbound calls:** statistically significant difference in missed-call proportions, p < **0.001**.
- **Tariff plan vs client missed-call-rate distribution:** statistically significant difference, p = **0.000469**.

These results suggest that waiting time, workload, call type, and client segment can provide useful context, but none should be used alone to judge operator performance.

## Business Recommendation

The analysis supports a monitoring system that prioritises operators for further investigation while keeping data-quality issues separate from individual performance.

I recommend:

- maintaining separate alerts for operator performance and calls without an identified operator;
- using a transparent score based on missed-call rate, waiting time, and outbound activity where applicable;
- prioritising operators whose classification remains stable across multiple sensitivity scenarios;
- reviewing routing and call-assignment processes because missed calls are heavily concentrated in records without an identified operator;
- recalibrating thresholds when official service and productivity targets become available.

## Dashboard

The final Tableau dashboard brings the main KPIs and operator-level results together in an interactive view for supervisors and managers.

👉 **[View the CallMeMaybe dashboard on Tableau Public](https://public.tableau.com/views/CallMeMaybe-EficinciadosOperadores/CallMeMaybe-Dashboard?:language=pt-BR&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)**

The dashboard includes:

- total operators;
- high-priority operators;
- operators requiring attention;
- operators with no current inefficiency signal;
- priority distribution;
- waiting time vs missed-call rate;
- sensitivity-analysis robustness;
- detailed operator-level KPIs.

## Project Structure

```text
telecom-operator-performance-analysis/
│
├── README.md
├── notebook/
│   └── callmemaybe_operator_performance_analysis.ipynb
└── data/
    └── README.md
