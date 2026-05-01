Minden, ami a [model](./Model.md) körül van, és [agent](./Agent.md)-té alakítja: [tools](./Tool.md), [system prompt](./System%20prompt.md), [context-window management](./Context%20window.md), permissions, hooks. **Claude.ai** és **Claude Code** ugyanazon a modellen is futhat, mégis másképp viselkedik, mert más a harnessük.

*Usage:*

"Same model, why is Claude Code editing files and Claude.ai just answering questions?"

"Different harnesses — Claude Code has [filesystem](./Filesystem.md) tools, a different system prompt, and a permission layer. The model isn't the variable here."
