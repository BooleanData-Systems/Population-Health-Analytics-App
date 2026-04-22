# Population Health Analytics

AI-powered clinical intelligence platform for population health management built natively on Snowflake Cortex.

## Overview

Analyze member risk, cost, utilization, care gaps, and outcomes across your entire population with interactive dashboards powered by Snowflake Cortex AI.

### Key Features

- **8 Analytics Tabs** — Overview, Risk, Cost, Utilization, Care Management, Cohort Builder, AI Insights, Help
- **30+ KPIs** — PMPM, ER rate, readmission rate, medication adherence, SDOH barriers, risk scores
- **HEDIS/NQF Measures** — HbA1c, BP monitoring, mammogram screening, wellness visits, medication adherence
- **Dynamic Filters** — Region, risk segment, payer, year — all cross-tab
- **AI Chat** — Ask questions about your population data using Snowflake Cortex (mistral-large2)
- **Custom Cohorts** — Build multi-criteria patient cohorts with instant KPI summaries
- **Work Lists** — High-risk outreach, ER diversion, urgent intervention lists with CSV export
- **Dark Mode** — Full light/dark theme toggle

## Setup

### Required Table References

After installing the app, bind six tables/views from your data layer.

#### 1. Member Demographics (Required)

| Column | Type | Description |
|--------|------|-------------|
| MEMBER_ID | VARCHAR | Unique member identifier |
| AGE | INT | Member age |
| AGE_GROUP | VARCHAR | Age bracket |
| GENDER | VARCHAR | Gender |
| REGION | VARCHAR | Geographic region |
| PAYER_NAME | VARCHAR | Insurance payer |
| PRIMARY_CONDITION | VARCHAR | Primary diagnosis |
| CHRONIC_CONDITION_COUNT | INT | Number of chronic conditions |
| RISK_SCORE | FLOAT | Composite risk score (0-100) |
| RISK_SEGMENT | VARCHAR | High/Rising/Low |
| CLINICAL_SEVERITY | VARCHAR | CRITICAL/AT_RISK/STABLE |
| TOTAL_COST | FLOAT | Total cost |
| ER_VISITS | INT | Emergency visits |
| READMISSIONS | INT | Hospital readmissions |
| AVG_MED_ADHERENCE | FLOAT | Medication adherence % |
| SDOH_RISK_FACTORS | INT | Social determinant risk factors |
| FOOD_INSECURITY | BOOLEAN | Food insecurity flag |
| HOUSING_INSTABILITY | BOOLEAN | Housing instability flag |
| TRANSPORTATION_BARRIER | BOOLEAN | Transportation barrier flag |
| SOCIAL_ISOLATION | BOOLEAN | Social isolation flag |
| IS_ACTIVE | BOOLEAN | Active member flag |

#### 2. Claims Data (Required)

| Column | Type | Description |
|--------|------|-------------|
| CLAIM_ID | VARCHAR | Claim identifier |
| MEMBER_ID | VARCHAR | Member identifier |
| SERVICE_MONTH | DATE | Service month |
| SERVICE_YEAR | INT | Service year |
| CLAIM_TYPE | VARCHAR | Claim type |
| CLAIM_STATUS | VARCHAR | APPROVED/DENIED/PENDING |
| PAID_AMOUNT | FLOAT | Paid amount |
| PAYER_NAME | VARCHAR | Payer name |
| MEMBER_REGION | VARCHAR | Member region |
| MEMBER_RISK_SEGMENT | VARCHAR | Risk segment |
| MEMBER_RISK_SCORE | FLOAT | Risk score |

#### 3. Encounters Data (Required)

| Column | Type | Description |
|--------|------|-------------|
| ENCOUNTER_ID | VARCHAR | Encounter identifier |
| MEMBER_ID | VARCHAR | Member identifier |
| ENCOUNTER_DATE | DATE | Encounter date |
| ENCOUNTER_MONTH | DATE | Encounter month |
| ENCOUNTER_YEAR | INT | Encounter year |
| ENCOUNTER_TYPE | VARCHAR | INPATIENT/EMERGENCY/OFFICE VISIT/WELLNESS VISIT |
| PROVIDER_SPECIALTY | VARCHAR | Provider specialty |
| LENGTH_OF_STAY | INT | Length of stay (days) |
| IS_READMISSION | BOOLEAN | Readmission flag |
| MEMBER_REGION | VARCHAR | Member region |
| MEMBER_RISK_SEGMENT | VARCHAR | Risk segment |

#### 4. Clinical Care Gaps (Required)

| Column | Type | Description |
|--------|------|-------------|
| GAP_ID | VARCHAR | Gap identifier |
| MEMBER_ID | VARCHAR | Member identifier |
| GAP_RULE | VARCHAR | HEDIS/NQF measure rule |
| GAP_CATEGORY | VARCHAR | Gap category |
| GAP_PRIORITY | VARCHAR | CRITICAL/WARNING/ROUTINE |
| DAYS_OVERDUE | INT | Days overdue |

#### 5. Outcome Tracking (Required)

| Column | Type | Description |
|--------|------|-------------|
| TRACKING_ID | VARCHAR | Tracking identifier |
| MEMBER_ID | VARCHAR | Member identifier |
| REGION | VARCHAR | Region |
| CURRENT_RISK_SEGMENT | VARCHAR | Current risk segment |
| PAYER_NAME | VARCHAR | Payer name |
| OUTCOME_TREND | VARCHAR | IMPROVING/STABLE/WORSENING |
| RISK_MIGRATION | VARCHAR | Migration direction |

#### 6. Interventions (Required)

| Column | Type | Description |
|--------|------|-------------|
| INTERVENTION_ID | VARCHAR | Intervention identifier |
| MEMBER_ID | VARCHAR | Member identifier |
| REGION | VARCHAR | Region |
| RISK_SEGMENT | VARCHAR | Risk segment |
| RISK_SCORE | FLOAT | Risk score |
| CLINICAL_SEVERITY | VARCHAR | Clinical severity |
| OPEN_CARE_GAPS | INT | Open care gaps |
| CRITICAL_CARE_GAPS | INT | Critical care gaps |
| RECOMMENDED_INTERVENTION | VARCHAR | Recommended intervention |
| ACTION_PLAN | VARCHAR | Action plan |
| ASSIGNED_TO | VARCHAR | Assigned care manager |
| PRIORITY_RANK | INT | Priority (1=highest) |

### Enable Cortex AI (Required)

Grant the Cortex user role via the **Permissions** tab in Snowsight.

## Privileges

| Privilege | Required | Purpose |
|-----------|----------|---------|
| Cortex User Role | Yes | Granted via Permissions tab |

## AI Features

All AI features use **Snowflake Cortex** (`COMPLETE` with `mistral-large2`). RAG-powered Q&A is grounded entirely in your population data. No external data is accessed.

## Data Privacy

- Data never leaves your account
- No data is copied, stored, or transmitted externally
- AI processing occurs entirely within Snowflake Cortex
- Only SELECT privileges requested

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-04 | Initial Marketplace release |
