Amit a [model](./Model.md) ténylegesen csinál. Adott [context](./Context.md) mellett mintavételez egy következő [token](./Token.md)-t, hozzáfűzi, majd újra fut. Minden output — egy mondat, egy [tool call](./Tool%20call.md), egy ezer soros fájl — tokenenként épül fel. A modelnek nincs más működési módja.

*Usage:*

"How does the [agent](./Agent.md) 'decide' to call a tool?"

"It doesn't — it's next-token prediction all the way down. The tool call is just a structured string the [harness](./Harness.md) parses out of the output stream."
