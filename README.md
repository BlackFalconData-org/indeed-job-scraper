# Indeed Job Scraper

Extract structured job listings from Indeed across 62 markets with built-in change tracking for recurring monitoring.

**[Indeed Job Scraper on Apify →](https://apify.com/blackfalcondata/indeed-job-scraper)**

---

## Key features



**Search with filters** — Search by keyword and location. Filter by country, remote filter, job type, and more.

**Detail enrichment** — Fetch full job descriptions, salary data, employer profiles, contact information for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

---

## Use cases



**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from indeed.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from indeed.com.

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

---

## Related products by Black Falcon Data



- [StepStone Scraper](https://github.com/BlackFalconData-org/stepstone-scraper) — Job listings from 18 European portals
- [Glassdoor Job Scraper](https://github.com/BlackFalconData-org/glassdoor-job-scraper) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://github.com/BlackFalconData-org/arbeitsagentur-scraper) — Germany's official job portal (1M+ listings)

---

*Last updated: 2026 03*
