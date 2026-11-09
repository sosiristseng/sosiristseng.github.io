---
title: LLM engines
tags:
- bookmarks
- ai
---

Inference engines powering LLMs.

## Generic

- [Lucebox](https://github.com/Luce-Org/lucebox) : LLM speculative inference server for heterogeneous hardware & consumer GPUs (esp. AMD GPUs).
- [SGLang](https://github.com/sgl-project/sglang) a high-performance serving framework. See also [SGLang Cookbook](https://docs.sglang.io/cookbook/intro)
- [TensorFold](https://github.com/ashhart/TensorFold) : LLM Inference Engine for *Metal* and *CUDA*.
- [Tensorsharp](https://github.com/zhongkaifu/TensorSharp) : a native .NET LLM inference engine and agent runtime for GGUF models.

### llama.cpp

[llama.cpp](https://github.com/ggml-org/llama.cpp) : LLM inference in C/C++ supporting `GGUF` format.

- [beellama.cpp](https://github.com/Anbeeld/beellama.cpp) : `llama.cpp` fork supporting the [KVarN](https://github.com/huawei-csl/KVarN) KV cache format.
- [ik_llama.cpp](https://github.com/ikawrakow/ik_llama.cpp) : `llama.cpp` fork with new quants and improved performance for MoE models.
- [KoboldCpp](https://github.com/lostruins/koboldcpp) : `llama.cpp` fork with text, image, speech, music, and video generation.

### vLLM

[vllm](https://github.com/vllm-project/vllm) : A high-throughput and memory-efficient inference and serving engine for LLMs.

- [Intel vllm](https://hub.docker.com/r/intel/vllm) a vLLM  docker image for *Intel* GPUs.
- [spark-vllm-docker](https://github.com/eugr/spark-vllm-docker) : a vLLM docker image for *DGX sparks*.
- [vllm-radiance](https://github.com/magiccodingman/vllm-radiance) : A vLLM inference-server image for the *AMD Radeon AI PRO R9700*.

## Mixture of Experts (MoE)

Tiered data access: hot experts on the GPU (VRAM), cold ones in the RAM, even data streaming from the SSD.

- [Basalt](https://github.com/jesdga95/basalt) : Local inference engine for Qwen3.8-Flash-Next on *NVIDIA Blackwell*.
- [FreeToken](https://github.com/FlashML-org/FreeToken) : Local inference engine with Bandwidth-Adaptive Execution.
- [PolyStrata](https://github.com/VecSzn/PolyStrata) : supports various MoE models.
- [Project Maya](https://github.com/mw00/project-maya) : supports GLM-5.3-Flash (321B MoE), DeepSeek-V4.1-Flash-1017 (748B MoE), and MiniMax-M3.1-Flash (428B MoE).
- [Strata](https://github.com/Niko1221/Strata) : runs Qwen3.8-Flash-Next and DeepSeekV4.1-Flash-1017 from 12GB+ VRAM with smart expert caching.

## Specialized

- [TabbyAPI](https://github.com/theroyallab/tabbyAPI/) the official API server for [exllamav3](https://github.com/turboderp-org/exllamav3) backend, an inference library for the EXL3 quantization format (smaller bit per weight).
- [ninfer](https://github.com/Neroued/ninfer), a C++/CUDA inference engine for explicitly registered Qwen checkpoints on a *single NVIDIA GeForce RTX 5090*.
