Ami egy [model](./Model.md)-t kiszolgál [inference](./Inference.md)-hez. Általában távoli service — Anthropic, OpenAI, Google —, de lehet lokális is: Ollama, LM Studio, llama.cpp a saját gépeden. A [harness](./Harness.md) nem maga futtatja a modelt; megkér egy providert.

*Usage:*

"Can we run this offline for the air-gapped client?"

"Swap the model provider to a local one — Ollama or llama.cpp on their box. The harness doesn't care, it just hits a different endpoint."
