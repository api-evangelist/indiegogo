---
name: Look up an Indiegogo creator
description: Resolve a creator profile by urlName, e.g. from a project's creatorUrlName.
api: openapi/indiegogo-public-openapi.yml
operations: [getCreator]
---

# Look up an Indiegogo creator

Resolve a campaign creator's public profile on the Indiegogo Public API
(`https://www.indiegogo.com/api/public`). Read-only, **no authentication**.

## Steps

1. **Obtain a creator urlName** — either from a project object's
   `creatorUrlName` (see the discover-projects skill) or a known slug
   (e.g. `defne-mustecaplioglu`).
2. **Fetch the creator** — `GET /api/public/creators/getCreator?urlName={urlName}`
   (`getCreator`). Returns `name`, `urlName`, `description`, `creatorPageUrl`,
   and `thumbImageUrl`.

## Rules

- No API key or token required.
- `description` and `thumbImageUrl` may be `null` / a placeholder image.
- Missing/invalid `urlName` returns HTTP 400 with
  `{ "success": false, "message": "URL name was not provided." }`. Check
  `success` first. See `errors/indiegogo-problem-types.yml`.
- A `Project.creatorUrlName` resolves against `Creator.urlName`
  (`data-model/indiegogo-data-model.yml`).
