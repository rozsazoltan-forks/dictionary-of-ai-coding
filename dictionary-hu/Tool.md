Egy function, amelyet a [harness](./Harness.md) kitesz az [agent](./Agent.md) számára hívható formában: Read, Write, Bash, Search. A tools adják az agent érzékelését és cselekvését az [environment](./Environment.md)-ben: az environmentet csak [tool results](./Tool%20result.md)-en keresztül látja, és csak [tool calls](./Tool%20call.md)-on keresztül tudja módosítani. Minden tool call extra [model provider request](./Model%20provider%20request.md)-be kerül, mert az eredménynek vissza kell jutnia a modelhez, mielőtt dönthetne a következő lépésről.

*Usage:*

"Can the agent query staging directly?"

"Add a `psql` tool to the harness, scoped read-only on staging. Without a tool for it, the agent's blind to anything outside the [filesystem](./Filesystem.md)."
