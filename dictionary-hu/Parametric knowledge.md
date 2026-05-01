Amit a [model](./Model.md) a [training](./Training.md)-ből "tud", és ami a [parameters](./Parameters.md)-ben van tárolva. Training időben rögzül — a model nem látja a saját parameters értékeit, és nem is tudja frissíteni őket. A részletesség a tömörítésben elvész: milliárdnyi tény préselődik fix számú parameterbe, és a ritkábbak elmosódnak. Ez ad fluency-t gyakori témákban, és fabricationt ritkábbakban. A [contextual knowledge](./Contextual%20knowledge.md) párja.

*Usage:*

"It writes flawless React but invents methods on our internal SDK."

"React is dense in the parametric knowledge — millions of training examples. Your SDK isn't, so the model fills in plausible-looking shapes. Load the SDK docs into [context](./Context.md)."
