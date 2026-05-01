Deterministic verification, amely az [environment](./Environment.md)-ben fut: tests, type checks, lints, build, pre-commit hooks. Pass/fail, nincs judgement. Ez az a jel, amelyből egy [agent](./Agent.md) önállóan tud korrigálni anélkül, hogy mást bevonna. A flaky test hibás check, nem "nem-check"; az automated checks *by design* determinisztikusak.

*Avoid:* "feedback loop" / "backpressure" — mindkettő összemossa a checkeket a [review](./Automated%20review.md)-val. *Avoid:* "test" — a tests automated checks, de nem minden automated check test.

*Usage:*

"The agent keeps shipping broken code in the [AFK](./AFK.md) runs."

"What automated checks are wired into the [sandbox](./Sandbox.md)?"

"Just the unit tests."

"Add typecheck and lint — it'll self-correct from those before the PR ever lands."
