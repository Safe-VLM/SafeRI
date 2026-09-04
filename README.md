# SafeRI

**Recognition and Intervention for Token-Level Safety Intervention in Large Vision Language Models**

[![Paper](https://img.shields.io/badge/arXiv-2609.03544-b31b1b.svg)](https://arxiv.org/abs/2609.03544)
[![Project Page](https://img.shields.io/badge/Project-Page-2f6f4e.svg)](https://safe-vlm.github.io/SafeRI/)

SafeRI is a recognition-and-intervention framework for intrinsic safety in large vision-language models. It monitors the evolving generation state and activates a safety adapter only when unsafe drift emerges, preserving the frozen backbone policy on already-safe trajectories.

> **Code release:** The core implementation will be released immediately upon acceptance.

## Highlights

- **Streaming risk recognition:** a lightweight recognizer evaluates the current pre-token hidden state during autoregressive generation.
- **On-demand intervention:** a gated LoRA safety adapter is activated only when the recognizer detects emerging risk.
- **Token-level control:** recognition at the current step causally controls intervention for the following decoding step.
- **Safety with limited utility loss:** SafeRI improves aggregate safety across multiple VLM backbones while largely preserving general multimodal capability.

## Method

SafeRI couples two components throughout decoding:

1. **Recognition** estimates whether the current response prefix is approaching an unsafe region.
2. **Intervention** activates a boundary-aligned LoRA module for a renewable window, redirecting the continuation toward a safe response.

When risk subsides, the gate closes and generation returns to the frozen-backbone policy. The intervention module is trained using unsafe prefixes, transition statements, and safe continuations.

## Results

| Backbone | Setting | Safety Avg. ↑ | General Avg. ↑ | Safety Δ |
|---|---|---:|---:|---:|
| Qwen3.5-9B | Base | 86.56 | 67.85 | — |
| Qwen3.5-9B | **SafeRI** | **88.88** | 67.64 | **+2.32** |
| Qwen3.5-4B | Base | 87.57 | 66.32 | — |
| Qwen3.5-4B | **SafeRI** | **88.28** | 64.85 | **+0.71** |
| Qwen3.5-2B | Base | 86.54 | 61.05 | — |
| Qwen3.5-2B | **SafeRI** | **87.70** | **62.21** | **+1.16** |
| Llama3.2-Vision-11B | Base | 83.49 | 59.45 | — |
| Llama3.2-Vision-11B | **SafeRI** | **84.27** | 58.93 | **+0.78** |

Safety Avg. is the arithmetic mean over SPA-VL-test harm, AdvBench, HADES, XSTest, and MSSBench. General Avg. is averaged over MMBench, MM-Vet, and BLINK. Please refer to the paper for full experimental settings, baseline comparisons, and ablations.

## Release Plan

The repository currently hosts the SafeRI project page. The core training and inference code, configuration files, and usage instructions will be published immediately upon acceptance.

## Citation

```bibtex
@misc{ma2026saferi,
  title         = {SafeRI: Recognition and Intervention for Token-Level Safety Intervention in Large Vision Language Models},
  author        = {Caoyuan Ma and Tian Gu and Wenpu Liu and Weichu Xie and Shuai Dong and Yuqi Xu and Ji Zhao and Ziyue Wang and Wenzheng Chang and Taiqiang Wu and Yongfu Zhu and Wenqi Shao and Zheng Wang and Yinqiang Zheng},
  year          = {2026},
  eprint        = {2609.03544},
  archivePrefix = {arXiv},
  primaryClass  = {cs.CV},
  url           = {https://arxiv.org/abs/2609.03544}
}
```

## Links

- [Paper](https://arxiv.org/pdf/2609.03544)
- [arXiv](https://arxiv.org/abs/2609.03544)
- [Project page](https://safe-vlm.github.io/SafeRI/)
