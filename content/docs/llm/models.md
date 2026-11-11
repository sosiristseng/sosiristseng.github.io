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

## Qwen3.8-27B

> Running the [Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) model

- [HyperQwen](https://github.com/syv-ai/HyperQwen) : Qwen3.8-27B on a single 24 GB card with vLLM.
- [MiaAI-Lab](https://github.com/MiaAI-Lab/Qwen3.8-27B-16gb-NVIDIA-GPUs-one-click-install) for one 16-24 GB GPU using the EXL3 quantization format.
- [ninfer-4090](https://github.com/sergiuszm/ninfer-4090) : Qwen3.8-27B on one RTX 4090. Based on `ninfer`.
- [MiaAI-Lab (DGX Spark)](https://github.com/MiaAI-Lab/Qwen3.8-27B-SGLang-DGX-Spark) on one DGX Spark.

Running with `llama.cpp` or GGUF-compliant engines:

- [ISTA: GSQ-RCO](https://huggingface.co/ISTA-DASLab/Qwen3.8-27B-GSQ-RCO-GGUF) : small quants of ISTA lab.
- [Swift-1.5-Qwen3.8-27b](https://huggingface.co/ukisai/Swift-1.5-Qwen3.8-27B-GGUF) : UkisAI's reasoning-efficient derivative of Qwen3.8-27B.
- [Unsloth Qwen3.8-27b](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)

## Qwen3.8-Flash-Next (Q38FN)

> Running the [Qwen3.8-Flash-Next](https://huggingface.co/Qwen/Qwen3.8-Flash-Next) model

- [Unsloth Q38FN](https://huggingface.co/unsloth/Qwen3.8-Flash-Next-GGUF)
- [MiaAI's recipe](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark-TensorFold) on one DGX Spark with TensorFold.
- [blazux's recipe](https://github.com/blazux/qwen3.8-Flash-DGX) on a single DGX Spark with vLLM.
- [myllmbox's recipe](https://github.com/myllmbox/qwen38-flash-next-recipe) on a single DGX Spark with vLLM.
- [colab-qwen38-g4](https://github.com/mizorewww/colab-qwen38-g4) : runs Q38FN on a Google Colab G4 GPU (96 GB VRAM).

## Deepseek v4.1 Flash

- [sybil's recipe](https://github.com/sybil-solutions/dsv41-flash-offload) : DeepSeek-V4.1-Flash EXL3 on one 24 GB RTX 3090 + DDR4 + NVMe.
- [jayleaton's recipe](https://github.com/jayleaton/deepseek-v41-tensorfold-spark) : DeepSeek-V4.1-Flash on 2x DGX Spark with TensorFold.
- [MiaAI's recipe](https://github.com/MiaAI-Lab/DeepSeek-v4.1-Flash-1017-2x-DGX-Sparks) : DeepSeek-V4.1-Flash-1017 EXL3 on 2x DGX Sparks with TensorFold.

## Gemma4

- [Gemma4-31B-QAT](https://huggingface.co/unsloth/gemma-4-31B-it-qat-GGUF)
- [Gemma4-26B-A4B-QAT](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)

## Speech recognition and text-to-speech (TTS)

- [VoxCPM](https://github.com/OpenBMB/VoxCPM)

## Document processing

- [docling](https://github.com/docling-project/docling)
- [MinerU](https://github.com/opendatalab/mineru)

## Biology

- [evo2](https://github.com/ArcInstitute/evo2)
- [AlphaGenome](https://github.com/google-deepmind/alphagenome)

## Image generation

- [MiniMax-H3-Image](https://huggingface.co/MiniMaxAI/MiniMax-H3-Image)
- [Qwen-Image](https://huggingface.co/Qwen/Qwen-Image)
