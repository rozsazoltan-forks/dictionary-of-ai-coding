Ugyanaz az input különböző outputot adhat. Ha kétszer futtatsz egy [model](./Model.md)-t azonos [context](./Context.md)-tel, két eltérő választ kaphatsz — néha csak egy szóban, néha teljesen más megközelítésben. Ehhez a kódodnak semmit sem kell változnia.

Ez része annak, ahogyan a modellek szöveget generálnak, és ahogyan a [model providers](./Model%20provider.md) kiszolgálják a [requests](./Model%20provider%20request.md)-eket. Nincs olyan kapcsoló, amellyel teljesen eltüntethető.

Számíts eredményszórásra, amikor egy [agent](./Agent.md) ugyanazon a feladaton dolgozik. Egyik nap élesnek tűnik a model; másik nap úgy, mintha elvesztette volna a fonalat. Ugyanaz a task, más dobás.

Ne narrativizáld túl. Az emberek pattern-matching gépek, és néhány rossz futás könnyen úgy érződik, mintha "the model got worse this week" bizonyítéka lenne. Többnyire csak a distribution.

_Usage:_

"Claude has been awful today. Did they ship a worse version?"

"Probably not — model output is non-deterministic. You're going to have good days and bad days on the same task. Try again tomorrow before you go looking for a cause."
