Tények, amelyeket az [agent](./Agent.md) közvetlenül ki tud olvasni az aktuális [context](./Context.md)-ből: a felhasználó feladata, beolvasott fájlok, [tool results](./Tool%20result.md), a [session](./Session.md) indulásakor betöltött [AGENTS.md](./AGENTS.md.md) tartalom. A [parametric knowledge](./Parametric%20knowledge.md) párja: a parametric a parameters-ből *felidézett* tudás; a contextual a [window](./Context%20window.md)-ból *olvasott* tudás. [Hallucinations](./Hallucination.md) sokkal ritkábbak, ha az agent contextual knowledge alapján dolgozik — a válasz ott van előtte, nem egy elmosódott memóriából kell előkaparnia.

*Reach for this term* csak akkor, ha parametric knowledge-dzsel állítod szembe; különben elég azt mondani: **context**.

*Avoid:* "working memory" — a contextual knowledge az, ami *most* a window-ban van; a [memory system](./Memory%20system.md) az, ami cross-session tartalmat juttat oda. Más léptékek, ne keverd őket.

*Usage:*

"Why does it nail the API when I paste the docs and fabricate it when I don't?"

"With the docs in, it's contextual knowledge — reading off the page. Without, it's parametric and the rare endpoints blur."
