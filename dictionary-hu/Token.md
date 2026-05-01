Az atomikus egység, amelyet a [model](./Model.md) olvas és ír. Nagyjából szó méretű, de nem pontosan: gyakori szavak egy tokenek, ritka vagy hosszú szavak több tokenre esnek szét. A [context window](./Context%20window.md) mérete, a költség és a latency mind tokens-ben mérődik.

*Avoid:* "word" — a tokenhatárok nem egyeznek meg a szóhatárokkal, és a tokens-per-second / tokens-per-dollar azok az egységek, amelyek ténylegesen számítanak.

*Usage:*

"How big is this prompt going to be?"

"Run it through the tokenizer — the schema's compact but the JSON keys are weird, so they'll split into more tokens than you think."
