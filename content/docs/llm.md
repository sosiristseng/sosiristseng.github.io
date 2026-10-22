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
- [llmspeed](https://llmspeed.dev/) : Feel how fast a local LLM runs before you buy the hardware

### Qwen3.8-27B

- [Unsloth](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)
- [ISTA: GSQ-RCO](https://huggingface.co/ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF) : small quants
- [Swift-1.5-Qwen3.8-27b](https://huggingface.co/ukisai/Swift-1.5-Qwen3.8-27B-GGUF) : UkisAI's reasoning-efficient derivative of Qwen3.8-27B.
- [MiaAI-Lab](https://github.com/MiaAI-Lab/Qwen3.8-27B-16gb-NVIDIA-GPUs-one-click-install) for one 16-24 GB GPU.
- [ninfer-4090](https://github.com/sergiuszm/ninfer-4090) : Qwen3.8-27B on one RTX 4090.
- [ninfer](https://github.com/Neroued/ninfer) : C++/CUDA inference engine for explicitly registered Qwen checkpoints on a single NVIDIA GeForce RTX 5090.

### Qwen3.8-Flash-Next

- [Unsloth](https://huggingface.co/unsloth/Qwen3.8-Flash-Next-GGUF)
- [MiaAI-Lab](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark-TensorFold) on one DGX Spark using TensorFold.
- [Strata](https://github.com/Niko1221/Strata) : run Qwen3.8-Flash-Next from 12GB+ VRAM with smart expert caching.

### GLM-5.3-Flash

- [Project Maya](https://github.com/mw00/project-maya) : run GLM-5.3-Flash (321B MoE) privately on your own GPU(s).

### Deepseek 4.1 flash

- [Project Maya](https://github.com/mw00/project-maya) : run Deepseek 4.1 flash privately on your own GPU(s).

### Gemma4

- [Gemma4-31B-QAT](https://huggingface.co/unsloth/gemma-4-31B-it-qat-GGUF)
- [Gemma4-26B-A4B-QAT](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)

### Speech recognition and text-to-speech

- [VoxCPM](https://github.com/OpenBMB/VoxCPM)

### Document processing

- [docling](https://github.com/docling-project/docling)

### Biology

- [evo2](https://github.com/ArcInstitute/evo2)

## Inference engine and front ends

- [exllamav3](https://github.com/turboderp-org/exllamav3) : ExLlamaV3 is an inference library for the EXL3 quantization format (smaller bit per weight).
- [FreeToken](https://github.com/FlashML-org/FreeToken) : Optimized for MoE models.
- [Lemonade](https://lemonade-server.ai/) for AMD GPUs.
- [Lucebox](https://github.com/Luce-Org/lucebox)
- [Project Maya](https://github.com/mw00/project-maya) : run GLM-5.3-Flash (321B MoE) and DS4.1f privately on your own GPU(s).
- [TensorFold](https://github.com/ashhart/TensorFold) : LLM Inference Engine for Metal and CUDA.
- [Unsloth desktop](https://unsloth.ai/docs/desktop)
- [open-webui](https://github.com/open-webui/open-webui) : User-friendly AI Interface supporting multiple backends.

### llama.cpp

- [llama.cpp](https://github.com/ggml-org/llama.cpp) GitHub repo.
- [beellama.cpp](https://github.com/Anbeeld/beellama.cpp) : `llama.cpp` fork supporting KVarN KV cache format.
- [ik_llama.cpp](https://github.com/ikawrakow/ik_llama.cpp) : `llama.cpp` fork with new quants and improved performance for MoE models.

### vLLM

- [vllm](https://github.com/vllm-project/vllm) GitHub repo.
- [Intel vllm](https://hub.docker.com/r/intel/vllm) vLLM  docker image for Intel GPUs.
- [spark-vllm-docker](https://github.com/eugr/spark-vllm-docker) : vLLM docker image for DGX sparks.

### SGLang

- [SGLang](https://github.com/sgl-project/sglang) GitHub repo.
- [SGLang Cookbook](https://docs.sglang.io/cookbook/intro)

## Agents and harnesses

- [Codewhale](https://codewhale.net/)
- [Hermes agent](https://hermes-agent.nousresearch.com/)
- [Minimax code](https://agent.minimaxi.com/docs/code/welcome)
- [OpenCode](https://opencode.ai/)
- [pi coding agent](https://pi.dev/)

### DeepSeek

- [Deepseek harness (DSH)](https://www.deepseek.com/harness/)
  - [Deepseek plugins](https://deepseekplugin.com/)
- [Deepseek reasonix](https://reasonix.io/) : cache-friendly harness for DeepSeek.

### MCP servers

> Model Context Protocol (MCP)

- [DuckDuckGo](https://github.com/nickclyde/duckduckgo-mcp-server)
- [Julia](https://github.com/aplavin/julia-mcp) : MCP server for persistent Julia sessions
- [Kaimon.jl](https://github.com/kahliburke/Kaimon.jl) : MCP server giving AI agents full access to Julia's runtime via a live Gate.
