# CMG Shares Outstanding (SEC XBRL) Web App

## Overview
This lightweight, single-page web app fetches the SEC XBRL concept EntityCommonStockSharesOutstanding for Chipotle Mexican Grill (CMG, CIK 0001058090), filters entries where:
- fy > 2020, and
- val is numeric,

then computes the maximum and minimum values among those filtered entries.

It displays the results on the page and allows you to download a data.json file containing:
- entityName
- max { fy, val }
- min { fy, val }

The title and H1 dynamically reflect the SEC entityName for CMG.

Note on User-Agent: Per SEC guidance, API requests should include a descriptive User-Agent. Browsers do not allow setting the User-Agent header directly from client-side JavaScript, which can lead to CORS or policy-related failures. This app:
- Attempts a direct fetch (often works).
- Provides a “curl” fallback with a proper User-Agent.
- Lets you paste the fetched JSON for processing if the browser request fails.

## Setup
No build steps are required.

- index.html is a self-contained app (HTML/CSS/JS inline).
- Simply open index.html in a modern browser.

Optional: For best reliability and compliance with SEC guidance, serve this page from a simple static server:
- Python: python3 -m http.server 8000
- Node (http-server): npx http-server -p 8000

Then navigate to http://localhost:8000.

## Usage
1. Open index.html.
2. The app will automatically attempt to fetch:
   https://data.sec.gov/api/xbrl/companyconcept/CIK0001058090/dei/EntityCommonStockSharesOutstanding.json
3. On success, you will see:
   - A title and H1 showing the SEC entityName.
   - Highest and lowest numeric values (FY > 2020) for shares outstanding.
   - A “Download data.json” button to save the results.
4. If the fetch fails (CORS/User-Agent restrictions):
   - Click “Copy curl command”.
   - Run the curl command in your terminal; it includes a descriptive User-Agent, as required by SEC guidance.
   - Paste the resulting JSON into the provided textarea.
   - Click “Process pasted JSON” to compute stats and enable the data.json download.

Notes:
- Filtering strictly uses fy > 2020 (i.e., 2021 and later) with numeric val entries.
- The app computes min/max across all filtered units.shares rows without deduplicating per fiscal year.

## Round 2
N/A (This is Round 1).