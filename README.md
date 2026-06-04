# Full Universal Deploy

## Goal

**Deep & zero-config integration** between (Vite) apps and deployment providers:
- Deep: support advanced features like SPA fallback, AI integrations, ...
- Zero-config: the deployment integration works out-of-the-box with no/minimal config.

This proposal is about extending [Universal Deploy](https://github.com/universal-deploy/universal-deploy) to support more common deployment features.

> [!NOTE]
> **Brainstorming: quick-wins & vision.**
>
> This isn't a fixed plan — it's brainstorming to develop quick-win opportunities for Universal Deploy as well as to develop the Universal Deploy vision.


## Static deployments

Support for:
- URL rewrites:
  - Use case: SPA fallback (e.g. serve `dist/client/product/index.html` for route `/proudct/:id` i.e. URLs `/product/42`, `/product/1337`, ...)
  - Use case: 404 page (serve `dist/client/404/index.html` for route `/*` as a fallback)
- URL redirects


## CLI

CLI integration:
- `$ vite deploy logs` => server logs
- `$ vite deploy status` => deployment status, and downtime status for past 30 days
- `$ vite deploy ls` => e.g. number of workers, system metrics (CPU usage, mem usage)
- `$ vite deploy db` => connect to DB and run queries, e.g. `SELECT { title, release_date } FROM movies;`
  - `$ vite deploy db migrate` => connect to DB and run migrations

> [!NOTE]
> **Why? AI.**
>
> AI cannot (practically) work with UIs — the CLI enables AI to access deployment information (e.g. deployment logs for debugging).


## Tasks

How to support tasks (cron jobs and queues) in a way that works for any deployment provider?

Is there a standard syntax for defining tasks & queues? The UNIX cron syntax?


## Environment Variables

How can we best manage/support secrets?

> [!NOTE]
> **What are secrets?**
>
> Secrets are environment variables that hold senstive information such as `DB_PASSWORD`.
>
> The goal here is that is that secrets are supported by the deployment provider without the user having to configure anything — the Vite-based framework and deployment provider talk to each other directly through Universal Deploy.
>
> See also:
> - [SecretSpec](https://secretspec.dev)

We can first focus on simple use cases for small teams, while maybe trying to be flexible for enterprises that have a rigid process for managing secrets.


## AI integration

How will deployment integration with AI workflows look like?

Example: error detected in deployment => AI is automatically prompted => AI can access deployment logs and source code => AI proposes fix => human review => fix is merged & deploy — the only human intervention here is reviewing the bug fix.
