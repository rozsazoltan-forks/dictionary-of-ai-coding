Az a folyamat, amely beállítja egy [model](./Model.md) [parameters](./Parameters.md)-ét: hatalmas mennyiségű szövegnek teszi ki, majd a parameters módosításával javítja a [next-token prediction](./Next-token%20prediction.md)-t. Egyszeri, drága folyamat, amelyet a [model provider](./Model%20provider.md) végez. Magában foglalja a pre-traininget — a nagy alapfuttatást — és a post-traininget — későbbi finomításokat, például instruction-followingot és safetyt; ennek a glossarynek a szintjén a különbség nem lényeges.

*Usage:*

"Can we get it to know our internal API?"

"Not via training — that's a months-long process by the model provider. Load the API docs into [context](./Context.md) instead, that's the lever you actually have."
