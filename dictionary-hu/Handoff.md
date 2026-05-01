[Agent](./Agent.md) [context](./Context.md) átvitele egyik [session](./Session.md)-ből egy másikba, visszaút nélkül. A hordozómechanizmus változhat: írott [handoff artifact](./Handoff%20artifact.md), memórián belüli összefoglaló ([compaction](./Compaction.md)) és más megoldások. Különbözik a [clearing](./Clearing.md)-től, ahol nincs transzfer. Okai lehetnek: szerepváltás (planner → implementer), [AFK](./AFK.md) run indítása, párhuzamos sessionökre bontás, vagy hely felszabadítása a [context window](./Context%20window.md)-ban.

*Usage:*

"Planning session is getting heavy — should I just keep going?"

"Do a handoff. Write the decisions to a doc, clear, start the implementation in a fresh session reading from it."
