# IRC Utility Operations Dashboard — V15 Client-Ready

Streamlit dashboard connected to the shared IRC Google Sheet.

## Main file path for Streamlit Cloud

```text
app.py
```

## Included pages

- Operations Command Center
- Exception Center
- Property Scorecard
- Geographic View
- Monthly Summary Report with one-page PDF export

## Important client-safe protections

This version is built so clients cannot browse raw spreadsheet data:

- No Data Explorer page
- No raw `st.dataframe` tables
- No CSV/Excel raw-data download
- No account number, meter number, due date, read period, previous reading, or current reading shown
- Monthly PDF export is summary-only
- Geographic map popups show summary information only

## Google Sheet

The repo is already configured to use:

```text
https://docs.google.com/spreadsheets/d/1_4coHOmEkzY9cLYRtqmnUJ51LuqeY6yz/edit?gid=910919948#gid=910919948
```

Reporting months are based on **Month + Year only**. Billing Date is not used for anomaly scoring, filters, trends, or missing-bill logic.

## Password

Default password in `config.py`:

```text
ChangeMeUtility2026!
```

For Streamlit Cloud, set this in app secrets instead:

```toml
APP_PASSWORD = "your-real-password"
```

## V15 changes

- Fixed percent-change colors by rendering inline HTML badges instead of relying on default Streamlit metrics.
- Green = favorable, red = unfavorable, yellow = watch, white = neutral/no comparison.
- Excludes properties/utilities from anomaly alerts when treatments are missing, zero, or not numeric.
- Keeps treatments as the driving force for anomaly detection.
- Fixed filter chip styling so “All” does not get cut off.
- Removed the unprofessional “Frozen Filters” label.
- Fixed title/header spacing so page titles are not cut off.
- Improved table/header spacing so labels like `Properties` and `Cost/Treatment` do not split awkwardly.
- Improved dark-mode contrast across legends, captions, filters, cards, and tables.
- Removed blank/empty card placeholders where practical.
- Added `Last Updated` at the bottom of the sidebar only.
- Keeps Latitude/Longitude support for exact map dots.

## Monthly email automation

This repo includes a GitHub Actions workflow:

```text
.github/workflows/monthly_report.yml
```

It can generate the one-page Monthly Summary PDF and email it monthly. It also has a manual **Run workflow** trigger.

Set these GitHub Secrets before relying on email delivery:

```text
REPORT_EMAIL_TO
REPORT_EMAIL_FROM
SMTP_USERNAME
SMTP_PASSWORD
SMTP_HOST      optional, defaults to smtp.gmail.com
SMTP_PORT      optional, defaults to 587
```

If email secrets are missing, the workflow still generates the PDF artifact and skips sending email.
