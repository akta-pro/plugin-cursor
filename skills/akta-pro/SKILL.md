---
name: akta-pro
description: Use the akta.pro MCP tools to find, enrich and monitor companies. Use for questions about a company, funding, M&A, investors, headcount, hiring, competitors, prospects, market maps, company lists, company news or industry news.
---

# akta.pro

## When to use

- Looking up or profiling a company
- Building a list of companies
- Tracking company or industry news and signals

## Instructions

1. Resolve companies first. Call company_search, then pass only the returned uuid as `company` to company tools. Never pass a name or website, and never guess a uuid.
   - If several candidates match, pick the one whose website matches the company the user means. One website can map to several entities.
   - For a subsidiary or product line, call company_search with include_child_companies set to true.
   - If no candidate fits, tell the user the company isn't covered.
2. Fetch only what the question needs. company_data requires an explicit `sections` list, so request just the relevant sections. For a broad overview, use company_data_concise instead.
3. Company lists. Call list_filters and get_filter_values before generate_company_list, and use the returned values verbatim. On Pay as you go, a list call returns at most 20 companies. Subscription and Enterprise allow up to 500.
   - Send at least one selective filter. Start with the core filters, then drop results that don't fit the request rather than stacking every filter up front.
   - Read `warnings` in the result. A dropped value means the list is broader than the user asked for.
   - The list returns identifiers only. For depth, call company_data on the companies that matter.
4. News. Call news_types and industry_search (for industry topics) before news_signals.
   - Use primary_company for news about a company and `company` for any mention. Don't pass both.
   - Pass news_types codes as type_codes and industry_search codes as `industry`. Use `query` only when the topic is neither a company nor an industry.
   - Narrow with start_date, end_date, sentiment, countries and news_score, and set group_articles to true to merge duplicate coverage.
   - Results carry summaries only. Pass the ids you need to news_detail (up to 10 per call) for the full text.
5. Pagination. news_signals, generate_company_list, job_posts, social_posts and employee_reviews page with limit and offset. news_signals returns at most 100 per call. A generate_company_list total_count of 500 means "500 or more", so narrow the filters instead of paging further.
6. product_reviews takes two calls: first without products to get the catalog ids, then with the ids you need.
7. Handle errors by status code:
   - 403 (plan-gated): call account_status and tell the user the tool needs a higher plan.
   - 402 (insufficient credits): tell the user their credits are used up and to top up.
   - 429: it's a rate limit, so wait and retry with exponential backoff, starting at 1 second and capping at 60 seconds.

## Plans and costs

- News history is 6 months on Pay as you go, 1 year on Subscription and no limit on Enterprise, so don't ask for older news on lower plans.
- On Pay as you go, company_data silently drops the funding_detail and mna_and_investment sections, so don't promise funding or M&A data from it.
- Discovery tools (company_search, industry_search, list_filters, get_filter_values, news_types, account_status) are free. generate_company_list costs 1.5 credits plus 0.2 per company, so keep lists as small as the question allows.
