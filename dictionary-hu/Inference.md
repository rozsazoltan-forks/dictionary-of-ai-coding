Egy betanított [model](./Model.md) futtatása output generálására — ez történik minden [model provider request](./Model%20provider%20request.md) során. A [parameters](./Parameters.md) változatlanok maradnak; a model csak [next-token prediction](./Next-token%20prediction.md)-t végez a kapott [context](./Context.md) alapján. A [training](./Training.md)-hez képest olcsó, de [token](./Token.md) alapon számlázott, és a modelhasználat domináns költsége.

*Usage:*

"Why does the bill scale with usage instead of being a flat license?"

"You're paying for inference — every model provider request runs the model on the provider's hardware. Training already happened, but inference costs accrue per request, and a single [turn](./Turn.md) can expand into many requests when [tools](./Tool.md) are called."
