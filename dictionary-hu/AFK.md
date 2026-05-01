---
aliases:
  - away from keyboard
  - AFK (away from keyboard)
---
Olyan working pattern, amikor a felhasználó elindít egy [session](./Session.md)-t, majd felügyelet nélkül hagyja futni az [agent](./Agent.md)-et. Ez az AI coding throughput-szorzója: több AFK session futhat párhuzamosan, miközben alszol, eszel vagy máson dolgozol. Biztonságosan általában megengedőbb [permission mode](./Permission%20mode.md) és [sandboxing](./Sandbox.md) mellett működik.

*Avoid:* "background agent" — ez a gépre fókuszál ("running in the background"), nem az emberi munkamintára ("the user has walked away"). Az AFK lényege az, hogy a felhasználó nem figyeli élőben.

*Usage:*

"I'm running this AFK — three sandboxed agents on the refactor, reviewing the PRs in the morning."

"[Bypass permissions](./Agent%20mode.md)?"

"Yeah, read-only [filesystem](./Filesystem.md), no network."
