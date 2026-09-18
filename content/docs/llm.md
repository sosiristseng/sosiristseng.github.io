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
- [MiaAI-Lab](https://github.com/MiaAI-Lab) : various recipes for popular models.

### Qwen3.8-27B

- [Unsloth](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)
- [ISTA: GSQ-RCO](https://huggingface.co/ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF) : small quants
- [Dirk](https://huggingface.co/peculiar-ragdoll/Dirk-Qwen3.8-27B-GGUF) : concise reasoning with an updated chat template.
- [MiaAI-Lab (SPARK)](https://github.com/MiaAI-Lab/Qwen3.8-27B-SGLang-DGX-Spark) on one DGX Spark.
- [MiaAI-Lab (16GB)](https://github.com/MiaAI-Lab/Qwen3.8-27B-16gb-NVIDIA-GPUs-one-click-install) for one 16-24 GB GPU.
- [Swift-Qwen3.8-27b](https://huggingface.co/ukisai/Swift-Qwen3.8-27b) : UkisAI's reasoning-efficient derivative of Qwen3.8-27B.

### Qwen3.8-Flash-Next

- [Unsloth](https://huggingface.co/unsloth/Qwen3.8-Flash-Next-GGUF)
- [MiaAI-Lab (SPARK)](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark) on one DGX Spark. (NVFP4 quant)

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

- [llama.cpp](https://github.com/ggml-org/llama.cpp) GitHub repo
- [beellama.cpp](https://github.com/Anbeeld/beellama.cpp) : `llama.cpp` fork supporting KVarN KV cache format.
- [ik_llama.cpp](https://github.com/ikawrakow/ik_llama.cpp) : `llama.cpp` fork with new quants and improved performance for MoE models.

### vLLM

- [vllm](https://github.com/vllm-project/vllm) GitHub repo
- [vllm-radiance](https://hub.docker.com/r/stilldeadcode/vllm-radiance) docker image for 2 R9700's.
- [spark-vllm-docker](https://github.com/eugr/spark-vllm-docker) : vLLM docker images for DGX sparks.

### SGLang

- [SGLang](https://github.com/sgl-project/sglang) GitHub repo
- [SGLang Cookbook](https://docs.sglang.io/cookbook/intro)

## MCP servers

> Model Context Protocol (MCP)

- [DuckDuckGo](https://github.com/nickclyde/duckduckgo-mcp-server)
- [Julia](https://github.com/aplavin/julia-mcp)

## Agents and harnesses

- [Codewhale](https://github.com/Hmbown/Codewhale)
- [Deepseek harness (DSH)](https://www.deepseek.com/harness/)
- [deepseek reasonix](https://github.com/esengine/deepseek-reasonix) : cache-friendly
- [Hermes agent](https://hermes-agent.nousresearch.com/)
- [OpenCode](https://opencode.ai/)
- [pi coding agent](https://pi.dev/)
