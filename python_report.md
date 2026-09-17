# Python Scripts QA Report

## ✅ Section2a_EDD_Customer_List_Analysis_Script.py — PASS
```

Total customers triggering >= 1 EDD criterion: 242 of 501

Validation — C88888 in EDD population: True
Validation — VE customers in EDD population: 2 (expect 2)
Validation — blocked+PEP customers in EDD population: 4
Validation — Criterion K population (K in codes): 214 (playbook cites 214 dataset-wide)

Urgency breakdown:
urgency
MEDIUM    223
HIGH       14
URGENT      5
Name: count, dtype: int64

Full EDD population: 242
Priority (URGENT+HIGH) case file: 19

Top 10 priority cases:
  customer_id              full_name country urgency criteria_codes
0      C88888  Mohammad Reza Al-Sana      US  URGENT  A, E, F, I, K
1      C12380             Jordan Lee      US  URGENT  B, D, F, J, K
2      C12427            Casey Smith      US  URGENT           B, J
3      C12183           Hayden Davis      US  URGENT           B, J
4      C12470        Parker Martinez      US  URGENT           B, J
5      C12100           Jordan Lopez      US    HIGH        B, F, K
6      C12480            Riley White      VE    HIGH        C, H, K
7      C12456         Quinn Martinez      US    HIGH           B, K
8      C12282        Riley Rodriguez      US    HIGH              B
9      C12201          Rowan Jackson      US    HIGH        B, F, K
```

## ✅ Section4b_Typology_Analysis_Script.py — PASS
```
  * 16 txns in $980.0-$995.0 band within 7 days (MCCs [4829, 6051]); total $15,833.59
  * 13 high-risk-MCC cross-border txns (20% of their high-risk-MCC activity is cross-border), $4,216.32 across ['AE', 'BR', 'CA', 'GB']
  * 8 KEYED (no-3DS) ECOM txns at high-risk MCC merchants over the dataset period (2 cross-border), $1,429.60 total -- DOUBLE RISK (no-auth + cross-border)
  Key txns: T301859, T303646, T305458, T308287, T309374, T313775

--- C12100 (Jordan Lopez) | score 62.7 | typologies: T04_GEO_HOPPING_XBORDER, T05_PEP_HIGH_RISK_MCC, T06_ECOM_NO_3DS ---
  * 8 high-risk-MCC cross-border txns (22% of their high-risk-MCC activity is cross-border), $1,199.53 across ['AE', 'CA', 'GB']
  * PEP customer: 28 txn(s) at high-risk MCC merchants exceeding 2x expected ticket (max 25.4x), $5,728.31 total
  * 11 KEYED (no-3DS) ECOM txns at high-risk MCC merchants over the dataset period (3 cross-border), $1,158.14 total -- DOUBLE RISK (no-auth + cross-border)
  Key txns: T300568, T302016, T302664, T302720, T304161, T305322

======================================================================
EXPORTING EXCEL WORKBOOK
======================================================================
  Wrote Summary, Top10_Customers, Top30_Transactions
  Wrote T01_Structuring (6 rows)
  Wrote T02_Card_Testing (8 rows)
  Wrote T03_Device_Sharing (2 rows)
  Wrote T04_Geo_Hopping_XBorder (342 rows)
  Wrote T05_PEP_High_Risk_MCC (341 rows)
  Wrote T06_ECOM_No_3DS (297 rows)
  Wrote T07_Chargeback_Outlier (1 merchant rows + 44 customer-link rows)
  Wrote T08_Cash_In_Cash_Out (1 rows)
  Wrote T09_IP_Ring (1 rows)
  Wrote T10_Self_Merchant (189 rows)
  Wrote T11_FATF_OFAC_Jurisdiction (42 rows)
  Wrote Full_Ranked_Customers (421 rows)

Saved workbook: /home/runner/work/cloudwalk-aml-qa/cloudwalk-aml-qa/qa_workspace/outputs/AML_Suspect_Detection_Results.xlsx
Sheets: ['Summary', 'Top10_Customers', 'Top30_Transactions', 'T01_Structuring', 'T02_Card_Testing', 'T03_Device_Sharing', 'T04_Geo_Hopping_XBorder', 'T05_PEP_High_Risk_MCC', 'T06_ECOM_No_3DS', 'T07_Chargeback_Outlier', 'T08_Cash_In_Cash_Out', 'T09_IP_Ring', 'T10_Self_Merchant', 'T11_FATF_OFAC_Jurisdiction', 'Full_Ranked_Customers']
```

