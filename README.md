<p align="center">
  <img src="assets/banner.jpg" alt="HelixWorld 1.0 — Sound and vision, born together" width="100%">
</p>

# HelixWorld

**HelixWorld 1.0** is a real-time interactive audio-visual world model from [Noiz AI](https://noiz.ai), with researchers from HKUST, Tsinghua, CMU, and Google DeepMind.

Give it an image and a prompt. Walk forward or turn around — picture and sound update together from the same Transformer. The spatial field (azimuth, distance, reverb) turns with the camera. Audio is not a soundtrack laid on afterwards.

> Weights, inference code, and the technical report ship in the coming weeks. [Open a feature request](https://github.com/NoizAI/HelixWorld/issues/new?template=feature_request.yml) if you want something on the roadmap.

<p align="center">
  <a href="https://github.com/NoizAI/HelixWorld/issues/2"><img src="https://img.shields.io/badge/arXiv-Coming%20Soon-b31b1b.svg?style=flat-square&logo=arxiv&logoColor=white" alt="arXiv"></a>
  <a href="https://github.com/NoizAI/HelixWorld/issues/4"><img src="https://img.shields.io/badge/Hugging%20Face-Coming%20Soon-ffcc4d.svg?style=flat-square&logo=huggingface&logoColor=black" alt="Hugging Face"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-Apache%202.0-green.svg?style=flat-square" alt="License"></a>
</p>

## Highlights

| | HelixWorld 1.0 |
| --- | --- |
| Roaming / camera navigation | Yes |
| Real-time | 24 FPS |
| Continuous generation | > 3 minutes |
| Joint audio-video | 48 kHz stereo, same Transformer |
| Spatial sound field | Follows viewpoint |
| Weights and code | Coming soon |

Genie 3, WorldPlay, LingBot-World and others roam visually. HelixWorld's difference is native audio-video, plus a spatial field that turns with the camera.

## Coming soon

- Weights + inference — [#1](https://github.com/NoizAI/HelixWorld/issues/1)
- Technical report — [#2](https://github.com/NoizAI/HelixWorld/issues/2)
- Interactive demo — [#3](https://github.com/NoizAI/HelixWorld/issues/3)
- Hugging Face checkpoints — [#4](https://github.com/NoizAI/HelixWorld/issues/4)

Training code may follow inference. Dataset is not planned for 1.0. Subscribe to [releases](https://github.com/NoizAI/HelixWorld/releases).

## Method

Four stages. Details, figures, and ablations ship with the report.

```text
spatial AV data  →  joint Transformer + action
                 →  causal rollout (KV cache, self-generated history)
                 →  few-step distillation (trajectory + DMD) for realtime
```

1. **Spatial AV data.** First-person real-world video (on-location sound) plus game-engine captures with known geometry and listener pose. Fake stereo, post-hoc scores, and narration are dropped.
2. **Joint generation + action.** Audio and video keep their own latents, enter one Transformer, and predict the next picture and sound from the current state and the user's action.
3. **Causal rollout.** Bidirectional video models can look ahead; interaction cannot. Converted to a causal generator with KV cache, then trained on its own generated history.
4. **Realtime.** Trajectory distillation + DMD cut denoising to a handful of steps. Action, decode, and AV output run as a pipeline.

## Roadmap

1.0 is real-time audio-video interaction. Next:

| | Tracker |
| --- | --- |
| Multi-agent | [#5](https://github.com/NoizAI/HelixWorld/issues/5) |
| Multi-person presence | [#6](https://github.com/NoizAI/HelixWorld/issues/6) |
| Long-horizon consistency | [#7](https://github.com/NoizAI/HelixWorld/issues/7) |
| Autonomous evolution | [#8](https://github.com/NoizAI/HelixWorld/issues/8) |
| Games / interactive film / education | [#10](https://github.com/NoizAI/HelixWorld/issues/10) |

## Citation

```bibtex
@misc{helixworld2026,
  title        = {HelixWorld: A Real-Time Interactive Audio-Visual World Model},
  author       = {{Noiz AI}},
  year         = {2026},
  howpublished = {\url{https://github.com/NoizAI/HelixWorld}},
  note         = {Weights and code forthcoming}
}
```

## License

Code is [Apache 2.0](LICENSE). The weight license will be published with the checkpoint.

Related work from the team: [AudioX](https://github.com/ZeyueT/AudioX), [AudioX-Turbo](https://github.com/NoizAI/AudioX-Turbo), [YuE](https://github.com/multimodal-art-projection/YuE).
