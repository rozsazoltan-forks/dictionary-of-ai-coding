[Input tokens](./Input%20tokens.md), amelyeket a [provider](./Model%20provider.md) egy korábbi [model provider request](./Model%20provider%20request.md)-ből cache-elt, hogy ne kelljen újra feldolgoznia őket. Amikor egymást követő requestek közös prefixet használnak, a provider a [prefix cache](./Prefix%20cache.md)-en keresztül újrahasznosítja a korábbi munkát, és a cached részt sokkal alacsonyabb áron számlázza. Ez teszi megfizethetővé a hosszú [sessions](./Session.md)-t — nélküle minden [turn](./Turn.md) újra kifizettetné a teljes historyt.

*Usage:*

"Cost on long sessions is brutal — eight bucks for a refactor."

"Check the cache tokens. If the [harness](./Harness.md) is reordering the [system prompt](./System%20prompt.md) or files between turns, the prefix breaks and you re-pay full input rate every request."
