[Indeed Job Scraper](https://apify.com/pramodkonde17/indeed-job-scraper?fpr=data)

# Indeed Job Scraper — Apify Actor

Scrape job listings from [Indeed.com](https://indeed.com) based on job roles, location, and other filters. Returns structured job data ready for analysis or export.

## Features

- Search multiple job roles in a single run
- Filter by location (city, state, remote)
- Filter by date posted, job type (full-time, part-time, contract, etc.)
- Filter by remote-only positions
- Optional minimum salary filter
- Scrapes full job descriptions from individual job pages
- Returns benefits, requirements, company rating, and hiring insights
- Pagination support to collect up to 500 jobs per role
- Proxy support (Apify Residential recommended)

## Input

| Field | Type | Description | Default |
| --- | --- | --- | --- |
| `jobRoles` | Array | List of job titles to search (required) | `["Software Engineer"]` |
| `location` | String | Location (city, state, or "Remote") | `"United States"` |
| `maxJobsPerRole` | Integer | Max results per role (1–500) | `50` |
| `datePostedFilter` | String | Recency filter: 1, 3, 7, 14 days | Any time |
| `jobType` | String | fulltime / parttime / contract / temporary / internship | All |
| `remoteOnly` | Boolean | Only return remote jobs | `false` |
| `salaryMin` | Integer | Minimum annual salary | — |
| `includeDescription` | Boolean | Fetch full description per job | `true` |
| `proxyConfiguration` | Object | Apify proxy settings | Residential |

### Example Input

```
{
    "jobRoles": ["Data Scientist", "Machine Learning Engineer", "AI Engineer"],
    "location": "San Francisco, CA",
    "maxJobsPerRole": 100,
    "datePostedFilter": "7",
    "jobType": "fulltime",
    "remoteOnly": false,
    "includeDescription": true,
    "proxyConfiguration": {
        "useApifyProxy": true,
        "apifyProxyGroups": ["RESIDENTIAL"]
    }
}
```

## Output

Each item in the dataset contains:

| Field | Description |
| --- | --- |
| `jobId` | Unique Indeed job ID |
| `jobTitle` | Job title |
| `company` | Company name |
| `location` | Job location |
| `salary` | Salary range (if listed) |
| `jobType` | Full-time, part-time, etc. |
| `datePosted` | When the job was posted |
| `summary` | Short summary from listing card |
| `description` | Full job description text |
| `descriptionHtml` | Full description as HTML |
| `benefits` | Listed benefits |
| `requirements` | Key requirements |
| `companyRating` | Indeed company rating |
| `companyReviewCount` | Number of company reviews |
| `hiringInsights` | Hiring pace or insights |
| `url` | Direct link to the job posting |
| `searchRole` | Which job role was searched |
| `scrapedAt` | Timestamp of when it was scraped |

### Example Output

```
{
    "jobId": "abc123def456",
    "jobTitle": "Senior Data Scientist",
    "company": "Acme Corp",
    "location": "San Francisco, CA",
    "salary": "$150,000 - $180,000 a year",
    "jobType": "Full-time",
    "datePosted": "2 days ago",
    "summary": "We are looking for a passionate Data Scientist...",
    "description": "About the role: We are looking for a passionate...",
    "benefits": ["Health insurance", "401(k)", "Remote work"],
    "companyRating": 4.2,
    "companyReviewCount": "312 reviews",
    "url": "https://www.indeed.com/viewjob?jk=abc123def456",
    "searchRole": "Data Scientist",
    "scrapedAt": "2024-01-15T10:30:00.000Z"
}
```

## Notes

- **Proxy usage**: Apify Residential proxies are strongly recommended. Indeed actively blocks datacenter IPs.
- **Rate of requests**: The actor uses `maxConcurrency: 5` to avoid triggering anti-bot measures.
- **Indeed's structure**: Indeed frequently updates its HTML structure. If results are empty, the selectors may need updating.
- **Legal**: Always check Indeed's Terms of Service before using this actor commercially. This actor is intended for research and personal use.

## Deployment

1. Clone or push this directory to Apify Console
2. Go to **Actors → Create new Actor**
3. Connect your GitHub repo or upload the files
4. Set your input in the **Input** tab
5. Run the actor

Or use the Apify CLI:

```
apify login
apify push
apify run
```