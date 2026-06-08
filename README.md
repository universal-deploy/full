# Full Universal Deploy

*Zero-config deep integration between Vite apps and deployment providers.*

**Contents**

- [Goal](#goal)
- [Static hosting](#static-hosting)
- [Async jobs](#async-jobs)
- [CLI](#cli)
- [AI](#ai)

## Goal

Extend [Universal Deploy](https://github.com/universal-deploy/universal-deploy): **deeper** integration between Vite aps and deployment — support features like SPA fallback, async jobs, ...

Everything stays **zero-config**: Vite apps can be deployed out-of-the-box with minimal config.

> [!NOTE]
> **Vite**
>
> We're currently focusing on the Vite ecosystem — supporting other bundlers is a long-term goal but not a short-term priority.


## Static hosting

Support for:
- URL rewrites, for following use cases:
  - SPA fallback (e.g. serve `dist/client/product/index.html` for route `/product/:id`, i.e. URLs `/product/42`, `/product/1337`, ...)
  - 404 page (serve `dist/client/404/index.html` as a catch-all fallback)
- URL redirects

> [!NOTE]
> **Marketing**
>
> It's a quick-win for a deployment provider to position itself as the **best solution for hosting static websites**. Vike (and others) will, accordingly, recommend its users to use such deployment provider. It's an effective way to earn trust and popularity amongst users.

> [!NOTE]
> **Implementation**
>
> Universal Deploy has been developed with such features in mind — implemention is relatively easy.


## Async jobs

How can the user define async tasks, queues, and cron jobs in a way that works across many deployment providers?

> [!NOTE]
> **Implementation**
>
> The implementation itself is relatively easy — this is mostly about researching and finding (new?) standard syntax. For example, let's explore whether we can use the UNIX cron syntax as the standard syntax for cron jobs.


## CLI

CLI integration:
- `$ vite deploy logs` => server logs
- `$ vite deploy status` => deployment status, downtime status for past 30 days, ...
- `$ vite deploy ls` => number of workers, system metrics (CPU usage, mem usage), ...
- `$ vite deploy db` => connect to DB and run queries, e.g. `SELECT { title, release_date } FROM movies;`
  - `$ vite deploy db migrate` => and run migrations
- `$ vite secrets` => manage production environment variables (e.g. `DB_PASSWORD`)
  ```shell
  # Set a secret
  $ vite deploy secrets set DB_PASSWORD lOK9uiUuCP75lMzQ
  # Get all secrets
  $ vite deploy secrets list
  ```

> [!NOTE]
> **Motivation: AI**
>
> AI cannot (practically) work with UIs — the CLI enables AI to access deployment data (such as deployment logs for debugging).

> [!NOTE]
> **Implementation**
>
> - We quickly implement `$ vike deploy` first (instead of `$ vite deploy`)
> - We talk to the Vite team about adding `$ vite deploy` to Vite's CLI:
>   - The Vite team has repeatedly shown interest in having Vite plugins be able to extend Vite's CLI (e.g. for further enabling frameworks to be "just Vite plugins")
>   - We're currently working with the Vite team on [Vite deployment plugins](https://github.com/vitejs/vite/discussions/20907). Adding a `deploy` CLI command is a natural next step.



## AI

What is the future of deployment integration with AI workflows?

Example:
- Error detected in deployment => AI is automatically prompted => AI can access deployment logs and source code => AI proposes fix => human review => fix is merged & deployed
- The only human intervention in the flow above is reviewing the bug fix
