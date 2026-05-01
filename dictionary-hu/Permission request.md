Amit a [harness](./Harness.md) megmutat a felhasználónak, mielőtt végrehajtana egy előzetesen nem jóváhagyott [tool call](./Tool%20call.md)-t. A [model](./Model.md) létrehoz egy tool callt; ahelyett, hogy a harness azonnal futtatná, megáll és kérdez. Jóváhagyás esetén fut; elutasítás esetén a harness az elutasítást [tool result](./Tool%20result.md)-ként jelenti vissza a modelnek. Ez a mechanizmus teszi az embert a [loop](./Human-in-the-loop.md)-ba kockázatos vagy érzékeny actionöknél.

*Usage:*

"It's been blocked on a permission request for ten minutes — I was in a meeting."

"That's the cost of human-in-the-loop. Pre-approve the safe [tools](./Tool.md) so the request only fires on the actually-risky calls."
