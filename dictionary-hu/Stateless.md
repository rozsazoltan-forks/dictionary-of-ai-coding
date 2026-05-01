Nem visz tovább információt. A [model](./Model.md) [model provider requests](./Model%20provider%20request.md) között stateless: minden request újraküldi a teljes [context window](./Context%20window.md)-t, mert a model nem lát mást. Egy [agent](./Agent.md) alapértelmezetten [sessions](./Session.md) között stateless: az új session üresen indul, korábbi sessionök nyoma nélkül. A [stateful](./Stateful.md) párja.

*Usage:*

"Why does it forget the convention every time I [clear](./Clearing.md)?"

"The model's stateless — the new session starts empty. If you want it carried, write it to [AGENTS.md](./AGENTS.md.md) or a memory file the [harness](./Harness.md) loads at session start."
