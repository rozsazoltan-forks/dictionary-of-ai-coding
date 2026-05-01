Egy behatárolt interakciós futás egy [agent](./Agent.md)-tel. Üresen indul, felhalmoz messages-t, [tool results](./Tool%20result.md)-t és beolvasott fájlokat, majd akkor ér véget, amikor [cleared](./Clearing.md), bezáródik, vagy [compacted](./Compaction.md) formában friss sessionbe kerül. A session az, ami *feltölti* a [context window](./Context%20window.md)-t: ha a context window a doboz, a session az a tartalom, amely lassan megtölti. Ami túl nagy egyetlen context windowhoz, azt sessionökre kell bontani.

*Usage:*

"How long can one session run before it falls apart?"

"Depends on the work — a focused refactor stays sharp longer than open-ended research. Once the session bloats, [hand off](./Handoff.md) or compact, don't push through."
