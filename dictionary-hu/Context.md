Az a releváns információ, amelyhez az [agent](./Agent.md) éppen hozzáfér. Absztrakt főnév: nem a nyers input, amit a model lát — az a [context window](./Context%20window.md) —, és nem a futó history — az a [session](./Session.md) —, hanem *amit az agent a feladat szempontjából tud*. "Loading something into context" azt jelenti, hogy az adott információ bekerül ebbe a halmazba; a "context engineering" ennek a gondozása.

*Usage:*

"It keeps inventing fields that aren't in the type."

"The type file isn't in context — it's reading the call sites and guessing. Read the definition in first."
