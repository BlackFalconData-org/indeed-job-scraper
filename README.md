# Indeed Job Scraper

Extract structured job listings from Indeed across 62 markets with built-in change tracking for recurring monitoring.

**[Indeed Job Scraper on Apify →](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi)**

---

## Key features






**Search with filters** — Search by keyword and location. Filter by country, remote filter, job type, and more.

**Detail enrichment** — Fetch full job descriptions, salary data, employer profiles, contact information for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 500). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases






**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from indeed.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from indeed.com.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on indeed.com to inform pricing decisions, hiring plans, or candidate negotiations.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "software developer",
  "maxResults": 50,
  "includeDetails": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Job search keywords. Single string or JSON array for multi-query (e.g. ["software engineer", "data analyst"]). Required unless startUrls is provided. |
| `country` | enum | `"US"` | Which Indeed domain to search (62 markets). Major markets (US, UK, DE, FR, etc.) are well-tested. Smaller markets are config-supported but listing volume varies. |
| `location` | string | — | City, state, or region to search within. Single string or JSON array for multi-location (e.g. ["New York", "San Francisco"]). Leave empty for nationwide results. |
| `startUrls` | array | — | Direct Indeed search or job detail URLs. Use instead of or alongside query. Accepts search pages (indeed.com/jobs?q=...) and job pages (indeed.com/viewjob?jk=...). |
| `maxResults` | integer | `50` | Maximum total job listings to return across all search sources. |
| `maxPages` | integer | `5` | Maximum SERP pages to scrape per search source. Each page typically contains 15 results. |
| `postedDays` | integer | — | Only return jobs posted within this many days. Automatically snapped to nearest valid value: 1, 3, 7, or 14. |
| `remoteFilter` | enum | — | Filter jobs by remote work availability. |
| `jobType` | enum | — | Filter by employment type. |
| `radius` | integer | — | Search radius around the specified location. Only applies when location is set. Valid values: 5, 10, 15, 25, 35, 50, 100. |
| `sort` | enum | `"relevance"` | Sort results by relevance (default) or by posting date (newest first). |
| `includeDetails` | boolean | `true` | Fetch each job's detail page for full description, JSON-LD data, requirements, benefits, and hiring signals. Set to false for fast SERP-only scraping. |
| `compact` | boolean | `false` | Output only ~12 core fields (jobId, title, company, location, salary, description, URL, dates, remote status). Ideal for AI agents, MCP workflows, and LLM context windows where token budget matters. |
| `descriptionMaxLength` | integer | — | Truncate job descriptions to this many characters (adds '...' suffix). Set to 0 to omit descriptions entirely. Leave empty for full descriptions. Useful for reducing payload size in API integrations and AI pipelines. |
| `includeCompanyProfile` | boolean | `false` | Fetch each unique company's /cmp/ page for industry, employee count, headquarters, revenue, and more. Cached per company within each run. |
| `incrementalMode` | boolean | `false` | Compare current results against stored state from a previous run. Each job is classified as NEW, UPDATED, UNCHANGED, EXPIRED, or REAPPEARED. Requires stateKey to be set. |
| `stateKey` | string | — | Stable identifier for the search universe being tracked. Use a descriptive key like "us-software-nyc" or "de-data-berlin". Different queries/locations should use different keys to avoid state cross-contamination. Required when incrementalMode is true. |
| `emitUnchanged` | boolean | `false` | When incremental mode is active, also output jobs that haven't changed since the last run. Default: only NEW, UPDATED, and REAPPEARED jobs are emitted. |
| `emitExpired` | boolean | `false` | When incremental mode is active, also output jobs from the previous state that were not found in the current run (marked as EXPIRED). |

---

## FAQ

<!-- WRITE: 4-6 Q&A pairs relevant to this product -->

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

---

## Known limitations

<!-- WRITE: 4-6 honest limitations -->

- <!-- WRITE: limitation 1 -->
- <!-- WRITE: limitation 2 -->


## Output fields

Every listing returns the same 74-field schema. Missing values are `null` — never omitted.

- `jobId`
- `jobKey`
- `title`
- `company`
- `companyUrl`
- `location`
- `description`
- `descriptionHtml`
- `descriptionLength`
- `salaryText`
- `salaryMin`
- `salaryMax`
- `salaryCurrency`
- `salaryType`
- `employmentType`
- `postedDate`
- `validThrough`
- `canonicalUrl`
- `portalUrl`
- `applyUrl`
- `requirements`
- `benefits`
- `sourceUrl`
- `sourceCountry`
- `sourceDomain`
- `searchQuery`
- `searchUrl`
- `isSponsored`
- `locationCity`
- `locationRegion`
- `locationCountry`
- `isRemote`
- `locationFormatted`
- `companyRating`
- `companyReviewsCount`
- `companyLogoUrl`
- `scrapedAt`
- `detailFetched`
- `contentQuality`
- `hiringAge`
- `isUrgentlyHiring`
- `numOfCandidates`
- `isRecurringHire`
- `jobCountry`
- `jobLanguage`
- `jobOccupations`
- `extractedEmails`
- `latitude`
- `longitude`
- `isRepost`
- `isLatestPost`
- `attributes`
- `jobTypes`
- `shiftAndSchedule`
- `workingSystem`
- `socialInsurance`
- `companyIndustry`
- `companyEmployeeRange`
- `companyEmployeeRangeRaw`
- `companySectorNames`
- `companyRevenue`
- `companyFoundedYear`
- `companyHeadquarters`
- `companyWebsite`
- `companyOpenJobsCount`
- `companyDescription`
- `companyCeo`
- `changeType`
- `trackedHash`
- `firstSeenAt`
- `lastSeenAt`
- `previousSeenAt`
- `expiredAt`
- `stateKey`


## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "ad864c37f1de92dd51c35b37c068a567af70e39d9d31f21aa5fae149011d8ca9",
  "jobKey": "2e960a289c9f26d8",
  "title": "PHP Developer",
  "company": "Upstate Breaker Wholesale Supply",
  "companyUrl": "https://www.indeed.com/cmp/Upstate-Breaker-Wholesale-Supply",
  "location": "Caledonia, NY, US",
  "description": "Job Summary: We are seeking a skilled full-time, in-house Backend Web Developer to join our team and support an established eCommerce website. This role involves developing new fea…",
  "descriptionHtml": "<p><b>Job Summary:</b></p>\n<p>We are seeking a skilled full-time, in-house <b>Backend Web Developer</b> to join our team and support an established eCommerce website. This role inv…",
  "descriptionLength": 1713,
  "salaryText": "From $40 an hour",
  "salaryMin": 40,
  "salaryMax": 40
}
```

*Truncated — full records contain 74 fields. See Output fields for the complete schema.*


**[Try Indeed Job Scraper now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi)**


## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.004 |

See the [actor on Apify](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) for current pricing.

---

## Related products by Black Falcon Data






- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal
- [Bilbasen Scraper](https://apify.com/blackfalcondata/bilbasen-scraper?fpr=1h3gvi) — Denmark's largest car marketplace

---


## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) — $5 credit included
2. Open the actor and paste your input
3. Click Start — results download as JSON, CSV, or Excel

Need more volume? [See pricing](https://apify.com/pricing?fpr=1h3gvi).

---

---

*Last updated: 2026 03*
