# Agent Hub Testing Dashboard — V3

Static dashboard: **Level 1** `index.html` + **24 Level 2 HTML** reports. Both levels load the **same per-environment JavaScript data files**.

## Copilot update contract (important)

**Only edit the matching `data/<report_key>.js` file. Never edit `index.html`, the Level 2 HTML, or `assets/*.js` when refreshing Jira/Zephyr data.**

Example: to update UK Ideation v2 Healthcheck, update `data/hc_uk_ideation_v2.js`. Both `index.html` and `hc_uk_ideation_v2.html` will show new values after reload.

Naming: `hc` = Healthcheck, `rt` = Regression Test; `hk|uk`, `ideation|poc|prod`, `v1|v2`. There are 24 matching `data/*.js` files.

Every data file defines:

```js
window.dashboardData = window.dashboardData || {};
window.dashboardData["hc_uk_ideation_v2"] = {
  purpose: "hc", region: "UK", stage: "Ideation", version: "v2.0",
  jiraDashboardUrl: null, updatedAt: null, sourceComplete: true,
  execution: {
    total: 220, passed: 175, failed: 8, blocked: 7,
    cancelled: 0, notApplicable: 0
  },
  defects: [
    { priority: "High", key: "DEMO-001", assignee: "Tester A",
      summary: "Example issue", url: null }
  ]
};
```

**Execution completion** = `(passed + failed + blocked + cancelled + notApplicable) / total * 100`. **Outstanding defects** = `defects.length`. These calculations are done by the browser on both levels, not copied into files. The executed status mapping is provisional; agree exact Zephyr statuses before using live data.

### Agent workflow

1. Determine the exact report key, its approved ZQL for test executions and JQL for outstanding defects.
2. Run existing company Jira/Zephyr tools and fetch **all pages**; handle rate limits. Do not assume the Jira Assistant skill supports ZQL without verifying its endpoint and access.
3. Verify query scope, distinct executions, totals, status counts, and defects; never fabricate missing records.
4. Replace **only the matching data file's object**. Set `updatedAt` to the actual collection timestamp. Use actual Jira URLs and dashboard URL when known; otherwise `null`.
5. If either query is incomplete, set `sourceComplete: false`; **do not publish partial results as complete**. Ideally keep the previous complete snapshot until a full refresh succeeds.
6. Validate the JS syntax, counts, and matching key. Refresh `index.html` and its detail HTML to see the same data. Commit only the data file.

### Local usage

Open `index.html` directly in Chrome/Edge using `file://`. Data loads with ordinary `<script src="data/...js">` tags, so no local server, Python, Node, build process, or fetch/CORS workaround is required.

All included values and `DEMO-` issues are **fictional samples**. They are not live Jira/Zephyr results. No real query configurations are bundled yet. Keep sensitive JQL/ZQL, credentials and internal URLs out of a public repository.
