Egy [agent](./Agent.md) egy másik agent munkáját review-zza, gyakran más [model](./Model.md)-lel vagy [system prompt](./System%20prompt.md)-tal. Nem determinisztikus: judgementet alkot. Bárhol futhat — PR előtt, commit historyn utólag, vagy [subagent](./Subagent.md)-ként session közben. Egy LLM-as-judge CI-ben automated review, nem [automated check](./Automated%20check.md); a kategóriát az dönti el, mit *csinál* az assertion, nem az, hol fut.

*Avoid:* "AI review" / "agent review" — túl homályosak, nem különítik el a working agenttől.

*Usage:*

"We're getting too many bad PRs from the [AFK](./AFK.md) runs."

"Add an automated review step before merge — different model, separate system prompt, scoped to security and contract changes."
