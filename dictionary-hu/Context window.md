Minden, amit a [model](./Model.md) lát egy-egy [model provider request](./Model%20provider%20request.md) során. Véges, model-specifikus, és ez az *egyetlen* felület, amelyen keresztül a model bármit érzékel.

*Avoid:* "memory" — a context window working state, és nem marad meg [sessions](./Session.md) között. A [Memory](./Memory%20system.md) külön réteg erre építve.

*Usage:*

"Can I just paste the whole monorepo into the prompt?"

"The context window's 200k [tokens](./Token.md) — that's maybe a fifth of the repo. Pick the files the task touches, leave the rest behind a [tool call](./Tool%20call.md)."
