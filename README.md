AML/CTF Compliance System — End-to-End Technical Case
CloudWalk Payments Inc. · Non-bank payment processor · FinCEN-regulated · Sponsor-bank model

Author: Vitor Cruz Completed: August 2026 · This repository contains the full deliverables package I produced as part of CloudWalk’s AML/CTF Analyst (US) technical selection case. Every figure has been independently computed and verified against the master dataset.

🔍 What this project is

A complete, production-grade AML/CTF compliance program built from scratch over a synthetic but realistic dataset of 501 customers, 100 merchants, 630 cards, and 32,348 transactions spanning 252 days. The work covers the full BSA/AML program lifecycle — from risk assessment and KYC/KYB remediation through transaction monitoring, SAR filing, regulator engagement, new product risk assessment, and AI-assisted workflow design.

The centerpiece is a Python detection engine that scores every customer across 11 independent typologies and surfaces the most suspicious accounts for investigation. A Streamlit dashboard wraps it with an interactive UI, live alert simulator, and entity drill-down. The SQL layer provides 12 parameterized PostgreSQL detection queries deployable in a real case-management environment.

🚨 Key Findings
Finding Detail
Money mule ring uncovered 12 coordinated accounts on a single device (dev_shared_4829) and single IP (45.129.55.210), executing $9,664.92 in scripted remittances at MCC 4829 in a 66-minute session
SAR filed FinCEN Form 111 (Initial), 12 subjects, $82,226.25 aggregate throughput — money laundering + suspicious use of multiple accounts + cyber indicators
Top 10 alerts worked 9 recommended to file, 1 escalated for OFAC-nexus review
EDD population 242 of 501 customers (48.3%) flagged across criteria A–K
Structuring detected 104 transactions in the $980–$995 band across the review period
Chargeback outlier Merchant M3030 (ElectroHub #330) at 12.0% vs. 0.73% portfolio baseline
OFAC escalation 1 customer with sanctions-match score above regulatory floor, guaranteed top-5 placement independent of composite score

📁 Repository Structure
├── app.py # Streamlit dashboard (UI layer)
├── detection_engine.py # 11-typology detection engine (importable)
├── requirements.txt # Python dependencies
├── Section2a_EDD_Customer_List_Analysis_Script.py # EDD population detector (criteria A–K)
├── Section4a_SQL_Detection_Queries.sql # 12 parameterized PostgreSQL alert rules
├── Section4a_T10_SelfMerchant_Correction_Script.py # T10 three-tier match model
├── Section4b_Typology_Analysis_Script.py # 11-typology composite scoring engine
├── Section4b_Suspect_Timeline_Script.py # SAR evidence: timelines + relationship network
├── dashboard_click_to_open.html # Static dashboard — open directly in browser
├── Section1a_AML_CTF_Risk_Assessment.pdf # Risk matrix and inherent/residual scoring
├── Section1b_AML_Program_Updates.pdf # Proposed program updates (9 sections)
├── Section2b_EDD_Remediation_Customer_C88888.pdf # Individual EDD remediation — OFAC-nexus customer
├── Section2b_KYB_Remediation_Merchants_M3004_M3025.pdf
├── Section2b_UBO_Critical_Case_Report.pdf
├── Section3_Suspicious_Activity_Report_SAR.pdf # Filed SAR — FinCEN Form 111 format
├── Section4b_Casework_Narratives_Top10_Alerts.pdf # Regulator-ready Five-Ws narratives
├── Section4c_Investigation_SLA_QA_Metrics.pdf # SLA tiers, QA framework, precision/recall
├── Section5_OCT_Crypto_OnRamp_Risk_Assessment.pdf # Pre-launch risk assessment (new products)
├── Section6a_FinCEN_Information_Request_Response.pdf
├── Section7_LLM_AI_Workflows.pdf # LLM-assisted SAR drafting + alert triage proposal
├── Reasoning_and_Methodology_CloudWalk_AML.pdf # Problem → Hypotheses → Test → Decision
├── Final_Presentation_Board_Examiner_Briefing.pdf
├── Section2a_EDD_Customer_List.xlsx # 242-customer EDD population
├── Section2b_UBO_Screening_Data_AllMerchants.xlsx # UBO screening, all 100 merchants
├── Section4b_Typology_Analysis_Full_Dataset.xlsx # Full typology hit table (421 customers)
├── Section4b_Suspect_Timeline_PreSAR.xlsx # Minute-by-minute timeline, top 3 subjects
├── SAR_Evidence_Package_Top3.xlsx # SAR evidence package — C12105, C12451, C12373
└── AML_KPI_Dashboard_Board_and_Examiner.xlsx # KPI dashboard for board and examiner review

🛠️ Tech Stack
Layer Tools
Detection engine Python 3 · pandas · sliding-window anchor pattern
Dashboard Streamlit · Plotly
SQL rules PostgreSQL 16 · parameterized CTEs
Data openpyxl · Excel workbooks
Reporting PDF (regulatory format) · FinCEN Form 111
AI/LLM layer Workflow design: extractive summarization for SAR narrative drafting + Tier-1 alert triage

⚡ Quick Start — Interactive Dashboard
bash

1. Clone the repository
git clone https://github.com/YOUR_USERNAME/cloudwalk-aml-ctf-case.git
cd cloudwalk-aml-ctf-case

2. Create and activate a virtual environment
python3 -m venv .venv
source .venv/bin/activate # Windows: .venv\Scripts\activate

3. Install dependencies
pip install -r requirements.txt

4. Run
streamlit run app.py

Upload AMLFT_Analyst_JIM.xlsx via the sidebar. The dashboard loads the full dataset and runs all 11 typologies automatically.

No install needed? Open dashboard_click_to_open.html directly in any browser — it’s a static snapshot with all computed numbers already embedded.

📋 Full Deliverables by Section
Section 1 — AML/CTF Program & Framework
Inherent and residual risk matrix across all applicable risk categories
Proposed AML program updates across 9 program components (BSA Officer, training, independent testing, recordkeeping, transaction monitoring, CIP/CDD/EDD, KYB/UBO, new products, regulator engagement)
Section 2 — KYC / KYB / CDD / EDD
EDD population: 242/501 customers across criteria A–K (PEP, high-risk jurisdiction, high-risk MCC, chargeback outlier, sanctions proximity, structuring, IP ring, device sharing, cash-in/out, geo-hopping, UBO jurisdiction)
Individual EDD remediation narratives: Customer C88888 (OFAC-nexus), Merchants M3004 and M3025
UBO screening across all 100 merchants; critical case report
Section 3 — Suspicious Activity Report
Complete SAR in FinCEN Form 111 format (Initial filing)
12 subjects · $82,226.25 aggregate · 66-minute coordinated session
FinCEN Part II category selections with evidentiary basis per item
Section 4 — Transaction Monitoring & Investigations
4a: 12 parameterized SQL detection queries (PostgreSQL); sliding-window anchor pattern; one-line threshold recalibration via params CTE
4b: 11-typology Python detection engine with composite scoring, diversification bonus, and OFAC regulatory-escalation floor; top-10 casework narratives (Five-Ws, counterparties, fund flows, SAR rationale)
4c: Three-tier investigation SLA framework (P1/P2/P3), QA sampling methodology, precision/recall measurement cycle
Section 5 — New Product Risk Assessment
Pre-launch risk assessment: OCT instant payouts + crypto on-ramp
Risk domains: money transmission licensing, OFAC screening at origination, chargeback/fraud velocity, blockchain analytics integration
Section 6 — Regulator Engagement & Reporting
FinCEN 314(a) information request response
KPI dashboard for board and examiner consumption
Section 7 — AI / LLM Automation
Workflow 1: LLM-assisted SAR narrative auto-draft (extractive, source-anchored)
Workflow 2: Tier-1 alert triage summarization
Governance controls, human-in-the-loop requirements, Lead Bank approval framework

📌 Notes
All data in this repository is synthetic — generated for the selection case. No real customer, merchant, or financial data is present.
SAR-related documents are marked confidential under 31 U.S.C. § 5318(g)(2) as a formatting convention reflecting real-world SAR confidentiality requirements. No real SAR has been filed.
The detection engine self-validates against documented case facts on every run (population counts, chargeback ratio, EDD count, structuring band count).

📬 Contact - Vitor Cruz · LinkedIn · Email
