---
aliases:
  - plan mode
  - accept-edits
  - bypass permissions
  - YOLO mode
---
Olyan preset, amely futásidőben alakítja, hogyan működik az [agent](./Agent.md): összecsomagol egy [permission mode](./Permission%20mode.md)-ot és a [system prompt](./System%20prompt.md)-ba injektált viselkedési instrukciókat. Példák: alap mód, amely kockázatos hívásoknál kérdez; **plan mode**, amely blokkolja a szerkesztéseket és research irányba tereli az agentet; **accept-edits** mód, amely automatikusan jóváhagyja az edit műveleteket; **bypass permissions** mód, köznyelven **YOLO mode**, amely mindent automatikusan jóváhagy. [Session](./Session.md) közben is átállítható.

*Vendor terms:* Claude Code ezt "permission modes"-nak, Codex "approval modes"-nak nevezi — mindkettő korábbi, mint a viselkedési bundling.

*Usage:*

"It keeps editing files when I just want a plan."

"Switch to plan mode — it'll block writes and stay in research."

"What about for the [AFK](./AFK.md) run later?"

"Bypass mode, but only inside the [sandbox](./Sandbox.md)."
