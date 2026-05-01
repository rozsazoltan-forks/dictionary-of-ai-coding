<!--
  GENERATED FILE — DO NOT EDIT.
  Source: dictionary-hu/*.md, internal/Curriculum.hu.md, internal/README.template.hu.md
  Regenerate: npm run generate:hu
-->

# AI Coding Dictionary — magyar kiadás

**Az AI coding elsőre könnyen tűnhet úgy, mintha csak szakértőknek szólna.** Megmagyarázatlan jargon. Rejtélyes hibák. Számlák, amelyek nem mindig látszanak arányban az elvégzett munkával.

Valójában nem erről van szó. A zavar nagy része mesterséges: **egy egész VC-funded gazdaság épült arra, hogy ezt a területet nehéz legyen átlátni**.

Az alapfogalmak egy délután alatt megtanulhatók. Ha megvannak, az egész kevésbé érződik találgatásnak.

Miért romlik a context? Miért ilyen magas a számla? Miért viselkedik ugyanaz a prompt másképp egyik napról a másikra?

Mindegyikre van tiszta válasz — amint valaki megmutatja, milyen szavakat kell használni.

Ezért készült ez a dictionary: **az AI coding szókincse magyarul elmagyarázva, az eredeti szakmai angol terminológia megtartásával**.

Az angol címszavakat és a fejlesztői példamondatokat szándékosan megtartottam. A cél nem az, hogy a szakmai nyelv eltűnjön, hanem hogy a magyar olvasó értse, pontosan mit jelentenek ezek a fogalmak issue-kban, PR-ekben, dokumentációban és AI coding toolokban.

**Want more than the vocabulary?** Join 62,000+ developers at **[aihero.dev/newsletter](https://www.aihero.dev/s/dictionary-newsletter)** for the original author's latest skills, thinking on AI engineering, and resources.

---

## Tartalomjegyzék

<details>
<summary>Section 1 — A model</summary>

- [Model](#model)
- [Parameters](#parameters)
- [Training](#training)
- [Inference](#inference)
- [Token](#token)
- [Next-token prediction](#next-token-prediction)
- [Non-determinism](#non-determinism)
- [Model provider](#model-provider)
- [Harness](#harness)
- [Model provider request](#model-provider-request)
- [Input tokens](#input-tokens)
- [Output tokens](#output-tokens)
- [Prefix cache](#prefix-cache)
- [Cache tokens](#cache-tokens)

</details>

<details>
<summary>Section 2 — Sessions, context windows és turns</summary>

- [Stateless](#stateless)
- [Context](#context)
- [Context window](#context-window)
- [Stateful](#stateful)
- [Agent](#agent)
- [System prompt](#system-prompt)
- [Session](#session)
- [Turn](#turn)

</details>

<details>
<summary>Section 3 — Tools és environment</summary>

- [Environment](#environment)
- [Filesystem](#filesystem)
- [Tool](#tool)
- [Tool call](#tool-call)
- [Tool result](#tool-result)
- [Permission request](#permission-request)
- [Permission mode](#permission-mode)
- [Agent mode](#agent-mode)
- [Sandbox](#sandbox)

</details>

<details>
<summary>Section 4 — Failure modes</summary>

- [Sycophancy](#sycophancy)
- [Hallucination](#hallucination)
- [Parametric knowledge](#parametric-knowledge)
- [Knowledge cutoff](#knowledge-cutoff)
- [Contextual knowledge](#contextual-knowledge)
- [Attention relationship](#attention-relationship)
- [Attention budget](#attention-budget)
- [Attention degradation](#attention-degradation)
- [Smart zone](#smart-zone)

</details>

<details>
<summary>Section 5 — Handoffs</summary>

- [Clearing](#clearing)
- [Handoff](#handoff)
- [Handoff artifact](#handoff-artifact)
- [Spec](#spec)
- [Ticket](#ticket)
- [Compaction](#compaction)
- [Autocompact](#autocompact)

</details>

<details>
<summary>Section 6 — Memory és steering</summary>

- [Memory system](#memory-system)
- [AGENTS.md](#agentsmd)
- [Progressive disclosure](#progressive-disclosure)
- [Skill](#skill)
- [Subagent](#subagent)

</details>

<details>
<summary>Section 7 — Working patterns</summary>

- [Human-in-the-loop](#human-in-the-loop)
- [AFK](#afk)
- [Automated check](#automated-check)
- [Automated review](#automated-review)
- [Human review](#human-review)
- [Vibe coding](#vibe-coding)
- [Design concept](#design-concept)
- [Grilling](#grilling)

</details>

## Section 1 — A model

### Model

A [parameters](#parameters). [Stateless](#stateless): [next-token prediction](#next-token-prediction)-t végez, és semmi mást. "Claude Opus 4.7" és "GPT-5" modellek. Önmagában egy model nem tud agentic módon működni; [harnessed](#harness) formába kell kerülnie.

*Usage:*

"Should we switch the model from Sonnet to Opus for the planning step?"

"Try it — but the harness is doing most of the lifting on this task. The model swap won't help if the [system prompt](#system-prompt) and [tools](#tool) are wrong."

### Parameters

A [model](#model) belsejében lévő számok — gyakran milliárdnyi érték —, amelyeket [training](#training) során hangolnak. Minden, amit a model "tud", ezekben él. A training beállítja őket; az [inference](#inference) változatlanul használja őket. Más néven *weights*.

*Usage:*

"Can we fine-tune it on our codebase?"

"That'd update the parameters — different model afterwards. For one project it's almost always cheaper to load the codebase as [context](#context) than to retrain."

### Training

Az a folyamat, amely beállítja egy [model](#model) [parameters](#parameters)-ét: hatalmas mennyiségű szövegnek teszi ki, majd a parameters módosításával javítja a [next-token prediction](#next-token-prediction)-t. Egyszeri, drága folyamat, amelyet a [model provider](#model-provider) végez. Magában foglalja a pre-traininget — a nagy alapfuttatást — és a post-traininget — későbbi finomításokat, például instruction-followingot és safetyt; ennek a glossarynek a szintjén a különbség nem lényeges.

*Usage:*

"Can we get it to know our internal API?"

"Not via training — that's a months-long process by the model provider. Load the API docs into [context](#context) instead, that's the lever you actually have."

### Inference

Egy betanított [model](#model) futtatása output generálására — ez történik minden [model provider request](#model-provider-request) során. A [parameters](#parameters) változatlanok maradnak; a model csak [next-token prediction](#next-token-prediction)-t végez a kapott [context](#context) alapján. A [training](#training)-hez képest olcsó, de [token](#token) alapon számlázott, és a modelhasználat domináns költsége.

*Usage:*

"Why does the bill scale with usage instead of being a flat license?"

"You're paying for inference — every model provider request runs the model on the provider's hardware. Training already happened, but inference costs accrue per request, and a single [turn](#turn) can expand into many requests when [tools](#tool) are called."

### Token

Az atomikus egység, amelyet a [model](#model) olvas és ír. Nagyjából szó méretű, de nem pontosan: gyakori szavak egy tokenek, ritka vagy hosszú szavak több tokenre esnek szét. A [context window](#context-window) mérete, a költség és a latency mind tokens-ben mérődik.

*Avoid:* "word" — a tokenhatárok nem egyeznek meg a szóhatárokkal, és a tokens-per-second / tokens-per-dollar azok az egységek, amelyek ténylegesen számítanak.

*Usage:*

"How big is this prompt going to be?"

"Run it through the tokenizer — the schema's compact but the JSON keys are weird, so they'll split into more tokens than you think."

### Next-token prediction

Amit a [model](#model) ténylegesen csinál. Adott [context](#context) mellett mintavételez egy következő [token](#token)-t, hozzáfűzi, majd újra fut. Minden output — egy mondat, egy [tool call](#tool-call), egy ezer soros fájl — tokenenként épül fel. A modelnek nincs más működési módja.

*Usage:*

"How does the [agent](#agent) 'decide' to call a tool?"

"It doesn't — it's next-token prediction all the way down. The tool call is just a structured string the [harness](#harness) parses out of the output stream."

### Non-determinism

Ugyanaz az input különböző outputot adhat. Ha kétszer futtatsz egy [model](#model)-t azonos [context](#context)-tel, két eltérő választ kaphatsz — néha csak egy szóban, néha teljesen más megközelítésben. Ehhez a kódodnak semmit sem kell változnia.

Ez része annak, ahogyan a modellek szöveget generálnak, és ahogyan a [model providers](#model-provider) kiszolgálják a [requests](#model-provider-request)-eket. Nincs olyan kapcsoló, amellyel teljesen eltüntethető.

Számíts eredményszórásra, amikor egy [agent](#agent) ugyanazon a feladaton dolgozik. Egyik nap élesnek tűnik a model; másik nap úgy, mintha elvesztette volna a fonalat. Ugyanaz a task, más dobás.

Ne narrativizáld túl. Az emberek pattern-matching gépek, és néhány rossz futás könnyen úgy érződik, mintha "the model got worse this week" bizonyítéka lenne. Többnyire csak a distribution.

_Usage:_

"Claude has been awful today. Did they ship a worse version?"

"Probably not — model output is non-deterministic. You're going to have good days and bad days on the same task. Try again tomorrow before you go looking for a cause."

### Model provider

Ami egy [model](#model)-t kiszolgál [inference](#inference)-hez. Általában távoli service — Anthropic, OpenAI, Google —, de lehet lokális is: Ollama, LM Studio, llama.cpp a saját gépeden. A [harness](#harness) nem maga futtatja a modelt; megkér egy providert.

*Usage:*

"Can we run this offline for the air-gapped client?"

"Swap the model provider to a local one — Ollama or llama.cpp on their box. The harness doesn't care, it just hits a different endpoint."

### Harness

Minden, ami a [model](#model) körül van, és [agent](#agent)-té alakítja: [tools](#tool), [system prompt](#system-prompt), [context-window management](#context-window), permissions, hooks. **Claude.ai** és **Claude Code** ugyanazon a modellen is futhat, mégis másképp viselkedik, mert más a harnessük.

*Usage:*

"Same model, why is Claude Code editing files and Claude.ai just answering questions?"

"Different harnesses — Claude Code has [filesystem](#filesystem) tools, a different system prompt, and a permission layer. The model isn't the variable here."

### Model provider request

Egy round-trip a [harness](#harness) és a [model provider](#model-provider) között. A harness elküldi az aktuális [context](#context)-et; a provider visszaad egy választ: egy [tool call](#tool-call)-t vagy final answert. Egyetlen felhasználói üzenet sok model provider requestet is generálhat, ha az [agent](#agent) [tools](#tool)-t hív — minden [tool result](#tool-result) újabb requestet indít.

*Usage:*

"One question burned forty thousand [tokens](#token)?"

"Look at the tool calls — twelve grep, eight read, four edits. Each tool result spawns another model provider request, and the whole [session](#session) prefix re-sends every time."

### Input tokens

[Tokens](#token), amelyeket a [harness](#harness) elküld minden [model provider request](#model-provider-request) során. Általában alacsonyabb áron számlázódnak, mint az [output tokens](#output-tokens).

*Usage:*

"Bill's high but the [agent](#agent)'s barely writing anything."

"It's the input tokens — every [turn](#turn) re-sends the whole [session](#session). Without the [prefix cache](#prefix-cache) you re-pay for the history each request."

### Output tokens

[Tokens](#token), amelyeket a [model](#model) visszagenerál. Általában magasabb áron számlázódnak, mint az [input tokens](#input-tokens), mert több compute kell az előállításukhoz.

*Usage:*

"The refactor [session](#session) is burning through credit even though the inputs are small."

"[Agent](#agent)'s rewriting whole files instead of patching. Output tokens cost roughly five times the input rate — get it emitting edits and the bill drops."

### Prefix cache

A [provider](#model-provider) oldalán lévő store, amely lehetővé teszi, hogy egymást követő [model provider requests](#model-provider-request) kihagyják egy közös prefix újrafeldolgozását. Amikor egy request eleje megegyezik egy friss korábbi request elejével — ugyanaz a [system prompt](#system-prompt), ugyanaz a history egy pontig —, a provider újrahasznosítja a korábbi munkát, és ezeket a [tokens](#token)-t sokkal alacsonyabb áron [cache tokens](#cache-tokens)-ként számlázza.

Bármi, ami megváltoztatja a prefixet — fájlok átrendezése, system prompt átírása [session](#session) közben, timestamp injektálása a tetejére — ettől a ponttól invalidálja a cache-t, és a request fennmaradó része teljes [input token](#input-tokens) áron számlázódik.

_Usage:_

"Why did the bill spike halfway through the session?"

"[Harness](#harness) started injecting the current time into the system prompt every [turn](#turn). Prefix cache breaks at the first changed token, so every request after that billed at full rate."

### Cache tokens

[Input tokens](#input-tokens), amelyeket a [provider](#model-provider) egy korábbi [model provider request](#model-provider-request)-ből cache-elt, hogy ne kelljen újra feldolgoznia őket. Amikor egymást követő requestek közös prefixet használnak, a provider a [prefix cache](#prefix-cache)-en keresztül újrahasznosítja a korábbi munkát, és a cached részt sokkal alacsonyabb áron számlázza. Ez teszi megfizethetővé a hosszú [sessions](#session)-t — nélküle minden [turn](#turn) újra kifizettetné a teljes historyt.

*Usage:*

"Cost on long sessions is brutal — eight bucks for a refactor."

"Check the cache tokens. If the [harness](#harness) is reordering the [system prompt](#system-prompt) or files between turns, the prefix breaks and you re-pay full input rate every request."

## Section 2 — Sessions, context windows és turns

### Stateless

Nem visz tovább információt. A [model](#model) [model provider requests](#model-provider-request) között stateless: minden request újraküldi a teljes [context window](#context-window)-t, mert a model nem lát mást. Egy [agent](#agent) alapértelmezetten [sessions](#session) között stateless: az új session üresen indul, korábbi sessionök nyoma nélkül. A [stateful](#stateful) párja.

*Usage:*

"Why does it forget the convention every time I [clear](#clearing)?"

"The model's stateless — the new session starts empty. If you want it carried, write it to [AGENTS.md](#agentsmd) or a memory file the [harness](#harness) loads at session start."

### Context

Az a releváns információ, amelyhez az [agent](#agent) éppen hozzáfér. Absztrakt főnév: nem a nyers input, amit a model lát — az a [context window](#context-window) —, és nem a futó history — az a [session](#session) —, hanem *amit az agent a feladat szempontjából tud*. "Loading something into context" azt jelenti, hogy az adott információ bekerül ebbe a halmazba; a "context engineering" ennek a gondozása.

*Usage:*

"It keeps inventing fields that aren't in the type."

"The type file isn't in context — it's reading the call sites and guessing. Read the definition in first."

### Context window

Minden, amit a [model](#model) lát egy-egy [model provider request](#model-provider-request) során. Véges, model-specifikus, és ez az *egyetlen* felület, amelyen keresztül a model bármit érzékel.

*Avoid:* "memory" — a context window working state, és nem marad meg [sessions](#session) között. A [Memory](#memory-system) külön réteg erre építve.

*Usage:*

"Can I just paste the whole monorepo into the prompt?"

"The context window's 200k [tokens](#token) — that's maybe a fifth of the repo. Pick the files the task touches, leave the rest behind a [tool call](#tool-call)."

### Stateful

Információt visz tovább. Egy [session](#session) [turns](#turn) között stateful: a [context](#context) halmozódik, ahogy a session fut, ezért sodródnak a hosszú sessionök a [dumb zone](#smart-zone) felé. Egy [agent](#agent) **sessions** között is stateful-lá tehető, ha [memory system](#memory-system) persistálja az információt az [environment](#environment)-be, majd jövőbeli sessionök elején visszatölti. A [model](#model) soha nem stateful; minden látszólagos folytonosság abból ered, hogy a [harness](#harness) újra beadja neki a contextet. A [stateless](#stateless) párja.

*Usage:*

"It remembered my preferences from yesterday — does that mean the model learned them?"

"No, the agent's stateful because the harness wrote them to a memory file and reloaded them at session start. The model itself saw nothing of yesterday."

### Agent

Egy [model](#model), amelyet [tools](#tool), [system prompt](#system-prompt) és [context window](#context-window) vesz körül a [harness](#harness)-en keresztül, és amely [turns](#turn) formájában kommunikál a felhasználóval. *Claude Code is an agent. Cursor is an agent. Claude.ai is an agent.* Az agent az, amivel ténylegesen beszélsz: nem pusztán maga a model, hanem a model működés közben, adott célra konfigurálva.

*Avoid:* "the AI", "the bot" — túl homályosak, mert elrejtik, hogy a parameters-ről vagy a harnessed rendszerről beszélsz.

*Usage:*

"Which agent are you using for the migration?"

"Claude Code locally, Cursor for the UI work — same model underneath, different harnesses."

### System prompt

Azok az instrukciók, amelyeket a [harness](#harness) minden [model provider request](#model-provider-request) elé illeszt — az [agent](#agent) állandó briefje: ki ő, hogyan viselkedjen, milyen [tools](#tool)-t hívhat, milyen konvenciókat kövessen. Általában stabil egy [session](#session) során.

*Usage:*

"Two harnesses, same [model](#model), totally different behavior on the same prompt."

"Different system prompts. One's tuned for terse code edits, the other for explaining — that's where the divergence lives, before your message even arrives."

### Session

Egy behatárolt interakciós futás egy [agent](#agent)-tel. Üresen indul, felhalmoz messages-t, [tool results](#tool-result)-t és beolvasott fájlokat, majd akkor ér véget, amikor [cleared](#clearing), bezáródik, vagy [compacted](#compaction) formában friss sessionbe kerül. A session az, ami *feltölti* a [context window](#context-window)-t: ha a context window a doboz, a session az a tartalom, amely lassan megtölti. Ami túl nagy egyetlen context windowhoz, azt sessionökre kell bontani.

*Usage:*

"How long can one session run before it falls apart?"

"Depends on the work — a focused refactor stays sharp longer than open-ended research. Once the session bloats, [hand off](#handoff) or compact, don't push through."

### Turn

Egy felhasználói üzenet és minden, amit az [agent](#agent) válaszként tesz addig, amíg vissza nem adja a szót a felhasználónak. Egy vagy több [model provider requests](#model-provider-request)-et tartalmaz — sokat, ha az agent [tools](#tool)-t hív. Egy tisztázó kérdés lezárja a turnt; a válaszod megnyitja a következőt. A hierarchia: [session](#session) **> Turn > Model provider request**.

*Usage:*

"One turn took two minutes?"

"It made fourteen [tool calls](#tool-call) inside that turn — each one is a separate model provider request. Latency stacks up before the agent finally yields back to you."

## Section 3 — Tools és environment

### Environment

Az a világ, amelyen az [agent](#agent) cselekszik — minden, ami a [harness](#harness)-en kívül van, és amit az agent [tool results](#tool-result)-en keresztül érzékel, illetve [tool calls](#tool-call)-on keresztül módosít. A harness *futtatja* az agentet; az environment az, *amiben* az agent dolgozik. Egy [`AGENTS.md`](#agentsmd) fájl az environmentben él; a harness tölti be a [context window](#context-window)-ba. A [filesystem](#filesystem) a leggyakoribb environment típus, de nem az egyetlen: adatbázis, távoli API vagy browser session is lehet environment.

*Avoid:* "environment" használata magára a runtime-ra vagy a harnessre — a harness a wrapper, az environment a workspace.

*Usage:*

"The agent can't see the staging DB schema."

"Wire it into the environment — give it a `psql` [tool](#tool) scoped to read-only on staging. The harness is fine, it just has nothing to act on."

### Filesystem

Fájlok és könyvtárak fája, amelyből az [agent](#agent) olvas, amelybe ír, és amelyben parancsokat futtat — coding agent esetén ez az alapértelmezett [environment](#environment). [AGENTS.md](#agentsmd), [skills](#skill), source code, build scripts és [tool](#tool) configok mind filesystemben élnek. Amikor egy [harness](#harness) "starts in your project", valójában egy filesystemre irányítja az agentet.

*Usage:*

"Why isn't it picking up my AGENTS.md?"

"It's running against a different filesystem — the [sandbox](#sandbox) mounted the parent dir, not the project root. Repoint the harness."

### Tool

Egy function, amelyet a [harness](#harness) kitesz az [agent](#agent) számára hívható formában: Read, Write, Bash, Search. A tools adják az agent érzékelését és cselekvését az [environment](#environment)-ben: az environmentet csak [tool results](#tool-result)-en keresztül látja, és csak [tool calls](#tool-call)-on keresztül tudja módosítani. Minden tool call extra [model provider request](#model-provider-request)-be kerül, mert az eredménynek vissza kell jutnia a modelhez, mielőtt dönthetne a következő lépésről.

*Usage:*

"Can the agent query staging directly?"

"Add a `psql` tool to the harness, scoped read-only on staging. Without a tool for it, the agent's blind to anything outside the [filesystem](#filesystem)."

### Tool call

A [model](#model) outputja, amely megnevez egy [tool](#tool)-t és annak argumentumait — önmagában csak strukturált szöveg. Magától nem csinál semmit; a [harness](#harness)-nek kell kiolvasnia és végrehajtania. A model egy [model provider request](#model-provider-request) során állítja elő.

*Usage:*

"It said it ran the tests but the file timestamps haven't changed."

"Look at the transcript — did it actually emit a tool call, or just describe running them? The model produces the call, but if the harness didn't execute it, nothing happened."

### Tool result

Amit a [harness](#harness) visszaküld egy [tool call](#tool-call) végrehajtása után: fájltartalom, command output, error. Ez az [agent](#agent) egyetlen ablaka az [environment](#environment) felé. A *következő* [model provider request](#model-provider-request) során jut vissza a [model](#model)-hez, ahol a model eldönti, mit kezd vele. A tool call és a tool result ugyanannak az exchange-nek a két vége, mindkettő egy [turn](#turn)-ön belül.

*Usage:*

"It's reasoning about the file like it's empty."

"The tool result came back as a permission denial, not the contents. The model only saw the error string — it has no other window onto the file."

### Permission request

Amit a [harness](#harness) megmutat a felhasználónak, mielőtt végrehajtana egy előzetesen nem jóváhagyott [tool call](#tool-call)-t. A [model](#model) létrehoz egy tool callt; ahelyett, hogy a harness azonnal futtatná, megáll és kérdez. Jóváhagyás esetén fut; elutasítás esetén a harness az elutasítást [tool result](#tool-result)-ként jelenti vissza a modelnek. Ez a mechanizmus teszi az embert a [loop](#human-in-the-loop)-ba kockázatos vagy érzékeny actionöknél.

*Usage:*

"It's been blocked on a permission request for ten minutes — I was in a meeting."

"That's the cost of human-in-the-loop. Pre-approve the safe [tools](#tool) so the request only fires on the actually-risky calls."

### Permission mode

Az [agent mode](#agent-mode) permission-gating része: mely [tool calls](#tool-call) váltanak ki [permission request](#permission-request)-et, és melyek futnak automatikusan. Ez volt a mode rendszerek eredeti célja, mielőtt a [harnesses](#harness) viselkedési instrukciókat is kezdtek csomagolni.

*Usage:*

"It paused on every grep — totally killed the [AFK](#afk) run."

"Loosen the permission mode for read-only [tools](#tool), keep prompting on writes and shell. Most permission requests on a research [session](#session) are noise."

### Agent mode

Olyan preset, amely futásidőben alakítja, hogyan működik az [agent](#agent): összecsomagol egy [permission mode](#permission-mode)-ot és a [system prompt](#system-prompt)-ba injektált viselkedési instrukciókat. Példák: alap mód, amely kockázatos hívásoknál kérdez; **plan mode**, amely blokkolja a szerkesztéseket és research irányba tereli az agentet; **accept-edits** mód, amely automatikusan jóváhagyja az edit műveleteket; **bypass permissions** mód, köznyelven **YOLO mode**, amely mindent automatikusan jóváhagy. [Session](#session) közben is átállítható.

*Vendor terms:* Claude Code ezt "permission modes"-nak, Codex "approval modes"-nak nevezi — mindkettő korábbi, mint a viselkedési bundling.

*Usage:*

"It keeps editing files when I just want a plan."

"Switch to plan mode — it'll block writes and stay in research."

"What about for the [AFK](#afk) run later?"

"Bypass mode, but only inside the [sandbox](#sandbox)."

### Sandbox

Izolált [environment](#environment), amelyben az [agent](#agent) fut: container, VM, ephemeral [filesystem](#filesystem), vagy restricted-permission shell. Korlátozza az agent actionjeinek blast radiusát: még ha destruktív parancsot futtat vagy rosszindulatú tartalmat fetch-el, a kár bent marad. Ez az a safety substrate, amely praktikussá teszi az [AFK](#afk)-t.

*Usage:*

"I want to let it run [bypass-permissions](#agent-mode) overnight but I'm not ready for that."

"Put it in a sandbox — fresh container, no credentials mounted, no network out. Worst case it nukes its own filesystem and you discard the container."

## Section 4 — Failure modes

### Sycophancy

Magabiztosan egyetértő [model](#model) output. Oka a [training](#training): a modelt olyan válaszok felé alakították, amelyeket az emberek kedveltek, az emberek pedig gyakran jobban kedvelik az egyetértést, mint azt, ha közlik velük, hogy tévednek. Így a model megtanulta, hogy az egyetértés jutalmazott — akkor is, ha maga az egyetértés hibás.

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

"Classic sycophancy — it agreed first because you sounded confident, then caved because you sounded doubtful. The plan's quality didn't change, your tone did. [Clear](#clearing) and re-ask without signalling either way."

### Hallucination

Magabiztosan hibás [model](#model) output. Két típusa van, eltérő okokkal és javításokkal:

- *Factuality hallucination* — kitalált vagy hibás tények a világról: nem létező function, rossz API signature, fake citation. Oka gyakran [parametric knowledge](#parametric-knowledge) hiányosság, különösen a [knowledge cutoff](#knowledge-cutoff) után. Fix: töltsd be a megfelelő [contextual knowledge](#contextual-knowledge)-t.
- *Faithfulness hallucination* — az output eltávolodik a betöltött **contextual knowledge**-től, a felhasználói instrukcióktól vagy a model saját korábbi reasoningjétől. Ez [attention degradation](#attention-degradation) tünete; a [dumb zone](#smart-zone)-ban romlik. Fix: [clear](#clearing) vagy [compact](#compaction).

*Avoid:* "hallucination" mint puszta szinonima arra, hogy "wrong" — ha nem nevezed meg a típust, diagnosztikailag keveset ér.

*Usage:*

"It hallucinated a `parseAsync` method on the schema."

"Factuality or faithfulness?"

"The method exists in the docs I pasted — it just stopped reading them after [turn](#turn) forty."

"Faithfulness then. Compact and reload, don't bother adding more docs."

### Parametric knowledge

Amit a [model](#model) a [training](#training)-ből "tud", és ami a [parameters](#parameters)-ben van tárolva. Training időben rögzül — a model nem látja a saját parameters értékeit, és nem is tudja frissíteni őket. A részletesség a tömörítésben elvész: milliárdnyi tény préselődik fix számú parameterbe, és a ritkábbak elmosódnak. Ez ad fluency-t gyakori témákban, és fabricationt ritkábbakban. A [contextual knowledge](#contextual-knowledge) párja.

*Usage:*

"It writes flawless React but invents methods on our internal SDK."

"React is dense in the parametric knowledge — millions of training examples. Your SDK isn't, so the model fills in plausible-looking shapes. Load the SDK docs into [context](#context)."

### Knowledge cutoff

Az a dátum, amely után a [model](#model)-nek nincs [parametric knowledge](#parametric-knowledge)-e. A cutoff utáni libraries, APIs és események fabrication trapek, hacsak a dokumentációjuk nincs betöltve [contextual knowledge](#contextual-knowledge)-ként. Minden model release saját cutoffal érkezik.

*Usage:*

"It keeps writing the v3 SDK syntax — we're on v5."

"v5 shipped after the knowledge cutoff. Load the v5 changelog as contextual knowledge, otherwise it'll keep fabricating from the older parametric version."

### Contextual knowledge

Tények, amelyeket az [agent](#agent) közvetlenül ki tud olvasni az aktuális [context](#context)-ből: a felhasználó feladata, beolvasott fájlok, [tool results](#tool-result), a [session](#session) indulásakor betöltött [AGENTS.md](#agentsmd) tartalom. A [parametric knowledge](#parametric-knowledge) párja: a parametric a parameters-ből *felidézett* tudás; a contextual a [window](#context-window)-ból *olvasott* tudás. [Hallucinations](#hallucination) sokkal ritkábbak, ha az agent contextual knowledge alapján dolgozik — a válasz ott van előtte, nem egy elmosódott memóriából kell előkaparnia.

*Reach for this term* csak akkor, ha parametric knowledge-dzsel állítod szembe; különben elég azt mondani: **context**.

*Avoid:* "working memory" — a contextual knowledge az, ami *most* a window-ban van; a [memory system](#memory-system) az, ami cross-session tartalmat juttat oda. Más léptékek, ne keverd őket.

*Usage:*

"Why does it nail the API when I paste the docs and fabricate it when I don't?"

"With the docs in, it's contextual knowledge — reading off the page. Without, it's parametric and the rare endpoints blur."

### Attention relationship

Amikor a [model](#model) minden egyes [token](#token)-t prediktál, figyelembe veszi a [context](#context) összes többi tokenjét — némelyiket erősen, másokat alig. Két token közötti párosítás az **attention relationship**. A jelentéssel bíró párok — például "her" és "Sarah", vagy egy `getUser()` hívás és a hozzá tartozó `function getUser` definíció — erősebben hatnak egymásra, mint a nem kapcsolódó elemek. Egy N tokenes context nagyságrendileg N² relationshipet tartalmaz.

*Usage:*

"It keeps confusing the two `user` symbols across the diff — sounds like we're in the [dumb zone](#smart-zone)."

"Yeah, the attention relationship between each call site and its declaration is fighting the other one — same token shape, different bindings. Rename one and the pairings sharpen."

### Attention budget

Minden [token](#token) véges mennyiségű influence-t tud szétosztani a [context](#context) többi része között. Ha erős influence jut [egy relationship](#attention-relationship)-re, kevesebb marad másokra. A budget tokenenként értendő, és nem nő attól, hogy a context hosszabb lesz — ezért hígulnak fel a hosszú [sessions](#session).

*Usage:*

"Why does it keep ignoring the schema I pasted at the top?"

"We're well into the [dumb zone](#smart-zone) — every token's attention budget is fixed, but the context kept growing. The signal on the schema is now competing with thousands of newer tokens."

### Attention degradation

Ahogy egy [session](#session) nő, minden [token](#token) [attention budget](#attention-budget)-je egyre több versengő elem között oszlik meg. Bármelyik [meaningful relationship](#attention-relationship) jelereje csökken; az irreleváns [context](#context) zajként befurakodik. Ugyanaz a [model](#model), ugyanazok a [parameters](#parameters) — csak több szájat kell etetni ugyanabból a tányérból. Ez okozza a smart zone / dumb [zone effect](#smart-zone)-et.

*Usage:*

"It's deep in the dumb zone — inventing generics that aren't in the type file."

"Attention degradation. The type definitions are still in context, but the signal on them is buried under everything we've added since. [Clear](#clearing) and reload."

### Smart zone

Egy [session](#session) elején az [agent](#agent) a "smart zone"-ban van: éles, fókuszált, jól idézi fel a releváns dolgokat. Ahogy a session nő, a "dumb zone" felé sodródik: pontatlanabb, feledékenyebb, több hibát vét — és több **faithfulness [hallucination](#hallucination)** jelenik meg. Ugyanaz a [model](#model), ugyanaz a [harness](#harness) — csak több [context](#context). Ez az [attention degradation](#attention-degradation) érezhető hatása. Ha a session felpuffad, [clear](#clearing) vagy [compact](#compaction); ne próbáld erőből átnyomni.

*Usage:*

"It nailed the first three components and just butchered the fourth."

"You're out of the smart zone — same model, just deep into the dumb zone now. Compact and reload the plan, the next component will land."

## Section 5 — Handoffs

### Clearing

A jelenlegi [session](#session) lezárása és egy friss indítása. A következő üzenet üres sessionnel és üres [context window](#context-window)-val indul. Általában a felhasználó kezdeményezi.

*Usage:*

"It's stuck looping on the failing test."

"Just clear it — start a fresh session with the plan doc and the test file. No point fighting the existing [context](#context)."

### Handoff

[Agent](#agent) [context](#context) átvitele egyik [session](#session)-ből egy másikba, visszaút nélkül. A hordozómechanizmus változhat: írott [handoff artifact](#handoff-artifact), memórián belüli összefoglaló ([compaction](#compaction)) és más megoldások. Különbözik a [clearing](#clearing)-től, ahol nincs transzfer. Okai lehetnek: szerepváltás (planner → implementer), [AFK](#afk) run indítása, párhuzamos sessionökre bontás, vagy hely felszabadítása a [context window](#context-window)-ban.

*Usage:*

"Planning session is getting heavy — should I just keep going?"

"Do a handoff. Write the decisions to a doc, clear, start the implementation in a fresh session reading from it."

### Handoff artifact

Olyan dokumentum, amely [handoff](#handoff) során hordozómechanizmusként működik: az egyik [session](#session) írja, a másik olvassa. Több lehetséges módszer egyike; lásd még **compaction**, [compaction](#compaction).

*Usage:*

"How do I split this between the planning [agent](#agent) and the implementing one?"

"Have the planner write a handoff artifact — file paths, decisions, constraints. The implementer's session opens with a pointer to the artifact and works from it as its brief."

### Spec

Egy [handoff artifact](#handoff-artifact), amely több [session](#session)-ből álló munkát ír le: mit építünk, nem azt, hogy az egyes sessionök hogyan végzik a saját részüket. A munka előrehaladtával változik. [Tickets](#ticket)-ből áll.

*Usage:*

"Should this all be one session?"

"No, write it up as a spec — break it into tickets, run each one in its own session. Trying to do the whole thing in a single [context](#context) will hit the [dumb zone](#smart-zone) before you're halfway."

### Ticket

Egy [handoff artifact](#handoff-artifact), amely egyetlen [session](#session) munkakörét határolja le. Állhat önmagában, vagy egy [spec](#spec) gyermekeként. A tickets blokkolhatják egymást vagy függhetnek testvér ticketektől, így a munka sorrendje nem lineáris tervből, hanem dependency graphból következik.

*Usage:*

"Where do I start on the migration spec?"

"Look at the ticket graph — the schema change blocks the backfill, the backfill blocks the API switch. Pick a leaf and run a session on it."

### Compaction

Egy memórián belüli [handoff](#handoff): az előző [session](#session) historyja összefoglalásra kerül, és ez seedeli az új sessiont. Lossy — részletességet cserélünk headroomra. Indíthatja manuálisan a felhasználó vagy [automatically](#autocompact) a harness.

*Usage:*

"[Context](#context)'s getting heavy and I still have the test pass to do."

"Compact before you start — write what's load-bearing into the summary prompt so the new session keeps the schema decisions and drops the exploration."

### Autocompact

[Compaction](#compaction), amelyet a [harness](#harness) automatikusan indít, amikor a [context window](#context-window) közel megtelik.

*Usage:*

"It doesn't seem to remember what we decided about the schema earlier."

"Autocompact fired between [turns](#turn) — the early decisions got summarised and we must have lost something. Reload the plan doc, or compact manually next time so you control what gets kept."

## Section 6 — Memory és steering

### Memory system

Olyan rendszer, amely megpróbálja az [agent](#agent)-et [stateful](#stateful)-lá tenni [sessions](#session) között. A session során információt persistál az [environment](#environment)-be, majd jövőbeli sessionök elején visszatölti a [context window](#context-window)-ba, így az agent folytonosságot hordoz akkor is, ha a felhasználó [clearing](#clearing)-gel lezárja az előző sessiont.

*Usage:*

"I keep having to re-tell it I'm on Postgres, not MySQL."

"Wire up a memory system — write what it learns to the [filesystem](#filesystem) on the first [turn](#turn), reload it at session start. The [model](#model) itself is [stateless](#stateless); the memory layer fakes continuity."

### AGENTS.md

Egy fájl az [environment](#environment)-ben, amelyet a [harness](#harness) a [session](#session) indulásakor betölt a [context window](#context-window)-ba — ez a projekt állandó briefje az [agent](#agent) számára. Cross-harness konvenció.

*Avoid:* AGENTS.md használata olyan tartalomra, amelyet [progressively disclosed](#progressive-disclosure) módon kellene betölteni. Ami ebben van, annak [token](#token) költsége van minden [turn](#turn) során.

*Usage:*

"Why is every session starting with 4k tokens already burned?"

"Check AGENTS.md — someone pasted the entire style guide in there instead of putting it behind a [skill](#skill)."

### Progressive disclosure

Csak azt a [context](#context)-et betölteni, amelyre az [agent](#agent)-nek éppen szüksége van, a többihez pointerekkel. UI designból kölcsönzött fogalom.

*Usage:*

"Should I dump the entire style guide into [AGENTS.md](#agentsmd)?"

"No — progressive disclosure. Reference the style guide as a [skill](#skill) the agent loads when it actually needs to write a component. AGENTS.md pays the [token](#token) cost every [turn](#turn)."

### Skill

Egységként csomagolt, betanítható capability: instrukciók és resource-ok egy konkrét feladat jó elvégzéséhez, az [environment](#environment)-ben tartva, és csak relevancia esetén betöltve a [context window](#context-window)-ba. A [progressive disclosure](#progressive-disclosure) egysége egy [harness](#harness)-ben.

*Avoid:* "[tool](#tool)" — a tool olyasmi, amit az [agent](#agent) *meghív*; a skill olyasmi, amit *elolvas*.

*Usage:*

"Where should I put the deploy runbook?"

"As a skill — the agent loads it only when the task involves deploys. In [AGENTS.md](#agentsmd) it'd burn [tokens](#token) on every [turn](#turn) for something we use weekly."

### Subagent

Egy [agent](#agent), amelyet egy másik agent indít [tool call](#tool-call)-on keresztül. Saját [session](#session)-ben fut, saját [context window](#context-window)-val, és egyetlen [tool result](#tool-result)-ot jelent vissza. Különbözik a [handoff](#handoff)-től: a parent kifejezetten választ vár; a handoffnak nincs visszaútja. **Nem indíthat további subagenteket** — a fa egy szint mély. A subagentek a [context](#context) izolálására vannak, nem hierarchiák komponálására.

*Usage:*

"The grep results are blowing out my context."

"Spawn a subagent to do the search — it'll burn its own context window on the noise and report back the two file paths you actually need."

## Section 7 — Working patterns

### Human-in-the-loop

Olyan working pattern, amelyben egy vagy több ember a [session](#session) során együtt dolgozik az [agent](#agent)-tel: review-zik, irányt módosít, vagy valós időben kollaborál. Az ember jelen van és aktívan részt vesz, nem csak egyedi actionöket engedélyez.

*Usage:*

"Run this [AFK](#afk) overnight?"

"No, schema migration — keep it human-in-the-loop. I want to see each step and steer if it picks the wrong column to backfill from."

### AFK

Olyan working pattern, amikor a felhasználó elindít egy [session](#session)-t, majd felügyelet nélkül hagyja futni az [agent](#agent)-et. Ez az AI coding throughput-szorzója: több AFK session futhat párhuzamosan, miközben alszol, eszel vagy máson dolgozol. Biztonságosan általában megengedőbb [permission mode](#permission-mode) és [sandboxing](#sandbox) mellett működik.

*Avoid:* "background agent" — ez a gépre fókuszál ("running in the background"), nem az emberi munkamintára ("the user has walked away"). Az AFK lényege az, hogy a felhasználó nem figyeli élőben.

*Usage:*

"I'm running this AFK — three sandboxed agents on the refactor, reviewing the PRs in the morning."

"[Bypass permissions](#agent-mode)?"

"Yeah, read-only [filesystem](#filesystem), no network."

### Automated check

Deterministic verification, amely az [environment](#environment)-ben fut: tests, type checks, lints, build, pre-commit hooks. Pass/fail, nincs judgement. Ez az a jel, amelyből egy [agent](#agent) önállóan tud korrigálni anélkül, hogy mást bevonna. A flaky test hibás check, nem "nem-check"; az automated checks *by design* determinisztikusak.

*Avoid:* "feedback loop" / "backpressure" — mindkettő összemossa a checkeket a [review](#automated-review)-val. *Avoid:* "test" — a tests automated checks, de nem minden automated check test.

*Usage:*

"The agent keeps shipping broken code in the [AFK](#afk) runs."

"What automated checks are wired into the [sandbox](#sandbox)?"

"Just the unit tests."

"Add typecheck and lint — it'll self-correct from those before the PR ever lands."

### Automated review

Egy [agent](#agent) egy másik agent munkáját review-zza, gyakran más [model](#model)-lel vagy [system prompt](#system-prompt)-tal. Nem determinisztikus: judgementet alkot. Bárhol futhat — PR előtt, commit historyn utólag, vagy [subagent](#subagent)-ként session közben. Egy LLM-as-judge CI-ben automated review, nem [automated check](#automated-check); a kategóriát az dönti el, mit *csinál* az assertion, nem az, hol fut.

*Avoid:* "AI review" / "agent review" — túl homályosak, nem különítik el a working agenttől.

*Usage:*

"We're getting too many bad PRs from the [AFK](#afk) runs."

"Add an automated review step before merge — different model, separate system prompt, scoped to security and contract changes."

### Human review

A felhasználó elolvassa az [agent](#agent) által készített kódot, és judgementet alkot róla. A diff vagy a módosított fájlok olvasása számít; az agent *leírásának* olvasása arról, hogy mit csinált, nem — a narration nem maga az artifact.

*Avoid:* "code review" önmagában — kétértelmű, lehet emberi vagy [automated](#automated-review).

*Usage:*

"I human-reviewed the [AFK](#afk) output."

"You read the diff or just the summary?"

"Diff. The summary said it deleted dead code — turned out the function was called from a generated file."

### Vibe coding

Olyan working pattern, amelyben a felhasználó [human review](#human-review) nélkül elfogadja az [agent](#agent) kódját. A diff opak marad — az számít, hogy a program viselkedik-e, nem az, mi van belül. [Automated review](#automated-review) és [automated checks](#automated-check) ettől még futhatnak; a vibe coding ezekről nem állít semmit.

*Avoid:* "vibe coding" mint a "low-quality AI coding" szinonimája — a terminus a review stance-t nevezi meg, nem az eredményül kapott kód minőségét.

*Usage:*

"Did you read what it changed in the auth flow?"

"Vibe coded it — login still works, that's all I checked."

"Read the diff before you push, vibing on auth is how secrets leak into logs."

### Design concept

A közös megértés arról, hogy mit építünk: a felhasználó és az [agent](#agent) között közösen tartott, de bármely konkrét assettől különálló fogalom. Brookes terminusa (*The Design of Design*): a beszélgetés, a [handoff artifacts](#handoff-artifact) és a kód mind olyan assetek, amelyek megpróbálják rögzíteni vagy elérni a design conceptet, de egyik sem *maga* az. A design concept minőségét annak a beszélgetésnek a minőségén érezni, amely létrehozta.

*Usage:*

"It's writing exactly what I asked for and it's still wrong."

"You don't share a design concept yet — it's filling gaps with assumptions. Keep talking until cancellation, refunds, and partial fulfilment all line up between you before you let it write a [spec](#spec)."

### Grilling

Technika egy [design concept](#design-concept) kialakítására egy [agent](#agent)-tel: az agent szokratikus módon interjúztatja a felhasználót, döntésről döntésre, és minden döntéshez ajánlott választ javasol. Lassítja a kész terv felé rohanást — addig nem készül [handoff artifact](#handoff-artifact), amíg a concept nem stabilizálódik.

*Usage:*

"It went straight to writing the [spec](#spec) and got the cancellation logic wrong."

"Grill it first — make it ask you about partial cancels, refunds, and timing before it commits anything to the doc. Cheaper to resolve in conversation than in code."

