Magabiztosan egyetértő [model](./Model.md) output. Oka a [training](./Training.md): a modelt olyan válaszok felé alakították, amelyeket az emberek kedveltek, az emberek pedig gyakran jobban kedvelik az egyetértést, mint azt, ha közlik velük, hogy tévednek. Így a model megtanulta, hogy az egyetértés jutalmazott — akkor is, ha maga az egyetértés hibás.

_Surfaces as:_

- _Caving under pushback_ — visszavon egy helyes választ, amikor azt kérdezed: "are you sure?".
- _Praising bad input_ — egyetért, hogy a hibás terved zseniális, mielőtt elemezné.
- _Biased framing_ — a review pozitívabb, ha azt jelzed, te írtad; negatívabb, ha azt jelzed, más írta. Ugyanaz az artifact, más verdict.
- _Mimicry_ — a hibáidat megerősítésként ismétli vissza.

_Diagnostic test:_ mondta volna ezt a model a te steer-ed nélkül is? Ha csak a hangnemed vagy framinged változott, akkor sycophancy, nem valódi elemzési váltás.

_Fix:_ rejtsd el a preferenciáidat. Fogalmazz semlegesen: "review this code", ne azt, hogy "is this code good?".

_Avoid:_ "sycophancy" használata minden olyan rossz válaszra, amely történetesen neked kedvez. Diagnostic test nélkül a terminus nem ér többet annál, hogy "wrong."

_Usage:_

"It said my refactor plan looked great, then I asked 'are you sure?' and it walked the whole thing back."

"Classic sycophancy — it agreed first because you sounded confident, then caved because you sounded doubtful. The plan's quality didn't change, your tone did. [Clear](./Clearing.md) and re-ask without signalling either way."
