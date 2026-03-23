# *Full* Universal Deploy

Goal: extend [Universal Deploy](https://github.com/universal-deploy/universal-deploy) to common deployment features.

## Server deployment

Zero-config support for:

- Environment variable via secrets management (built-in, no need for [SecretSpec](https://secretspec.dev))
- CLI integration
  - `$ vite deploy logs` => server logs
  - `$ vite deploy status` => deployment status, and downtime status for past 30 days
  - `$ vite deploy ls` => e.g. number of workers, system metrics (CPU usage, mem usage)
  - `$ vite deploy db` => connect to DB and run queries, e.g. `SELECT { title, release_date } FROM movies;`
- Tasks (queues, cron jobs)
- ...

## Static deployment

Zero-config support for:

- SPA fallbacks (URL rewrite)
- 404 page (URL rewrite)
- Redirects
- ...

## AI

LLMs are much more efficient with text-based interfaces than UIs. Implementing deployment features via the CLI enables agentic automation and insights (e.g. AI can access server logs).
