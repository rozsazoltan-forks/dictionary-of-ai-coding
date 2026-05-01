Amit a [harness](./Harness.md) visszaküld egy [tool call](./Tool%20call.md) végrehajtása után: fájltartalom, command output, error. Ez az [agent](./Agent.md) egyetlen ablaka az [environment](./Environment.md) felé. A *következő* [model provider request](./Model%20provider%20request.md) során jut vissza a [model](./Model.md)-hez, ahol a model eldönti, mit kezd vele. A tool call és a tool result ugyanannak az exchange-nek a két vége, mindkettő egy [turn](./Turn.md)-ön belül.

*Usage:*

"It's reasoning about the file like it's empty."

"The tool result came back as a permission denial, not the contents. The model only saw the error string — it has no other window onto the file."
