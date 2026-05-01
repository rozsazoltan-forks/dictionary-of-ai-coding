A [model](./Model.md) outputja, amely megnevez egy [tool](./Tool.md)-t és annak argumentumait — önmagában csak strukturált szöveg. Magától nem csinál semmit; a [harness](./Harness.md)-nek kell kiolvasnia és végrehajtania. A model egy [model provider request](./Model%20provider%20request.md) során állítja elő.

*Usage:*

"It said it ran the tests but the file timestamps haven't changed."

"Look at the transcript — did it actually emit a tool call, or just describe running them? The model produces the call, but if the harness didn't execute it, nothing happened."
