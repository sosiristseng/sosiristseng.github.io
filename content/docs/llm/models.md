---
title: Models and Engines
tags:
- bookmarks
- ai
---

> How to install an LLM inference engine and host an LLM model

## Find models and recipes

- [Hugging face](https://huggingface.co/)
- [Modelscope](https://www.modelscope.ai)
- [Unsloth](https://unsloth.ai/docs)
- [Club 3090](https://github.com/noonghunna/club-3090) : recipes for 3090/4090/5090 owners.
- [MiaAI-Lab](https://github.com/MiaAI-Lab) : various recipes for popular models.

---

- [Qwen 3.8 27B](qw38-27.md)
- [Qwen 3.8 flash next](qw38fn.md)
- [Inkling 2 mini](Inkling-2-mini.md)

### Deepseek v4.1 Flash

- [sybil's recipe](https://github.com/sybil-solutions/dsv41-flash-offload) : DeepSeek-V4.1-Flash EXL3 on one 24 GB RTX 3090 + DDR4 + NVMe.
- [jayleaton's recipe](https://github.com/jayleaton/deepseek-v41-tensorfold-spark) : DeepSeek-V4.1-Flash on 2x DGX Spark with TensorFold.
- [MiaAI's recipe](https://github.com/MiaAI-Lab/DeepSeek-v4.1-Flash-1017-2x-DGX-Sparks) : DeepSeek-V4.1-Flash-1017 EXL3 on 2x DGX Sparks with TensorFold.

### Gemma4

- [Gemma4-31B-QAT](https://huggingface.co/unsloth/gemma-4-31B-it-qat-GGUF)
- [Gemma4-26B-A4B-QAT](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)

### Speech recognition and text-to-speech (TTS)

- [VoxCPM](https://github.com/OpenBMB/VoxCPM)

### Document processing

- [docling](https://github.com/docling-project/docling)
- [MinerU](https://github.com/opendatalab/mineru)

### Biology

- [evo2](https://github.com/ArcInstitute/evo2)
- [AlphaGenome](https://github.com/google-deepmind/alphagenome)

### Image generation

- [MiniMax-H3-Image](https://huggingface.co/MiniMaxAI/MiniMax-H3-Image)
- [Qwen-Image](https://huggingface.co/Qwen/Qwen-Image)

## Inference engines

- [Hyperflare](https://github.com/NVIDIA/hyperflare-inference) : a local inference server for NVIDIA SM120/SM121 GPUs.
- [Lucebox](https://github.com/Luce-Org/lucebox) : LLM speculative inference server for heterogeneous hardware & consumer GPUs (esp. AMD GPUs).
- [Magnitude](https://github.com/magnitudedev/magnitude) : an open source inference engine that tunes its kernels on your hardware.
- [SGLang](https://github.com/sgl-project/sglang) a high-performance serving framework. See also [SGLang Cookbook](https://docs.sglang.io/cookbook/intro)
- [TensorFold](https://github.com/ashhart/TensorFold) : LLM Inference Engine for *Metal* and *CUDA*.
- [Tensorsharp](https://github.com/zhongkaifu/TensorSharp) : a native .NET LLM inference engine and agent runtime for GGUF models.
- [TabbyAPI](https://github.com/theroyallab/tabbyAPI/) the official API server for [exllamav3](https://github.com/turboderp-org/exllamav3) backend, an inference library for the EXL3 quantization format (smaller bit per weight).
- [FreeToken](https://github.com/FlashML-org/FreeToken) : Local inference engine with Bandwidth-Adaptive Execution.
- [Project Maya](https://github.com/mw00/project-maya) : supports GLM-5.3-Flash (321B MoE), DeepSeek-V4.1-Flash-1017 (748B MoE), and MiniMax-M3.1-Flash (428B MoE).

### llama.cpp

[llama.cpp](https://github.com/ggml-org/llama.cpp) : LLM inference in C/C++ supporting `GGUF` format.

- [beellama.cpp](https://github.com/Anbeeld/beellama.cpp) : `llama.cpp` fork supporting the [KVarN](https://github.com/huawei-csl/KVarN) KV cache format.
- [ik_llama.cpp](https://github.com/ikawrakow/ik_llama.cpp) : `llama.cpp` fork with new quants and improved performance for MoE models.
- [KoboldCpp](https://github.com/lostruins/koboldcpp) : `llama.cpp` fork with text, image, speech, music, and video generation.

---

- [llama-optimize](https://github.com/bigattichouse/llama-optimize) : Find good llama.cpp command-line parameters for a given GGUF model on your machine, automatically, using statistically-designed experiments.

### vLLM

[vllm](https://github.com/vllm-project/vllm) : a high-throughput and memory-efficient inference and serving engine for LLMs.

- [DeepInfer](https://github.com/deepseek-ai/deepinfer) : High-performance, large-scale inference framework for *DeepSeek* models.
- [Intel vllm](https://hub.docker.com/r/intel/vllm) a vLLM  docker image for *Intel* GPUs.
- [Paiton](https://github.com/Eliovp-BV/paiton-vllm-plugin) : optimized for *AMD Radeon AI PRO R9700*.
- [spark-vllm-docker](https://github.com/eugr/spark-vllm-docker) : a vLLM docker image for *DGX sparks*.
- [vllm-radiance](https://github.com/magiccodingman/vllm-radiance) : a vLLM inference-server image for the *AMD Radeon AI PRO R9700*.
