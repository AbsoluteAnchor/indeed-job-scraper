[Indeed Job Scraper](https://apify.com/bradmccloskey/indeed-job-scraper?fpr=data)

Scrape job listings from Indeed at scale. Search by keyword, location, and filter for remote positions. Get structured job data including salary ranges, company names, descriptions, and posting dates for recruitment, market research, and job market analysis.

## Why use this scraper?

- **Recruitment automation**: Build candidate sourcing pipelines by tracking job market demand
- **Salary benchmarking**: Collect salary data across roles, locations, and industries
- **Job market analysis**: Track hiring trends, in-demand skills, and emerging roles
- **Competitive hiring intelligence**: Monitor what your competitors are hiring for
- **Career research**: Analyze job requirements and qualifications at scale

## Features

- **Keyword search**: Search any job title, skill, company, or keyword
- **Location filtering**: Target specific cities, states, or zip codes
- **Remote filter**: Return only remote/work-from-home positions
- **Salary extraction**: Capture salary ranges when listed by employers
- **Anti-detection**: Built-in browser stealth to avoid blocks
- **Proxy support**: Works with Apify proxy or your own residential proxies

## What data you get

| Field | Type | Description |
| --- | --- | --- |
| `job_id` | string | Unique job identifier |
| `source` | string | `indeed` |
| `title` | string | Job title |
| `company` | string | Company name |
| `location` | string | Job location (city, state, zip) |
| `salary` | string | Salary range (e.g., "$120,000 - $160,000 a year") |
| `job_type` | string | Full-time, Part-time, Contract, etc. |
| `description` | string | Job description snippet |
| `requirements` | array | Listed requirements and qualifications |
| `posted_date` | string | When the job was posted (e.g., "3 days ago") |
| `url` | string | Direct job listing URL |
| `is_remote` | boolean | Whether the position is remote |

## Input example

```
{
    "searchQueries": ["data engineer", "python developer", "devops engineer"],
    "location": "San Francisco, CA",
    "remoteOnly": false,
    "maxResultsPerQuery": 50
}
```

## Output example

```
{
    "job_id": "indeed_a1b2c3d4e5",
    "source": "indeed",
    "title": "Senior Data Engineer",
    "company": "Stripe",
    "location": "San Francisco, CA 94103",
    "salary": "$180,000 - $250,000 a year",
    "job_type": "Full-time",
    "description": "We're looking for an experienced Data Engineer to design, build, and maintain data pipelines that power Stripe's analytics and machine learning platforms...",
    "requirements": ["Python", "SQL", "Apache Spark", "AWS/GCP", "Data modeling"],
    "posted_date": "2 days ago",
    "url": "https://www.indeed.com/viewjob?jk=a1b2c3d4e5",
    "is_remote": false
}
```

## Use cases

### Salary benchmarking reports

Search for a role across multiple cities. Compare salary ranges by location to build compensation benchmarks for HR teams.

### Job market trend analysis

Run weekly scrapes for trending tech skills (AI/ML, Rust, Kubernetes). Track how demand shifts over time for recruiting agencies and workforce planning.

### Competitive hiring intelligence

Monitor job postings from specific companies. Identify when competitors are ramping up hiring in a new area or technology.

### Lead generation for recruiters

Build lists of companies actively hiring. Cross-reference with LinkedIn and CRM data for recruiter outreach.

## Tips for best results

- **Combine keywords**: "python developer" finds more results than just "python"
- **Use `remoteOnly: true`** to filter for remote-only positions
- **Multi-city runs**: Search across multiple locations in one run for broader coverage
- **Schedule daily runs** to catch new listings before they expire
- **Use Apify proxy** for best reliability on large runs

## Pricing

**$3.00 per 1,000 results** (pay-per-result). Platform fees included.

## Integrations

Export results to Google Sheets, Airtable, Slack, Zapier, Make, or webhooks using Apify's built-in integrations. Download as JSON, CSV, or Excel.