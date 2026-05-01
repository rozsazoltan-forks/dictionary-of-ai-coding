A [provider](./Model%20provider.md) oldalán lévő store, amely lehetővé teszi, hogy egymást követő [model provider requests](./Model%20provider%20request.md) kihagyják egy közös prefix újrafeldolgozását. Amikor egy request eleje megegyezik egy friss korábbi request elejével — ugyanaz a [system prompt](./System%20prompt.md), ugyanaz a history egy pontig —, a provider újrahasznosítja a korábbi munkát, és ezeket a [tokens](./Token.md)-t sokkal alacsonyabb áron [cache tokens](./Cache%20tokens.md)-ként számlázza.

Bármi, ami megváltoztatja a prefixet — fájlok átrendezése, system prompt átírása [session](./Session.md) közben, timestamp injektálása a tetejére — ettől a ponttól invalidálja a cache-t, és a request fennmaradó része teljes [input token](./Input%20tokens.md) áron számlázódik.

_Usage:_

"Why did the bill spike halfway through the session?"

"[Harness](./Harness.md) started injecting the current time into the system prompt every [turn](./Turn.md). Prefix cache breaks at the first changed token, so every request after that billed at full rate."
