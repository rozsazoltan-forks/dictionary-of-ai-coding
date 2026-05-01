Egységként csomagolt, betanítható capability: instrukciók és resource-ok egy konkrét feladat jó elvégzéséhez, az [environment](./Environment.md)-ben tartva, és csak relevancia esetén betöltve a [context window](./Context%20window.md)-ba. A [progressive disclosure](./Progressive%20disclosure.md) egysége egy [harness](./Harness.md)-ben.

*Avoid:* "[tool](./Tool.md)" — a tool olyasmi, amit az [agent](./Agent.md) *meghív*; a skill olyasmi, amit *elolvas*.

*Usage:*

"Where should I put the deploy runbook?"

"As a skill — the agent loads it only when the task involves deploys. In [AGENTS.md](./AGENTS.md.md) it'd burn [tokens](./Token.md) on every [turn](./Turn.md) for something we use weekly."
