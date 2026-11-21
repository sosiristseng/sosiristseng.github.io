---
title: Qwen 3.8 flash next
tags:
- bookmarks
- ai
---

> Running the [Qwen3.8-Flash-Next](https://huggingface.co/Qwen/Qwen3.8-Flash-Next) model

- [Unsloth Q38FN](https://huggingface.co/unsloth/Qwen3.8-Flash-Next-GGUF)

## On discrete GPU with a large system RAM

- [Basalt](https://github.com/jesdga95/basalt) : Local inference engine for Qwen3.8-Flash-Next on *NVIDIA Blackwell*.
- [PolyStrata](https://github.com/VecSzn/PolyStrata) : supports various MoE models.
- [Strata](https://github.com/Niko1221/Strata) : runs Qwen3.8-Flash-Next and DeepSeekV4.1-Flash-1017 from 12GB+ VRAM with smart expert caching.

## On one DGX spark

- [MiaAI's recipe](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark-TensorFold)
- [blazux's recipe](https://github.com/blazux/qwen3.8-Flash-DGX)
- [myllmbox's recipe](https://github.com/myllmbox/qwen38-flash-next-recipe)
- [salient data's recipe](https://github.com/salient-data/qwen38-next-dgx-recipe)
- [devopsfortunato's recipe](https://github.com/devopsfortunato/Qwen3.8-Flash-Next-FP4-Local-DGX-Spark)

## Others

- [colab-qwen38-g4](https://github.com/mizorewww/colab-qwen38-g4) : runs Q38FN on a Google Colab G4 GPU (96 GB VRAM).
