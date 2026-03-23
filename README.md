# *Full* Universal Deploy

See: https://github.com/universal-deploy/universal-deploy

Same idea but, full-fledged common deployment features.

## Static deployment

Zero-config support for:

- SPA fallback (URL rewrite)
- 404 pages (URL rewrite)
- Redirects
- More?

## Server deployment

Zero-config support for:

- Environment variable and secrets management (built-in, no need for [SecretSpec](https://secretspec.dev))
- CLI integration
  - `$ vite deploy status` => deployment status + downtime status past 30 days
  - `$ vite deploy logs` => server logs
  - `$ vite deploy ls` => number of workers, system metrics (e.g. CPU usage, mem usage), ...
  - `$ vite deploy db` => connect to DB and run queries e.g. `SELECT { title, release_date } FROM movies;`
- Cron jobs
- More?

## AI

LLMs much prefer text-based interfaces rather than UIs. Deployment features via CLI is significantly more efficient for agentic automation and insights (e.g. enables AI to access server logs).
