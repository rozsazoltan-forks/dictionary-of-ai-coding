Magabiztosan hibás [model](./Model.md) output. Két típusa van, eltérő okokkal és javításokkal:

- *Factuality hallucination* — kitalált vagy hibás tények a világról: nem létező function, rossz API signature, fake citation. Oka gyakran [parametric knowledge](./Parametric%20knowledge.md) hiányosság, különösen a [knowledge cutoff](./Knowledge%20cutoff.md) után. Fix: töltsd be a megfelelő [contextual knowledge](./Contextual%20knowledge.md)-t.
- *Faithfulness hallucination* — az output eltávolodik a betöltött **contextual knowledge**-től, a felhasználói instrukcióktól vagy a model saját korábbi reasoningjétől. Ez [attention degradation](./Attention%20degradation.md) tünete; a [dumb zone](./Smart%20zone.md)-ban romlik. Fix: [clear](./Clearing.md) vagy [compact](./Compaction.md).

*Avoid:* "hallucination" mint puszta szinonima arra, hogy "wrong" — ha nem nevezed meg a típust, diagnosztikailag keveset ér.

*Usage:*

"It hallucinated a `parseAsync` method on the schema."

"Factuality or faithfulness?"

"The method exists in the docs I pasted — it just stopped reading them after [turn](./Turn.md) forty."

"Faithfulness then. Compact and reload, don't bother adding more docs."
