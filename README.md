# Agent Hub Testing Dashboard

Static HTML testing dashboard with **Level 1 overview** and **24 independent Level 2 environment reports**.

- Open `index.html` for the overview.
- Healthcheck: `hc_<region>_<stage>_<version>.html`
- Regression Test: `rt_<region>_<stage>_<version>.html`
- Region: `hk`, `uk`; stage: `ideation`, `poc`, `prod`; version: `v2`, `v1`.
- Each detail page embeds its **own** `reportData` object. Copilot should update that object from verified Jira/Zephyr data, not change layout or other environments.
- `assets/styles.css` contains shared styling; `assets/detail.js` renders the detail pages.
- `index.html` has sample overview data. Refresh it separately after updating detail reports.
- All sample metrics and DEMO issue IDs are **fictional**. `jiraDashboardUrl: null` and `url: null` intentionally disable external navigation until configured.
- Do not present partial ZQL pages as complete totals. Confirm pagination, status mapping, and timestamps before publishing real data.
- Completion formula in prototype: `executed / total * 100`. Define executed statuses explicitly before real integration.

No build, Python, Node, or server required. Open pages locally or host with GitHub Pages.
