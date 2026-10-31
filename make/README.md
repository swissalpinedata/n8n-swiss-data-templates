# Make scenarios for Swiss and DACH data

Make has an official Apify app, so no blueprint import is needed. Build each scenario in about five minutes.

## New Swiss companies (Zefix, SHAB) to Google Sheets

1. New scenario. First module: Apify, **Run an Actor**. Connect your Apify account (API token from https://console.apify.com/settings/integrations).
2. Actor: `swissalpinedata/swiss-company-register-scraper`. Run synchronously: Yes.
3. Input JSON:
   `{"mode": "new-companies", "cantons": ["ZH"], "subRubrics": ["HR01"], "dateFrom": "{{formatDate(addDays(now; -1); "YYYY-MM-DD")}}", "maxItems": 500}`
4. Second module: Apify, **Get Dataset Items**, Dataset ID = `defaultDatasetId` from module 1.
5. Third module: Google Sheets, **Add a Row**. Map name, uid, legal_form, seat, canton, address, purpose, capital, url.
6. Schedule: every weekday at 07:00.

## Jobs from company career sites (Personio, Workable, Recruitee, SmartRecruiters, Teamtailor) to Google Sheets

Same three modules with actor `swissalpinedata/eu-ats-jobs` and input
`{"companies": ["https://ottonova.jobs.personio.de", "https://bunq.recruitee.com"], "includeDescription": false, "maxItems": 1000}`.
In Google Sheets use **Search Rows** on the url column first and a filter "Total number of bundles = 0" before **Add a Row**, so only new jobs are added. Schedule: weekly.

## Swiss jobs (jobs.ch, jobup.ch, JobScout24, job-room.ch) to Slack

Actor `swissalpinedata/swiss-jobs-scraper`, input `{"query": "python", "location": "Zürich", "maxItems": 50}`, then Slack, **Create a Message** with `{{title}} at {{company}}, {{location}}: {{url}}`. Schedule: daily.
