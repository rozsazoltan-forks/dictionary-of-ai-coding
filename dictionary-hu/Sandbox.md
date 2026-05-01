---
aliases:
  - Sandboxing
  - Sandbox / Sandboxing
---
Izolált [environment](./Environment.md), amelyben az [agent](./Agent.md) fut: container, VM, ephemeral [filesystem](./Filesystem.md), vagy restricted-permission shell. Korlátozza az agent actionjeinek blast radiusát: még ha destruktív parancsot futtat vagy rosszindulatú tartalmat fetch-el, a kár bent marad. Ez az a safety substrate, amely praktikussá teszi az [AFK](./AFK.md)-t.

*Usage:*

"I want to let it run [bypass-permissions](./Agent%20mode.md) overnight but I'm not ready for that."

"Put it in a sandbox — fresh container, no credentials mounted, no network out. Worst case it nukes its own filesystem and you discard the container."
