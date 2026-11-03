---
title: LLM models
tags:
- bookmarks
- ai
---

> How to find and host an LLM model on your computer

- [Hugging face](https://huggingface.co/)
- [Modelscope](https://www.modelscope.ai)

## General recipes

- [Club 3090](https://github.com/noonghunna/club-3090) : recipes for 3090/4090/5090 owners.
- [MiaAI-Lab](https://github.com/MiaAI-Lab) : various recipes for popular models.
- [Unsloth](https://unsloth.ai/docs)

## Inference engines

- [exllamav3](https://github.com/turboderp-org/exllamav3) : ExLlamaV3 is an inference library for the EXL3 quantization format (smaller bit per weight).
- [Project Maya](https://github.com/mw00/project-maya) : run GLM-5.3-Flash (321B MoE), DeepSeek-V4.1-Flash-1017 (748B MoE) and MiniMax-M3.1-Flash (428B MoE) privately on your own GPU(s)
- [FreeToken](https://github.com/FlashML-org/FreeToken) : Optimized for MoE models.
- [Strata](https://github.com/Niko1221/Strata) : run Qwen3.8-Flash-Next and DeepSeekV4.1-Flash-1017 from 12GB+ VRAM with smart expert caching.
- [SGLang](https://github.com/sgl-project/sglang) GitHub repo. See also [SGLang Cookbook](https://docs.sglang.io/cookbook/intro)
- [TensorFold](https://github.com/ashhart/TensorFold) : LLM Inference Engine for Metal and CUDA.

### llama.cpp

- [llama.cpp](https://github.com/ggml-org/llama.cpp) GitHub repo.
- [beellama.cpp](https://github.com/Anbeeld/beellama.cpp) : `llama.cpp` fork supporting KVarN KV cache format.
- [ik_llama.cpp](https://github.com/ikawrakow/ik_llama.cpp) : `llama.cpp` fork with new quants and improved performance for MoE models.

### vLLM

- [vllm](https://github.com/vllm-project/vllm) GitHub repo.
- [Intel vllm](https://hub.docker.com/r/intel/vllm) vLLM  docker image for Intel GPUs.
- [spark-vllm-docker](https://github.com/eugr/spark-vllm-docker) : vLLM docker image for DGX sparks.

## Qwen3.8-27B

> Running the [Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) model

- [ISTA: GSQ-RCO](https://huggingface.co/ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF) : small quants of ISTA lab.
- [MiaAI-Lab](https://github.com/MiaAI-Lab/Qwen3.8-27B-16gb-NVIDIA-GPUs-one-click-install) for one 16-24 GB GPU using the EXL3 quantization format.
- [ninfer-4090](https://github.com/sergiuszm/ninfer-4090) : Qwen3.8-27B on one RTX 4090. Based on [ninfer](https://github.com/Neroued/ninfer), a C++/CUDA inference engine for explicitly registered Qwen checkpoints on a single NVIDIA GeForce RTX 5090.
- [Swift-1.5-Qwen3.8-27b](https://huggingface.co/ukisai/Swift-1.5-Qwen3.8-27B-GGUF) : UkisAI's reasoning-efficient derivative of Qwen3.8-27B.
- [Unsloth](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)

## Qwen3.8-Flash-Next

> Running the [Qwen3.8-Flash-Next](https://huggingface.co/Qwen/Qwen3.8-Flash-Next) model

- [Unsloth](https://huggingface.co/unsloth/Qwen3.8-Flash-Next-GGUF)
- [MiaAI-Lab](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark-TensorFold) on one DGX Spark using TensorFold.
- [Strata](https://github.com/Niko1221/Strata) : run Qwen3.8-Flash-Next from 12GB+ VRAM with smart expert caching.

## Gemma4

Use them with `llama.cpp`.

- [Gemma4-31B-QAT](https://huggingface.co/unsloth/gemma-4-31B-it-qat-GGUF)
- [Gemma4-26B-A4B-QAT](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)


## Speech recognition and text-to-speech (TTS)

- [VoxCPM](https://github.com/OpenBMB/VoxCPM)

## Document processing

- [docling](https://github.com/docling-project/docling)
- [MinerU](https://github.com/opendatalab/mineru)

## Biology

- [evo2](https://github.com/ArcInstitute/evo2)
