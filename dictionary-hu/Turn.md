Egy felhasználói üzenet és minden, amit az [agent](./Agent.md) válaszként tesz addig, amíg vissza nem adja a szót a felhasználónak. Egy vagy több [model provider requests](./Model%20provider%20request.md)-et tartalmaz — sokat, ha az agent [tools](./Tool.md)-t hív. Egy tisztázó kérdés lezárja a turnt; a válaszod megnyitja a következőt. A hierarchia: [session](./Session.md) **> Turn > Model provider request**.

*Usage:*

"One turn took two minutes?"

"It made fourteen [tool calls](./Tool%20call.md) inside that turn — each one is a separate model provider request. Latency stacks up before the agent finally yields back to you."
