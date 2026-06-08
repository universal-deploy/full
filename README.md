# Full Universal Deploy

## Goal

*Zero-config, deep integration between (Vite) apps and deployment providers.*
- **Deep**: advanced features like SPA fallback, AI integrations, ...
- **Zero-config**: deployment works out-of-the-box with no/minimal config.

This proposal is about extending [Universal Deploy](https://github.com/universal-deploy/universal-deploy) to support more common deployment features.


## Static hosting

Support for:
- URL rewrites:
  - Use case: SPA fallback (e.g. serve `dist/client/product/index.html` for route `/proudct/:id` i.e. URLs `/product/42`, `/product/1337`, ...)
  - Use case: 404 page (serve `dist/client/404/index.html` for route `/*` as a fallback)
- URL redirects

> [!NOTE]
> *Marketing**
>
> It's a quick-win for a deployment provider to position itself as the best solution to host static websites. Vike (and others) will, accordingly, recommend its users to use deployment providers for static websites. It's an effective way to earn trust and popularity amongst users.

> [!NOTE]
> **Implementation**
>
> Universal Deploy has been developed with such features in mind — implementing this is relatively easy.


## Async jobs

How can the user define async tasks, queues, cron jobs in a way that works across many deployment providers?

> [!NOTE]
> **Implementation**
>
> The implementation itself is relatively easy — this is mostly about researching and finding (new?) standard syntax. For example, let's see if can use the UNIX cron syntax as a standard syntax for cron jobs.


## CLI

CLI integration:
- `$ vite deploy logs` => server logs
- `$ vite deploy status` => deployment status, and downtime status for past 30 days
- `$ vite deploy ls` => e.g. number of workers, system metrics (CPU usage, mem usage)
- `$ vite deploy db` => connect to DB and run queries, e.g. `SELECT { title, release_date } FROM movies;`
  - `$ vite deploy db migrate` => connect to DB and run migrations
- `$ vite secrets` => manage production environment variables (e.g. `DB_PASSWORD`)
  - ```shell
    # Get all secrets
    $ vite deploy secrets list
    ```
  - ```shell
    # Set a secret
    $ vite deploy secrets set DB_PASSWORD lOK9uiUuCP75lMzQ
    ```

> [!NOTE]
> **Motivation: AI**
>
> AI cannot (practically) work with UIs — the CLI enables AI to access deployment information (e.g. deployment logs for debugging).

> [!NOTE]
> **Implementation**
>
> - We first quickly implement `$ vike deploy` (instead of `$ vite deploy`)
> - We talk to the Vite about adding `$ vite deploy` to Vite's CLI:
    - The Vite team has repeatedly shown interest of having Vite plugins be able to extend Vite's CLI (e.g. for supporting the idea that frameworks are "just Vite plugins")
    - We're currently working with the Vite team and the Vite ecosystem on [Vite deployment plugins](https://github.com/vitejs/vite/discussions/20907). Thus, adding a `deploy` CLI command is the next natural step.



## AI integration

How will deployment integration with AI workflows look like?

Example: error detected in deployment => AI is automatically prompted => AI can access deployment logs and source code => AI proposes fix => human review => fix is merged & deploy — the only human intervention here is reviewing the bug fix.
