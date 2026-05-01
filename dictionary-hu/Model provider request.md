Egy round-trip a [harness](./Harness.md) és a [model provider](./Model%20provider.md) között. A harness elküldi az aktuális [context](./Context.md)-et; a provider visszaad egy választ: egy [tool call](./Tool%20call.md)-t vagy final answert. Egyetlen felhasználói üzenet sok model provider requestet is generálhat, ha az [agent](./Agent.md) [tools](./Tool.md)-t hív — minden [tool result](./Tool%20result.md) újabb requestet indít.

*Usage:*

"One question burned forty thousand [tokens](./Token.md)?"

"Look at the tool calls — twelve grep, eight read, four edits. Each tool result spawns another model provider request, and the whole [session](./Session.md) prefix re-sends every time."
