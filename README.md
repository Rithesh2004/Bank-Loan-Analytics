# Bank Loan Analytics

An end-to-end banking data analytics project focused on loan portfolio performance, repayment behaviour, credit risk indicators, and branch-level distribution.

**Author:** Danduri Rithesh  
**Project:** Banking Analytics — Group 1  
**Tools:** Microsoft Excel · MySQL Workbench · Tableau · Power BI

> This repository contains project documentation, SQL analysis queries, and aggregate dashboard previews. Raw workbooks, source datasets, and packaged BI files are intentionally not included in this public release because the supplied files contain client/customer names, account or client identifiers, dates of birth, demographic attributes, or embedded source data. Publish only properly anonymized or synthetic data and BI extracts.

## Project overview

The Bank Loan Analytics workstream examines the loan portfolio across clients, loan accounts, repayment summaries, branches, and loan products. The goal is to make portfolio totals, repayment performance, credit-risk flags, and branch distribution easier to monitor through SQL and interactive dashboards.

### Dataset scope

The project presentation records the following dataset counts:

| Dataset component | Records / entities |
|---|---:|
| Clients | 1,000 |
| Loan accounts | 2,000 |
| Repayment summaries | 2,000 |
| Branches | 180 |
| Loan products | 11 |

The uploaded loan fact CSV contains 2,000 rows and 49 columns. It includes client-related and demographic fields, so the raw file is not published in this repository.

## Workflow

1. **Data inspection** — review source tables, field types, date coverage, and key relationships.
2. **Data cleaning and preparation** — check missing values, trim whitespace, standardize dates, validate IDs, inspect duplicates, and validate financial fields.
3. **SQL analysis** — validate table counts and relationships, inspect loan status and repayment flags, and calculate portfolio KPIs.
4. **Dashboarding** — present portfolio totals, status mix, regional and product distribution, annual disbursement trends, and branch performance in Excel, Tableau, and Power BI.
5. **Business review** — document validation items that require confirmation before drawing operational conclusions.

## KPI framework

### Basic KPIs

| KPI | Definition used in the project |
|---|---|
| Total loan accounts | Count of records in `fact_loan` in the supplied SQL |
| Total loan amount disbursed | Sum of `Loan Amount` |
| Total funded amount | Sum of `Funded Amount` |

### Main KPIs

| KPI | Definition used in the project |
|---|---|
| Total repayments collected | Sum of `Total Pymnt` in `fact_repayment` |
| Loan default rate | Records flagged `Y` in `Is Default Loan` divided by all repayment records |
| Loan delinquency rate | Records flagged `Y` in `Is Delinquent Loan` divided by all repayment records |
| Principal recovery rate | Total principal received divided by total funded amount, multiplied by 100 |
| Loan distribution by branch | Distinct loan accounts and total loan amount grouped by `BranchID` and branch name |

**Interpretation note:** The SQL script currently uses `COUNT(*)` for Total Loan Accounts, although its comment describes unique accounts. Confirm whether `Account ID` is unique in the loaded fact table; if not, use `COUNT(DISTINCT \`Account ID\`)` to report distinct accounts. The supplied SQL also calculates default and delinquency rates using repayment records as the denominator. Keep that denominator explicit when comparing results across tools.

## Dashboard previews

### Excel dashboard
![Bank Loan Excel dashboard](screenshots/bank-loan-excel-dashboard.png)

### Power BI dashboard
![Bank Loan Power BI dashboard](screenshots/bank-loan-powerbi-dashboard.png)

### Tableau dashboard
![Bank Loan Tableau dashboard](screenshots/bank-loan-tableau-dashboard.png)

The screenshots are aggregate dashboard previews extracted from the Group 1 project presentation. The editable workbook files are not included in this public package because their embedded data has not been privacy-reviewed.

## SQL contents

`SQL/loan_validation_and_kpis.sql` includes:

- Database/table presence and record-count checks
- Missing-value checks
- Duplicate and unique-ID checks
- Date and financial-value validation
- Loan-to-client, product, branch, and repayment relationship checks
- Loan-status, default-flag, delinquency-flag, and repayment-behaviour distributions
- Three basic KPIs and five main KPIs

The client-level `INSERT` statements from the original SQL upload have been excluded from this public copy.

## Validation findings to investigate

The Group 1 presentation lists these checks as validation items, not confirmed data errors:

- Loan Status shows 206 default records, while the repayment table has 100 records flagged as default.
- 147 records marked `On-Time` carry a delinquency flag.
- 991 records have `Funded Amount` greater than `Loan Amount`.
- Missing age and date-of-birth values remain `NULL` until verified.

These items should be reconciled against source definitions and business rules before treating them as errors or making credit-risk recommendations.

## Repository structure

```text
Bank-Loan-Analytics/
├── README.md
├── SQL/
│   └── loan_validation_and_kpis.sql
├── screenshots/
│   ├── bank-loan-excel-dashboard.png
│   ├── bank-loan-powerbi-dashboard.png
│   └── bank-loan-tableau-dashboard.png
├── data/
│   └── README.md
└── docs/
    └── release-checklist.md
```

## How to use the SQL

1. Create or select the `bank_loan_analytics` database.
2. Import appropriately anonymized tables with the expected table and column names.
3. Open `SQL/loan_validation_and_kpis.sql` in MySQL Workbench.
4. Run the validation sections first.
5. Review the KPI definitions and confirm denominator/join logic before comparing with dashboard totals.

## Limitations

- The public repository does not include raw client-level datasets or packaged BI files.
- Dashboard screenshots are static previews and do not provide interactive filtering.
- KPI definitions are documented as implemented in the supplied project SQL and presentation; they should be validated with the business owner before operational use.

## Project credit

Banking Analytics — Group 1

- **Danduri Rithesh** — SQL queries and Excel-based analytical dashboards
- **A Vinitha Sree** — Dashboard development and project analysis
- **Vaibhav Dhananjay Kamble** — Interactive dashboards for debit and credit transaction analysis

---

If you use or adapt this project, retain appropriate attribution and ensure that any data you publish is anonymized and approved for public sharing.
