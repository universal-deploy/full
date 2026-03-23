# *Full* Universal Deploy

Goal: extend [Universal Deploy](https://github.com/universal-deploy/universal-deploy) to common deployment features.

## Server deployment

Zero-config support for:

- Environment variable: secrets management (built-in, no need for [SecretSpec](https://secretspec.dev))
- CLI integration
  - `$ vite deploy logs` => server logs
  - `$ vite deploy status` => deployment status + downtime status past 30 days
  - `$ vite deploy ls` => number of workers, system metrics (e.g. CPU usage, mem usage), ...
  - `$ vite deploy db` => connect to DB and run queries e.g. `SELECT { title, release_date } FROM movies;`
- Cron jobs
- ...

## Static deployment

Zero-config support for:

- SPA fallback (URL rewrite)
- 404 pages (URL rewrite)
- Redirects
- ...

## AI

LLMs much prefer text-based interfaces rather than UIs. Deployment features via CLI is significantly more efficient for agentic automation and insights (e.g. AI can access server logs).
