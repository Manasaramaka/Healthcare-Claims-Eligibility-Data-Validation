# Healthcare Claims & Eligibility Data Validation

> SQL-based data validation project simulating pre-migration UAT checks for a healthcare payer system — covering claims, eligibility, provider, and member data integrity.

---

## Project Overview

A healthcare payer is migrating claims and eligibility data into a new system. Before go-live, the Business Analyst must validate that all records migrated correctly, business rules are enforced, and no data integrity gaps exist.

This project replicates that validation process end-to-end:
- Identify bad or missing records
- Validate business rules across datasets
- Reconcile record counts
- Document UAT findings
- Produce an executive summary of data quality issues

---

## Business Context

This is the core pre-migration validation work that healthcare organizations require before any system go-live. A Business Analyst in this environment is responsible for ensuring claims, eligibility, provider, and member data is accurate, complete, and rule-compliant before production cutover.

---

## Dataset Structure

Four CSV files simulate a payer's core operational data:

| File | Key Fields |
|---|---|
| `members.csv` | Member_ID, Name, DOB, Plan_Type, Effective_Date |
| `eligibility.csv` | Member_ID, Eligibility_Start, Eligibility_End, Status |
| `providers.csv` | Provider_ID, Specialty, State |
| `claims.csv` | Claim_ID, Member_ID, Provider_ID, DOS, Amount, Status |

100–200 rows per file with intentionally seeded data quality issues for validation testing.

---

## Validation Rules

| Rule | Description |
|---|---|
| Rule 1 | Claim member must exist in Members table |
| Rule 2 | Claim date of service (DOS) must fall within active eligibility period |
| Rule 3 | Provider on claim must exist in Providers table |
| Rule 4 | No duplicate Claim_IDs |
| Rule 5 | Claim amount must be greater than $0 |
| Rule 6 | Member eligibility status must be Active at time of claim |

---

## Deliverables

### 1. `validation_queries.sql`
SQL scripts for each validation rule:
- Missing or unmatched member records
- Claims outside eligibility window
- Invalid or missing provider references
- Duplicate claim detection
- Zero or negative claim amounts
- Inactive member status at time of claim

### 2. `uat_findings.md` — UAT Test Case Summary

| Test Case | Records Checked | Issues Found | Result |
|---|---|---|---|
| Member Exists in Members Table | 200 | 4 | ❌ Fail |
| Eligibility Window Validation | 200 | 11 | ❌ Fail |
| Provider Reference Validation | 200 | 2 | ❌ Fail |
| Duplicate Claim ID Check | 200 | 0 | ✅ Pass |
| Claim Amount > $0 | 200 | 3 | ❌ Fail |
| Active Member Status at DOS | 200 | 7 | ❌ Fail |

### 3. `executive_summary.pdf` — 1-Page Leadership Report

| Metric | Value |
|---|---|
| Total Records Reviewed | 200 claims |
| Validation Rules Applied | 6 |
| Total Issues Identified | 27 |
| High Severity Issues | 15 |
| Pass Rate | 78.5% |

Includes recommendations for remediation before system go-live.

---

## Repository Structure

```
Healthcare-Claims-Eligibility-Validation/
│
├── data/
│   ├── members.csv
│   ├── eligibility.csv
│   ├── providers.csv
│   └── claims.csv
│
├── sql/
│   └── validation_queries.sql
│
├── findings/
│   ├── uat_findings.md
│   └── executive_summary.pdf
│
└── README.md
```

---

## Tools Used

| Tool | Purpose |
|---|---|
| SQL (SQLite / PostgreSQL) | Data validation queries |
| Excel / CSV | Dataset creation and review |
| Markdown | UAT findings documentation |
| PDF | Executive summary reporting |

---

## Skills Demonstrated through this project

- Healthcare claims and eligibility data analysis
- SQL-based business rule validation and reconciliation
- UAT planning, test case execution, and defect documentation
- Pre-migration data quality assessment
- Executive reporting and findings communication
- Cross-dataset joins across member, provider, eligibility, and claims tables
- Digital Transformation / Platform Migration BA
- Salesforce / Healthcare CRM BA
