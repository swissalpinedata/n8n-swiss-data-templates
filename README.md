# n8n and Make templates: Swiss jobs, Zefix companies, Personio jobs and German jobs to Google Sheets

Ready to import n8n workflows (and Make scenario guides) that pull Swiss and DACH public data through Apify actors by [Swiss Alpine Data](https://apify.com/swissalpinedata) and write it to Google Sheets on a schedule. No community nodes needed.

## Full workflows

Complete templates with deduplication, filters, email reports, failure alerts and setup notes inside the workflow. Tested end to end on n8n Cloud.

### Find new Swiss companies from the Zefix and SHAB register as qualified B2B leads

Every weekday: new register entries for your cantons, filtered by legal form and keywords, new companies added to a Google Sheet, one email summary.

File: [`n8n/zefix-new-companies-b2b-leads.json`](n8n/zefix-new-companies-b2b-leads.json). Actor: https://apify.com/swissalpinedata/swiss-company-register-scraper

### Track hiring spikes from Personio, Workable, Recruitee and Teamtailor career sites

Every Monday: open jobs from your company watchlist, new ones stored in a Google Sheet, one report ranking companies by new openings.

File: [`n8n/ats-hiring-spike-tracker.json`](n8n/ats-hiring-spike-tracker.json). Actor: https://apify.com/swissalpinedata/eu-ats-jobs

### Get a daily email of new jobs from jobs.ch, jobup.ch, JobScout24 and job-room.ch

Every morning: your searches across four Swiss job boards, duplicates merged, jobs you already received skipped. No spreadsheet needed.

File: [`n8n/swiss-job-alert-email.json`](n8n/swiss-job-alert-email.json). Actor: https://apify.com/swissalpinedata/swiss-jobs-scraper

## Simple templates: setup

1. Get an Apify API token at https://console.apify.com/settings/integrations (free plan works).
2. In n8n create a Header Auth credential: name `Authorization`, value `Bearer YOUR_TOKEN`, and select it in the "Run Apify actor" node.
3. Create a Google Sheet with the column names from the "Pick columns" node in row 1, paste its URL into the Google Sheets node.
4. Change the input (keywords, cantons, companies) in the HTTP Request body. Each actor page lists all input fields.

## Simple templates

### New Swiss companies (Zefix, SHAB) to Google Sheets

Every weekday at 07:00 adds yesterday's new company registrations (SHAB HR01) in canton Zürich to a Google Sheet: name, UID, legal form, seat, address, purpose and capital. A ready B2B lead list of fresh GmbH and AG founders.

File: [`n8n/zefix-new-companies-to-google-sheets.json`](n8n/zefix-new-companies-to-google-sheets.json). Actor: https://apify.com/swissalpinedata/swiss-company-register-scraper

### Jobs from Personio, Workable, Recruitee, SmartRecruiters, Teamtailor career sites to Google Sheets

Every Monday at 08:00 collects all open jobs from a list of company career sites and upserts them into a Google Sheet keyed on the job URL, so new openings show up as new rows. Use it as a hiring signal tracker for sales or competitor monitoring.

File: [`n8n/personio-workable-jobs-to-google-sheets.json`](n8n/personio-workable-jobs-to-google-sheets.json). Actor: https://apify.com/swissalpinedata/eu-ats-jobs

### Swiss jobs from jobs.ch, jobup.ch, JobScout24, job-room.ch to Google Sheets

Every morning at 07:00 searches the four big Swiss job boards for one keyword and place and upserts the results into a Google Sheet keyed on the job URL.

File: [`n8n/swiss-jobs-to-google-sheets.json`](n8n/swiss-jobs-to-google-sheets.json). Actor: https://apify.com/swissalpinedata/swiss-jobs-scraper

### German jobs from the Arbeitsagentur Jobbörse to Google Sheets

Every morning at 07:00 fetches the jobs published in the last day on the Jobbörse of the Bundesagentur für Arbeit for one keyword and place, and upserts them into a Google Sheet.

File: [`n8n/arbeitsagentur-jobs-to-google-sheets.json`](n8n/arbeitsagentur-jobs-to-google-sheets.json). Actor: https://apify.com/swissalpinedata/arbeitsagentur-jobs-scraper

## Make

Step by step scenarios with the official Apify app in Make: [make/README.md](make/README.md).

## Code examples

Python, Node and curl examples for the same actors:

* [swiss-jobs-api](https://github.com/swissalpinedata/swiss-jobs-api)
* [arbeitsagentur-jobs-api](https://github.com/swissalpinedata/arbeitsagentur-jobs-api)
* [zefix-api-python](https://github.com/swissalpinedata/zefix-api-python)
* [austria-jobs-api](https://github.com/swissalpinedata/austria-jobs-api)
* [flatfox-api-python](https://github.com/swissalpinedata/flatfox-api-python)
* [personio-jobs-api](https://github.com/swissalpinedata/personio-jobs-api)

## License

MIT. The data comes from public sources; you are responsible for using it in line with the GDPR and the terms of the source sites.
