Egy [handoff artifact](./Handoff%20artifact.md), amely egyetlen [session](./Session.md) munkakörét határolja le. Állhat önmagában, vagy egy [spec](./Spec.md) gyermekeként. A tickets blokkolhatják egymást vagy függhetnek testvér ticketektől, így a munka sorrendje nem lineáris tervből, hanem dependency graphból következik.

*Usage:*

"Where do I start on the migration spec?"

"Look at the ticket graph — the schema change blocks the backfill, the backfill blocks the API switch. Pick a leaf and run a session on it."
