Amikor a [model](./Model.md) minden egyes [token](./Token.md)-t prediktál, figyelembe veszi a [context](./Context.md) összes többi tokenjét — némelyiket erősen, másokat alig. Két token közötti párosítás az **attention relationship**. A jelentéssel bíró párok — például "her" és "Sarah", vagy egy `getUser()` hívás és a hozzá tartozó `function getUser` definíció — erősebben hatnak egymásra, mint a nem kapcsolódó elemek. Egy N tokenes context nagyságrendileg N² relationshipet tartalmaz.

*Usage:*

"It keeps confusing the two `user` symbols across the diff — sounds like we're in the [dumb zone](./Smart%20zone.md)."

"Yeah, the attention relationship between each call site and its declaration is fighting the other one — same token shape, different bindings. Rename one and the pairings sharpen."
