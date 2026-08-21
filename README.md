# questgro-uptime

External synthetic check for **QuestGro** (https://cg.oculogic.io), which runs on a
Mac Mini behind a Cloudflare tunnel. A watchdog on that Mac cannot tell you the Mac
is gone — this one runs on GitHub's infrastructure instead.

* `.github/workflows/probe.yml` — every ~5 min: `GET https://cg.oculogic.io/health`,
  3 attempts, requires `200` **and** `{"status":"ok"}`. Pings a Healthchecks.io check
  on success, `/fail` on failure, and fails the job so it is visible here too.
* Alert delivery is Healthchecks.io → email to carl@oculogicgroup.com.
* **No credentials in this repo.** The only secret is `HC_PING_URL` (repo secret).

Full monitoring stack lives on the Mac at `/Users/carlmacmini/questgro-monitor/`.
Moving to Render? Change `HEALTH_URL` in `probe.yml` and `health_url` in the Mac's
`config.json`.
