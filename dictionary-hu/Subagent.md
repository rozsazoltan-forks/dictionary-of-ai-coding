Egy [agent](./Agent.md), amelyet egy másik agent indít [tool call](./Tool%20call.md)-on keresztül. Saját [session](./Session.md)-ben fut, saját [context window](./Context%20window.md)-val, és egyetlen [tool result](./Tool%20result.md)-ot jelent vissza. Különbözik a [handoff](./Handoff.md)-től: a parent kifejezetten választ vár; a handoffnak nincs visszaútja. **Nem indíthat további subagenteket** — a fa egy szint mély. A subagentek a [context](./Context.md) izolálására vannak, nem hierarchiák komponálására.

*Usage:*

"The grep results are blowing out my context."

"Spawn a subagent to do the search — it'll burn its own context window on the noise and report back the two file paths you actually need."
