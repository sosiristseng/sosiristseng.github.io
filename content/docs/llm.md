---
title: LLMs
toc: true
type: docs
tags:
- bookmarks
---

Large language models (LLMs), APIs, agents, and harnesses.

## Models and recipes

- [Hugging face](https://huggingface.co/)
- [Unsloth](https://unsloth.ai/docs)
- [Club 3090](https://github.com/noonghunna/club-3090) : recipes for 3090/4090/5090 owners.

### Qwen3.8-27B

- [Unsloth](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)
- [GSQ-RCO](https://huggingface.co/ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF) : small quants
- [Dirk](https://huggingface.co/peculiar-ragdoll/Dirk-Qwen3.8-27B-GGUF) : concise reasoning with an updated chat template
- [MiaAI-Lab](https://github.com/MiaAI-Lab/Qwen3.8-27B-SGLang-DGX-Spark) on one DGX Spark.
- [MiaAI-Lab](https://github.com/MiaAI-Lab/Qwen3.8-27B-DFlash2-EXL3-5.0bpw) for one 24GB GPU or one DGX Spark.

### Qwen3.8-Flash-Next

- [Unsloth: Qwen3.8-Flash-Next](https://huggingface.co/unsloth/Qwen3.8-Flash-Next-GGUF)
- [qwen38-flash-next-spark](https://github.com/0xBakeer/qwen38-flash-next-spark) on one DGX Spark.

### Deepseek v4 flash

- [MiaAI Lab: DS4f](https://github.com/MiaAI-Lab/DeepSeek-v4-Flash-One-DGX-Spark) on one DGX Spark.
- [Entrpi: DS4f on spark](https://github.com/Entrpi/ds4-on-spark) on one DGX Spark.

### Gemma4

- [Gemma4-31B-QAT](https://huggingface.co/unsloth/gemma-4-31B-it-qat-GGUF)
- [Gemma4-26B-A4B-QAT](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)

### Speech recognition and text-to-speech

- [VoxCPM](https://github.com/OpenBMB/VoxCPM)

### Document processing

- [docling](https://github.com/docling-project/docling)

### Biology

- [evo2](https://github.com/ArcInstitute/evo2)

## Runtime

- [FreeToken](https://github.com/FlashML-org/FreeToken) : Optimized for MoE models.
- [Unsloth desktop](https://unsloth.ai/docs/desktop)
- [Lemonade](https://lemonade-server.ai/) for AMD GPUs.
- [Lucebox](https://github.com/Luce-Org/lucebox)
- [ninfer](https://github.com/Neroued/ninfer) : C++/CUDA inference engine for explicitly registered Qwen checkpoints on a single NVIDIA GeForce RTX 5090.

### llama.cpp

- [llama.cpp GitHub repo](https://github.com/ggml-org/llama.cpp)
- [beellama.cpp](https://github.com/Anbeeld/beellama.cpp) : `llama.cpp` fork supporting KVarN KV cache format.
- [ik_llama.cpp](https://github.com/ikawrakow/ik_llama.cpp) : `llama.cpp` fork with new quants and improved performance for MoE models.

### vLLM

- [vllm GitHub repo](https://github.com/vllm-project/vllm)
- [vllm-radiance](https://hub.docker.com/r/stilldeadcode/vllm-radiance) docker image for 2 R9700's.
- [spark-vllm-docker](https://github.com/eugr/spark-vllm-docker) : vLLM docker images for DGX sparks.

### SGLang

- [SGLang GitHub repo](https://github.com/sgl-project/sglang)
- [SGLang Cookbook](https://docs.sglang.io/cookbook/intro)
- [MiaAI-Lab recipes](https://github.com/MiaAI-Lab?tab=repositories&type=source)

## MCP servers

> Model Context Protocol (MCP)

- [DuckDuckGo](https://github.com/nickclyde/duckduckgo-mcp-server)
- [Julia](https://github.com/aplavin/julia-mcp)

## Agents and harnesses

- [Deepseek harness](https://www.deepseek.com/harness/en/)
- [pi coding agent](https://pi.dev/)
- [Qwen code](https://qwen.ai/qwencode)
- [Codewhale](https://github.com/Hmbown/Codewhale)
