# akta.pro for Cursor

akta.pro provides private company data, news and signals to AI agents. This plugin connects Cursor to the akta.pro MCP server, so the agent can find, enrich and monitor companies without leaving the editor.

## What you can do

- **Find companies with filters:** build company lists, market maps, target accounts and peer sets using industry, location, ownership, funding, investors, revenue, valuation and more.
- **Enrich companies and build profiles:** data on 20M+ companies across 74 structured fields, covering firmographics, management, products, funding, M&A, investments, revenue, valuation, technology and more.
- **Monitor company news, signals and events:** track 20M+ companies across 77 event types, including funding, M&A, partnerships, product launches, executive changes, hiring, layoffs and litigation.
- **Monitor industry news, signals and events:** surface activity and trends across 30,000+ sub-sectors.
- **Analyze alternative signals:** headcount, web traffic, job posts, social posts, employee reviews and product reviews, all resolved to the same company ID.

Outputs are compact, filterable and traceable to source, which keeps tool calls reliable and context usage small.

## Setup

1. Install the plugin from the Cursor Marketplace.
2. Open **Customize → MCPs**, find **akta-pro** and click **Authenticate**.
3. Sign in to akta.pro in the browser and click **Allow**. New users can sign up for free at https://playground.akta.pro/signup, and every new account includes free credits.
4. The akta-pro server turns green with 17 tools. No API key is needed.

## Tools

| Group | Tools | Plan |
|---|---|---|
| Discovery | company_search, industry_search, list_filters, get_filter_values, news_types, account_status | Free on any plan |
| Company data | company_data, company_data_concise | Any plan; funding_detail and mna_and_investment need Subscription or Enterprise |
| Company lists | generate_company_list | Any plan; Pay as you go returns up to 20 companies per call |
| News | news_signals, news_detail | Any plan |
| Alternative signals | headcount_trends, website_traffic, job_posts, social_posts, employee_reviews, product_reviews | Subscription or Enterprise |

## Plans

| | Pay as you go | Subscription | Enterprise |
|---|---|---|---|
| How to start | Free signup credits, top-ups from $1 | Monthly plan | Contact sales@akta.pro |
| Company search, profiles, news | ✓ | ✓ | ✓ |
| News history | 6 months | 1 year | No limit |
| Company lists | Up to 20 companies per call | Up to 500 | Up to 500 |
| Funding and M&A detail | Not included (skipped without an error) | Summary (first 3 rounds/deals) | Full history |
| Alternative signals | Not included | ✓ | ✓ |
| Rate limit | 25 requests/min | 100 to 300 requests/min | Custom |

## Data freshness

- Company records refresh every month.
- High-frequency fields such as funding, M&A, investments, leadership changes and signals update in near real time.
- News runs on a real-time pipeline. Headcount, web traffic and job post data refresh monthly. Social posts, employee reviews and product reviews update in near real time.

## Example prompts

**Works on any plan**
- Find 20 bootstrapped or founder-owned HVAC businesses in California valued under $10M.
- Build a profile of Ramp, including revenue, valuation, products and leadership.
- Find healthcare CXO appointments in the US from the last 3 months.
- Show the latest product launches and partnerships for Notion.

**With a Subscription**
- Show Ramp's funding history, investors and acquisitions.
- Find headcount growth by department and website traffic for Coda.
- Show job posts and LinkedIn posts for Canva.
- Compare employee reviews and product reviews for Notion and Coda.

## Troubleshooting

- **"Needs authentication":** open Customize → MCPs and click Authenticate again.
- **HTTP 403, plan-gated:** the tool or data isn't included in your plan, so upgrade. Ask the agent to run account_status to check your plan.
- **HTTP 402:** you have insufficient credits, so top up.
- **HTTP 429:** you've hit a rate limit. It can be the per-minute limit or a daily or monthly quota for that endpoint, so waiting a moment won't always work. Limits are per account and shared across every way you connect, including the API, the CLI and MCP clients.
- **Company not found:** company tools accept only the ID returned by company_search, so search by name or website first.

## Support

- Email: support@akta.pro
