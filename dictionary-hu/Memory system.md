Olyan rendszer, amely megpróbálja az [agent](./Agent.md)-et [stateful](./Stateful.md)-lá tenni [sessions](./Session.md) között. A session során információt persistál az [environment](./Environment.md)-be, majd jövőbeli sessionök elején visszatölti a [context window](./Context%20window.md)-ba, így az agent folytonosságot hordoz akkor is, ha a felhasználó [clearing](./Clearing.md)-gel lezárja az előző sessiont.

*Usage:*

"I keep having to re-tell it I'm on Postgres, not MySQL."

"Wire up a memory system — write what it learns to the [filesystem](./Filesystem.md) on the first [turn](./Turn.md), reload it at session start. The [model](./Model.md) itself is [stateless](./Stateless.md); the memory layer fakes continuity."
