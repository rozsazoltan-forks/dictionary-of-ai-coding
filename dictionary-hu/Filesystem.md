Fájlok és könyvtárak fája, amelyből az [agent](./Agent.md) olvas, amelybe ír, és amelyben parancsokat futtat — coding agent esetén ez az alapértelmezett [environment](./Environment.md). [AGENTS.md](./AGENTS.md.md), [skills](./Skill.md), source code, build scripts és [tool](./Tool.md) configok mind filesystemben élnek. Amikor egy [harness](./Harness.md) "starts in your project", valójában egy filesystemre irányítja az agentet.

*Usage:*

"Why isn't it picking up my AGENTS.md?"

"It's running against a different filesystem — the [sandbox](./Sandbox.md) mounted the parent dir, not the project root. Repoint the harness."
