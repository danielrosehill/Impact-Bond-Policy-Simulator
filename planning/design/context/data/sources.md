# INDIGO Data Sources

**Import date**: 2024-12-24

Data sourced from the Government Outcomes Lab (GO Lab) INDIGO database.

---

## Current Data

```
data/
├── outcome-funds/
│   └── outcome-funds.csv           # Main outcome funds listing
├── pipelines/
│   └── pipelines.csv               # Pipeline projects
└── raw/
    ├── funds/
    │   ├── funds.csv
    │   ├── funds_documents.csv
    │   ├── funds_geographic_areas_for_outcome_payment.csv
    │   ├── funds_organisations.csv
    │   └── outcome-funds.csv
    ├── organizations/
    │   ├── organisations.csv
    │   ├── organisations_controlled_by.csv
    │   ├── organisations_org-idssecondary.csv
    │   └── organisations_sources.csv
    └── projects/
        ├── pipelines.csv
        ├── projects.csv
        ├── projects_delivery_locations.csv
        ├── projects_documents.csv
        ├── projects_intermediary_services.csv
        ├── projects_investments.csv
        ├── projects_outcome_funds.csv
        ├── projects_outcome_metrics.csv
        ├── projects_outcome_payer_cost.csv
        ├── projects_outcome_payment_commitments.csv
        ├── projects_outcome_payment_plans.csv
        ├── projects_outcome_payments.csv
        ├── projects_outcome_pricings.csv
        ├── projects_provider_side_cost.csv
        ├── projects_results.csv
        ├── projects_service_provisions.csv
        ├── projects_sources.csv
        ├── projects_technical_assistance_details.csv
        ├── projects_technical_assistances.csv
        └── projects_transactions.csv
```

---

## Download URLs

### Project Listings CSV
https://golab-indigo-data-store.herokuapp.com/app/project_download

### Organisation Listings CSV
https://golab-indigo-data-store.herokuapp.com/app/organisation_download

### Outcomes Fund Listings CSV
https://golab-indigo-data-store.herokuapp.com/app/fund_download

### All Data (CSV by data type)
https://golab-indigo-data-store.herokuapp.com/app/all_public_data_file_per_data_type_csv.zip

### API Access
https://golab-indigo-data-store.herokuapp.com/app/api1/project
https://golab-indigo-data-store.herokuapp.com/app/api1/organisation

### Data Dictionary
https://indigo-data-standard.readthedocs.io/en/latest/data-dictionary/index.html
