# Charis Viewer translation models

Translation models for the on-device translation of [Charis Viewer](https://github.com/noriaji/charis-viewer) (an unofficial Second Life viewer).
They are **not** used unless a user turns on "translate on this PC" and presses the download button in the viewer. The text that is translated never leaves the PC.

The files are in the [Releases](../../releases) of this repository, not in the source tree.

## What the files are

Each `.ctm` file is a small archive (format `CTM1`, written by the viewer's own tooling) that holds one machine-translation model converted to the
[CTranslate2](https://github.com/OpenNMT/CTranslate2) format (int8) together with its SentencePiece tokenizer files (and, for two models, a small `charis.json` with a target-language token).
**No model was trained or changed here: the weights are the original ones, only converted.** The viewer checks the size and the SHA-256 of every file before it uses it (the values are in `SHA256SUMS.txt` and in the viewer's source), unpacks only the expected file names, and downloads only over HTTPS.

| File | Direction | Original model | License of the original (and of this file) |
|---|---|---|---|
| `en-ja.ctm` | English to Japanese | [staka/fugumt-en-ja](https://huggingface.co/staka/fugumt-en-ja) (FuguMT) | CC BY-SA 4.0 |
| `ja-en.ctm` | Japanese to English | [Helsinki-NLP/opus-mt-ja-en](https://huggingface.co/Helsinki-NLP/opus-mt-ja-en) | Apache-2.0 |
| `en-zh.ctm` | English to Chinese | [Helsinki-NLP/opus-mt-en-zh](https://huggingface.co/Helsinki-NLP/opus-mt-en-zh) | Apache-2.0 |
| `en-es.ctm` | English to Spanish | [Helsinki-NLP/opus-mt-en-es](https://huggingface.co/Helsinki-NLP/opus-mt-en-es) | Apache-2.0 |
| `en-fr.ctm` | English to French | [Helsinki-NLP/opus-mt-en-fr](https://huggingface.co/Helsinki-NLP/opus-mt-en-fr) | Apache-2.0 |
| `en-ru.ctm` | English to Russian | [Helsinki-NLP/opus-mt-en-ru](https://huggingface.co/Helsinki-NLP/opus-mt-en-ru) | Apache-2.0 |
| `en-it.ctm` | English to Italian | [Helsinki-NLP/opus-mt-en-it](https://huggingface.co/Helsinki-NLP/opus-mt-en-it) | Apache-2.0 |
| `en-de.ctm` | English to German | [Helsinki-NLP/opus-mt-en-de](https://huggingface.co/Helsinki-NLP/opus-mt-en-de) | CC BY 4.0 |
| `en-pt.ctm` | English to Portuguese | [Helsinki-NLP/opus-mt-tc-big-en-pt](https://huggingface.co/Helsinki-NLP/opus-mt-tc-big-en-pt) | CC BY 4.0 |
| `m2m.ctm` | Japanese/Korean/English: ja-ko, ko-ja, en-ko, ko-en | [facebook/m2m100_418M](https://huggingface.co/facebook/m2m100_418M) | MIT |

## Licenses and credits

- Every file here is a converted copy of the model named in the table and is distributed under **the license of that model**. `en-ja.ctm` is therefore under **CC BY-SA 4.0** (a share-alike license): if you build on it, you must publish your result under the same license and credit the author. The change made here is only the conversion to the CTranslate2 int8 format.
- The OPUS-MT models are by the Language Technology Research Group at the University of Helsinki and the OPUS-MT project. Please cite: J. Tiedemann and S. Thottingal, "OPUS-MT - Building open translation services for the World", EAMT 2020.
- FuguMT (`fugumt-en-ja`) is by staka (https://huggingface.co/staka). M2M100 is by Facebook AI Research (Meta).
- Translations made with these models are machine translations and can be wrong.

The license texts: [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0), [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/), [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/), [MIT](https://opensource.org/license/mit).

## Motion model (release `motion-1`)

The release [`motion-1`](../../releases/tag/motion-1) holds one file for Charis Viewer's "Motion Between Poses" feature: `mmm_v6_soma_fp32.onnx`, the MotionBricks SOMA motion model from NVIDIA's [NVlabs/motionbricks](https://github.com/NVlabs/motionbricks) (v0.2.0, commit 54fc563).
**It is an unmodified copy of the original.** It is used only when a user presses the download button in the viewer, and it runs on the user's own PC (no pose data is sent anywhere).

- License: **NVIDIA Open Model Agreement**, "Licensed by NVIDIA Corporation under the NVIDIA Open Model Agreement." The full text is in the release (`NVIDIA-Open-Model-Agreement.txt`), copied from the [agreement page](https://www.nvidia.com/en-us/agreements/enterprise-software/nvidia-open-model-agreement/). The origin and the "no changes" statement are in `NOTICE`. A copy of both is also in [`motion-1/`](motion-1) in this repository.
- Size 757,864,273 bytes, SHA-256 `856419dc72aeb14e591eebf4dd0ea05734a2506ddb00bcd39dd6dac2ad60f4fb` (also in `SHA256SUMS.txt`). The viewer checks both before it uses the file.

## Updating

A file is never replaced under the same release: the viewer pins the SHA-256 of each file. A new set of models gets a new release tag (`models-2`, ...), and a new viewer points to it. Older viewers keep working with the older release.
