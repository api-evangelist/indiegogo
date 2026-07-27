---
name: Discover active Indiegogo crowdfunding projects
description: List active crowdfunding campaigns and drill into one by its urlName.
api: openapi/indiegogo-public-openapi.yml
operations: [getActiveCrowdfundingProjects, getCrowdfundingProject]
---

# Discover active Indiegogo crowdfunding projects

Use the Indiegogo Public API (`https://www.indiegogo.com/api/public`) to browse
live crowdfunding campaigns. The API is read-only and requires **no
authentication**.

## Steps

1. **List active projects** — `GET /api/public/projects/getActiveCrowdfundingProjects`
   (`getActiveCrowdfundingProjects`). Returns a JSON array of projects ordered by
   `campaignStartDate`. Each item includes `projectName`, `projectUrlName`,
   `shortDescription`, `campaignGoal`, `fundsGathered`, `currencyShortName`,
   `backerCount`, and `campaignEndDate`.
2. **Pick a project** — take the `projectUrlName` of the campaign you want
   (e.g. `olive--lemon`).
3. **Fetch project detail** — `GET /api/public/projects/getCrowdfundingProject?urlName={projectUrlName}`
   (`getCrowdfundingProject`). Returns the full project object.

## Rules

- No API key or token is needed; do not send auth headers.
- Results are cached server-side for a short duration — do not poll tightly.
- On a missing/invalid `urlName` the API returns HTTP 400 with
  `{ "success": false, "message": "..." }` (not RFC 9457). Check `success`
  before reading data. See `errors/indiegogo-problem-types.yml`.
- Identifiers are human-readable `urlName` slugs, not numeric ids
  (`conventions/indiegogo-conventions.yml`).