## ✅ Section4b_Suspect_Timeline_Script.py — PASS
```
  Emerson Anderson | country: CA | risk_rating: low | PEP: False | KYC level: standard
  Total transactions: 97 | Period: 2025-03-05 02:44:53+00:00 to 2025-11-06 11:56:17+00:00
  Flagged transactions: 32 of 97
  Distinct customers linked via shared device: 11
  Distinct customers linked via shared IP: 11
  Merchants shared with the other 2 target customers: 54 total (40 at high-risk MCC merchants -- the operationally relevant overlap)
  Actual monthly volume: $1,174.74 vs expected $8,877.66 (-87%)
  Actual avg ticket: $97.87 vs expected $28.54 (+243%)

======================================================================
CUSTOMER #3: C12373
======================================================================
  Drew Smith | country: US | risk_rating: low | PEP: False | KYC level: standard
  Total transactions: 108 | Period: 2025-03-02 13:59:58+00:00 to 2025-11-06 18:25:45+00:00
  Flagged transactions: 30 of 108
  Distinct customers linked via shared device: 11
  Distinct customers linked via shared IP: 11
  Merchants shared with the other 2 target customers: 52 total (37 at high-risk MCC merchants -- the operationally relevant overlap)
  Actual monthly volume: $1,329.52 vs expected $10,847.05 (-88%)
  Actual avg ticket: $100.70 vs expected $12.72 (+692%)

======================================================================
EXPORTING EXCEL WORKBOOK
======================================================================
  Wrote Timeline_C12105 (101 rows, 29 flagged)
  Wrote Timeline_C12451 (97 rows, 32 flagged)
  Wrote Timeline_C12373 (108 rows, 30 flagged)

Saved workbook: /home/runner/work/cloudwalk-aml-qa/cloudwalk-aml-qa/qa_workspace/outputs/SAR_Evidence_Package_Top3.xlsx
Sheets: ['Summary', 'Timeline_C12105', 'Timeline_C12451', 'Timeline_C12373', 'Relationship_Network', 'CDD_Profile_Analysis']
```

## ✅ TASK_7_4_Self_Merchant_Correction.py — PASS
```
  * 16 txns in $980.0-$995.0 band within 7 days (MCCs [4829, 6051]); total $15,833.59
  * 13 high-risk-MCC cross-border txns (20% of their high-risk-MCC activity is cross-border), $4,216.32 across ['AE', 'BR', 'CA', 'GB']
  * 8 KEYED (no-3DS) ECOM txns at high-risk MCC merchants over the dataset period (2 cross-border), $1,429.60 total -- DOUBLE RISK (no-auth + cross-border)
  Key txns: T301859, T303646, T305458, T308287, T309374, T313775

--- C12100 (Jordan Lopez) | score 62.7 | typologies: T04_GEO_HOPPING_XBORDER, T05_PEP_HIGH_RISK_MCC, T06_ECOM_NO_3DS ---
  * 8 high-risk-MCC cross-border txns (22% of their high-risk-MCC activity is cross-border), $1,199.53 across ['AE', 'CA', 'GB']
  * PEP customer: 28 txn(s) at high-risk MCC merchants exceeding 2x expected ticket (max 25.4x), $5,728.31 total
  * 11 KEYED (no-3DS) ECOM txns at high-risk MCC merchants over the dataset period (3 cross-border), $1,158.14 total -- DOUBLE RISK (no-auth + cross-border)
  Key txns: T300568, T302016, T302664, T302720, T304161, T305322

======================================================================
EXPORTING EXCEL WORKBOOK
======================================================================
  Wrote Summary, Top10_Customers, Top30_Transactions
  Wrote T01_Structuring (6 rows)
  Wrote T02_Card_Testing (8 rows)
  Wrote T03_Device_Sharing (2 rows)
  Wrote T04_Geo_Hopping_XBorder (342 rows)
  Wrote T05_PEP_High_Risk_MCC (341 rows)
  Wrote T06_ECOM_No_3DS (297 rows)
  Wrote T07_Chargeback_Outlier (1 merchant rows + 44 customer-link rows)
  Wrote T08_Cash_In_Cash_Out (1 rows)
  Wrote T09_IP_Ring (1 rows)
  Wrote T10_Self_Merchant (189 rows)
  Wrote T11_FATF_OFAC_Jurisdiction (42 rows)
  Wrote Full_Ranked_Customers (421 rows)

Saved workbook: /home/runner/work/cloudwalk-aml-qa/cloudwalk-aml-qa/qa_workspace/outputs/AML_Suspect_Detection_Results.xlsx
Sheets: ['Summary', 'Top10_Customers', 'Top30_Transactions', 'T01_Structuring', 'T02_Card_Testing', 'T03_Device_Sharing', 'T04_Geo_Hopping_XBorder', 'T05_PEP_High_Risk_MCC', 'T06_ECOM_No_3DS', 'T07_Chargeback_Outlier', 'T08_Cash_In_Cash_Out', 'T09_IP_Ring', 'T10_Self_Merchant', 'T11_FATF_OFAC_Jurisdiction', 'Full_Ranked_Customers']
```


**Summary: 4/4 scripts passed**
