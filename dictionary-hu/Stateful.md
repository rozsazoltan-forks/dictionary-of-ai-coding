Információt visz tovább. Egy [session](./Session.md) [turns](./Turn.md) között stateful: a [context](./Context.md) halmozódik, ahogy a session fut, ezért sodródnak a hosszú sessionök a [dumb zone](./Smart%20zone.md) felé. Egy [agent](./Agent.md) **sessions** között is stateful-lá tehető, ha [memory system](./Memory%20system.md) persistálja az információt az [environment](./Environment.md)-be, majd jövőbeli sessionök elején visszatölti. A [model](./Model.md) soha nem stateful; minden látszólagos folytonosság abból ered, hogy a [harness](./Harness.md) újra beadja neki a contextet. A [stateless](./Stateless.md) párja.

*Usage:*

"It remembered my preferences from yesterday — does that mean the model learned them?"

"No, the agent's stateful because the harness wrote them to a memory file and reloaded them at session start. The model itself saw nothing of yesterday."
