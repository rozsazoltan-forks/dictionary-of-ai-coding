Az a világ, amelyen az [agent](./Agent.md) cselekszik — minden, ami a [harness](./Harness.md)-en kívül van, és amit az agent [tool results](./Tool%20result.md)-en keresztül érzékel, illetve [tool calls](./Tool%20call.md)-on keresztül módosít. A harness *futtatja* az agentet; az environment az, *amiben* az agent dolgozik. Egy [`AGENTS.md`](./AGENTS.md.md) fájl az environmentben él; a harness tölti be a [context window](./Context%20window.md)-ba. A [filesystem](./Filesystem.md) a leggyakoribb environment típus, de nem az egyetlen: adatbázis, távoli API vagy browser session is lehet environment.

*Avoid:* "environment" használata magára a runtime-ra vagy a harnessre — a harness a wrapper, az environment a workspace.

*Usage:*

"The agent can't see the staging DB schema."

"Wire it into the environment — give it a `psql` [tool](./Tool.md) scoped to read-only on staging. The harness is fine, it just has nothing to act on."
