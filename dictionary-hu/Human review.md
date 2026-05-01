A felhasználó elolvassa az [agent](./Agent.md) által készített kódot, és judgementet alkot róla. A diff vagy a módosított fájlok olvasása számít; az agent *leírásának* olvasása arról, hogy mit csinált, nem — a narration nem maga az artifact.

*Avoid:* "code review" önmagában — kétértelmű, lehet emberi vagy [automated](./Automated%20review.md).

*Usage:*

"I human-reviewed the [AFK](./AFK.md) output."

"You read the diff or just the summary?"

"Diff. The summary said it deleted dead code — turned out the function was called from a generated file."
