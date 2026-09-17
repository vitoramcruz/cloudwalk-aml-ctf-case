# CloudWalk Payments Inc. — AML/CTF Monitoring Dashboard

> **Candidate:** Vitor Cruz | **Submission date:** 2026-08-24 | **Target role:** AML/CTF Analyst (US) — CloudWalk Payments Inc.
> Part of the CloudWalk AML/CTF technical case submission. See `MANIFEST_AND_SIGNATURES.pdf` (package root) for the SHA-256 checksum and digital signature covering this file.


A Streamlit dashboard over the tested CloudWalk AML case detection engine. It
ingests the analyst workbook, runs the 11-typology suspect engine and the EDD
population detector, and exposes portfolio KPIs, Plotly charts, an entity
drill-down, and a live threshold simulator.

## Files

| File                  | Purpose                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| `app.py`              | Streamlit UI: ingestion, KPIs, charts, drill-down, alert simulator.     |
| `detection_engine.py` | Importable detection engine. **The tested detection logic lives here.** |
| `requirements.txt`    | Pinned runtime dependencies.                                            |
| `README.md`           | This file.                                                             |

### `detection_engine.py` — what it is

`detection_engine.py` is the **importable extraction** of the two tested case
scripts, `Section4b_Typology_Analysis_Script.py` (11-typology engine) and
`Section2a_EDD_Customer_List_Analysis_Script.py` (EDD A–K detector). The
original scripts are monolithic run-on-import programs with hardcoded thresholds
and a fixed workbook path, so they cannot be imported or re-run with tuned
parameters. This module carries the **same detection logic and the same default
parameters** — the sliding-window anchor primitive, the 11 typologies, the
composite weight table, the diversification bonus, the OFAC regulatory-escalation
floor, and the EDD criteria — refactored into callable, parameterized functions.
Nothing was re-tuned. `app.py` imports from it and never re-implements detection.

The module self-validates against documented case facts:

- Populations reconciled to **501 customers / 100 merchants / 630 cards** (guards
  against the `openpyxl` blank-row padding artifact where `ws.max_row ≈ 999`).
- Portfolio chargeback ratio **≈ 0.73%**.
- EDD population **242 / 501**.
- Structuring band $980–995 → **104 in-band transactions**.
- Flagship device-sharing ring: **11** customers under the strict 60-minute
  window, **12** once the window is widened (66-minute end-to-end span).

## Quick start

```bash
# 1) create and activate a virtual environment (recommended)
python3 -m venv .venv
source .venv/bin/activate            # Windows: .venv\Scripts\activate

# 2) install dependencies
pip install -r requirements.txt

# 3) run
streamlit run app.py
```

Streamlit opens `http://localhost:8501` in your browser. Upload the AML workbook
(`.xlsx`) via the sidebar. If a file named `AMLFT_Analyst_JIM__1_.xlsx` sits next
to `app.py`, it is auto-loaded as a convenience for local development.

**Expected workbook sheets:** `Transactions`, `Customers_KYC`, `Merchants_KYB`,
`Cards` (column names as in the case dataset).

## What each section does

- **KPI header** — Total alerts (distinct customers with ≥1 typology hit), a
  false-positive-rate **proxy**, SARs filed (case-disposition input), and the
  portfolio chargeback ratio. The FPR shown is a monitoring-model proxy derived
  from the composite-score escalation cut, **not** a QA-validated disposition
  rate; a validated FPR requires case-management outcome labels.
- **Portfolio charts** — monthly alerting-transaction trend (stacked by
  typology), alerting-customers-by-typology breakdown, and risk-rating
  distribution (alerting customers vs. whole portfolio).
- **Entity drill-down** — pick a `customer_id` (ordered by suspicion rank) or
  `merchant_id` to see KYC/KYB context, triggered typologies with evidence, the
  entity's transactions, and a timeline scatter.
- **Alert simulator** — sliders for the structuring band / window / min-txns and
  the device-sharing window / min-customers / hard-block floor recompute those
  detectors against the in-session dataset in real time, with deltas against the
  case-default baseline.
- **EDD population** — the 242-customer EDD list with urgency, deadline and
  triggered criteria, filterable by urgency tier.

## Performance notes

- The full 11-typology run is cached (`@st.cache_data`) on the uploaded file's
  bytes, so it runs once per dataset; subsequent interactions are instant.
- The simulator uses lightweight single-typology recompute functions
  (`count_structuring_alerts`, `count_device_sharing_alerts`) so slider changes
  stay responsive without re-running the whole engine.

## Deploying beyond localhost

- **Streamlit Community Cloud:** push these files to a Git repo and point the app
  at `app.py`; it installs `requirements.txt` automatically.
- **Docker:** `pip install -r requirements.txt` then
  `streamlit run app.py --server.port 8501 --server.address 0.0.0.0`.
- **Internal server / headless:** add `--server.headless true` and put it behind
  your standard authenticated reverse proxy. Handle the workbook as regulated
  data; SAR confidentiality (31 U.S.C. § 5318(g)(2)) applies to any case handling
  downstream of this tool.
