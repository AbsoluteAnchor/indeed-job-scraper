[Indeed Job Scraper](https://apify.com/khadinakbar/indeed-job-scraper?fpr=data)

# 💼 Extract Indeed Job Listings — Salaries, Remote & Full Details

**Scrape Indeed.com job postings at scale.** Get structured job data including parsed salary ranges (min/max as numbers), remote/hybrid/on-site status, job type, company ratings, benefits, and full descriptions — ready for spreadsheets, CRMs, AI pipelines, and HR tools.

---

## What Does This Actor Do?

This actor scrapes job listings from Indeed.com and returns clean, structured JSON data. You provide a job title keyword and location (or a direct Indeed search URL), and it returns every matching job with all available details — no login required, no cookies needed.

Works across 9 country domains: United States, United Kingdom, Canada, Australia, India, Germany, France, Singapore, and New Zealand.

## Why Use This Indeed Job Scraper?

**60% cheaper than the top competitor** — $2 per 1,000 jobs vs $5/1k elsewhere. Same data, lower cost.

**Structured salary data** — most scrapers return "45,000 - 65,000 a year" as a text blob. This actor parses it into `salary_min: 45000`, `salary_max: 65000`, `salary_period: "year"` — ready to filter and sort without regex hacks.

**Remote/Hybrid flag** — instantly filter remote jobs with `is_remote: true` or `work_type: "Hybrid"`. No manual parsing needed.

**Dual extraction strategy** — extracts from Indeed's embedded JSON payload first (fast and complete), falls back to CSS selectors with 3 fallbacks per field if the page structure changes.

**Export to anything** — CSV, JSON, Excel, Google Sheets, or directly to your CRM via the Apify API.

## What Data Can This Actor Extract?

| Field | Type | Example |
| --- | --- | --- |
| `job_title` | string | "Senior Software Engineer" |
| `company_name` | string | "Acme Corp" |
| `company_rating` | number | null | 4.2 |
| `location` | string | "Austin, TX" |
| `is_remote` | boolean | false |
| `work_type` | string | null | "Hybrid" |
| `job_type` | string | null | "Full-time" |
| `salary_min` | number | null | 90000 |
| `salary_max` | number | null | 130000 |
| `salary_currency` | string | null | "USD" |
| `salary_period` | string | null | "year" |
| `salary_text` | string | null | "$90,000–$130,000 a year" |
| `description` | string | "We are looking for..." |
| `posted_at` | string | null | "3 days ago" |
| `benefits` | array | null | ["Health insurance", "401k"] |
| `job_url` | string | "[https://indeed.com/viewjob?jk=](https://indeed.com/viewjob?jk=)..." |
| `scraped_at` | string | "2026-04-09T10:30:00.000Z" |

---

## How to Scrape Indeed Jobs — Step-by-Step Tutorial

### Option A: Search by Keyword + Location (Most Common)

1. Open the actor and enter your **Job Search Query** (e.g. `"data analyst"`)
2. Enter a **Location** (e.g. `"Chicago, IL"` or `"Remote"`)
3. Set **Maximum Results** — start with 50, increase for bulk runs
4. Click **Run** — results appear in the **Output** tab

### Option B: Scrape from a Direct Indeed URL

1. Open Indeed.com and perform any search (filters, date posted, salary — anything)
2. Copy the URL from your browser address bar
3. Paste it into the **Direct Indeed URLs** field
4. Run the actor — it will paginate through all results automatically

### Option C: Run via API (for developers)

```
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('USERNAME/indeed-job-scraper').call({
    searchQuery: 'software engineer',
    location: 'San Francisco, CA',
    maxResults: 200,
    country: 'www',
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(`Scraped ${items.length} jobs`);
// items[0] → { job_title: "Senior SWE", company_name: "Google", salary_min: 180000, ... }
```

### Option D: Call via Claude or any AI Agent (MCP)

This actor is optimized for the Apify MCP server. When Claude or another AI agent needs job market data, it will discover and call this actor automatically.

Example prompts that work:

- *"Find me 100 data scientist jobs in New York with salaries above $100k"*
- *"What remote engineering jobs are available in Canada?"*
- *"Scrape 500 Indeed job listings for nurse practitioners"*

---

## Pricing

This actor uses **pay-per-event** pricing: **$0.002 per job listing** (= $2 per 1,000 jobs).

| Jobs Scraped | Cost |
| --- | --- |
| 50 jobs | $0.10 |
| 100 jobs | $0.20 |
| 500 jobs | $1.00 |
| 1,000 jobs | $2.00 |
| 5,000 jobs | $10.00 |

Plus a small run start fee of $0.0005 per run. You can set a **maximum spend limit** in your Apify account to cap costs automatically.

---

## Input Parameters

| Parameter | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `searchQuery` | string | No* | — | Job title, skill, or keyword to search |
| `location` | string | No | — | City, state, ZIP, or "Remote" |
| `startUrls` | array | No* | — | Direct Indeed.com search URLs |
| `maxResults` | integer | No | 50 | Max jobs to scrape (1–1000) |
| `country` | select | No | `www` | Country domain (www/uk/ca/au/in/de/fr/sg/nz) |
| `proxyConfiguration` | object | No | Residential | Proxy settings |

*Either `searchQuery` or `startUrls` is required.

---

## Output Format

Each job record in the dataset looks like this:

```
{
    "job_id": "a1b2c3d4e5f67890",
    "job_title": "Senior Software Engineer",
    "company_name": "Acme Corporation",
    "company_rating": 4.2,
    "location": "Austin, TX",
    "is_remote": false,
    "work_type": "Hybrid",
    "job_type": "Full-time",
    "salary_min": 90000,
    "salary_max": 130000,
    "salary_currency": "USD",
    "salary_period": "year",
    "salary_text": "$90,000 - $130,000 a year",
    "description": "We are looking for a Senior Software Engineer to join our platform team...",
    "posted_at": "3 days ago",
    "benefits": ["Health insurance", "401(k)", "Paid time off", "Remote work options"],
    "job_url": "https://www.indeed.com/viewjob?jk=a1b2c3d4e5f67890",
    "source_url": "https://www.indeed.com/jobs?q=software+engineer&l=Austin%2C+TX",
    "scraped_at": "2026-04-09T10:30:00.000Z"
}
```

---

## Common Use Cases

**Talent acquisition & recruitment** — build a pipeline of open roles in your target market, track which companies are hiring, and identify in-demand skills by reading job descriptions at scale.

**Salary benchmarking** — collect hundreds of salary data points for specific roles and locations. Use `salary_min`/`salary_max` fields to calculate market medians without any text parsing.

**Job board aggregation** — build a niche job board by scraping Indeed listings for specific industries and re-publishing them with added context.

**AI-powered job matching** — pipe job descriptions into an LLM to match candidates to roles, extract required skills, or generate summaries.

**Competitive research for HR teams** — monitor what your competitors are hiring for, how quickly roles are filled, and what compensation they advertise.

**Market research & workforce analytics** — track hiring velocity by city, industry, or company over time. Export to Excel or your BI tool of choice.

---

## FAQ

**Does this require an Indeed account or login?**
No. This actor scrapes publicly available job listings without any login or account.

**How many results can I get per search?**
Indeed typically shows up to ~1,000 results per search query. For more, use multiple queries or different locations. Set `maxResults` up to 1,000 per run.

**Will it get blocked?**
The actor uses stealth Playwright with residential proxies and human-like delays to minimize detection. Occasional retries are normal and handled automatically.

**Can I scrape multiple countries?**
Yes — change the `country` field to `uk`, `ca`, `au`, `in`, `de`, `fr`, `sg`, or `nz`.

**Why are some salary fields null?**
Indeed only shows salary when employers choose to disclose it. Many listings don't include salary data — this is a limitation of Indeed, not the scraper.

**How do I export to Excel or Google Sheets?**
After a run, go to the **Output** tab → click **Export** → choose CSV or Excel. Or use the Apify API to fetch results programmatically.

---

## Works Great With

- **[Contact Enricher](https://apify.com/store)** — add email/phone to companies found in job listings
- **[Google Sheets Integration](https://apify.com/apify/google-sheets-import-export)** — auto-export results to a live spreadsheet
- **[Apify Scheduler](https://docs.apify.com/platform/schedules)** — run daily to track new postings automatically

---

## Legal Disclaimer

This actor is intended for lawful data collection from publicly available sources. Indeed.com job listings are publicly accessible without authentication. Users are responsible for compliance with applicable laws, Indeed's Terms of Service, and relevant data protection regulations (GDPR, CCPA, etc.). Do not use this actor to collect personal data without a legal basis or to circumvent Indeed's rate limits maliciously. The actor author assumes no liability for misuse.