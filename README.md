<h2 align="center">MECAT: A Multi-Experts Constructed Benchmark for Fine-Grained Audio Understanding Tasks</h2>

<p align="center">
<a href="https://arxiv.org/abs/2507.23511"><b>📖 Paper</b></a> | <a href="https://nyd3001.github.io/mecat-demo"><b>🎧 Demo</b></a> | <a href="https://nyd3001.github.io/mecat-demo/leaderboard.html"><b>🏆 Leaderboard</b></a> | <a href="https://huggingface.co/datasets/mispeech/MECAT-Caption"><b>🔊 MECAT-Caption (HF)</b></a> | <a href="https://huggingface.co/datasets/mispeech/MECAT-QA"><b>🔊 MECAT-QA (HF)</b></a>
</p>

<p align="center"><img src="https://cdn.jsdelivr.net/gh/xiaomi-research/mecat@main/src/logo.png" alt="MECAT Logo" width="300"/></p>

## News

- **2026.08.20** — The [MECAT Leaderboard](https://nyd3001.github.io/mecat-demo/leaderboard.html) is now available with comprehensive benchmark results.
- **2026.04.30** — 🎉 MECAT was accepted to [**ICML 2026**](https://openreview.net/forum?id=MgjXTLpmgf), accompanied by the release of an interactive [audio demo](https://nyd3001.github.io/mecat-demo).
- **2026.03.27** — [**ACAVCaps**](https://github.com/xiaomi-research/acavcaps), a companion training set for MECAT, was released alongside its [**ICASSP 2026 paper**](https://ieeexplore.ieee.org/document/11463626).
- **2025.12.17** — MECAT was optimized for the [**Interspeech 2026 Audio Encoder Challenge**](https://dataoceanai.github.io/Interspeech2026-Audio-Encoder-Challenge/).
- **2025.08.02** — The MECAT project was launched.

## Table of Contents
- [News](#news)
- [1. Introduction](#1-introduction)
- [2. Features](#2-features)
- [3. Data Distribution](#3-data-distribution)
- [4. Tasks](#4-tasks)
  - [4.1 Audio-Captioning](#41-audio-captioning)
  - [4.2 Audio-Question-Answering](#42-audio-question-answering)
- [5. Example Data](#5-example-data)
  - [5.1 Audio Captioning Example](#51-audio-captioning-example)
  - [5.2 Audio Question Answering Example](#52-audio-question-answering-example)
- [6. Evaluation Metrics](#6-evaluation-metrics)
- [7. Usage](#7-usage)
  - [7.1 Installation](#71-installation)
  - [7.2 Quick Start with Qwen2-Audio Example](#72-quick-start-with-qwen2-audio-example)
  - [7.3 Command Line Evaluation](#73-command-line-evaluation)
  - [7.4 Direct Data Evaluation](#74-direct-data-evaluation)
- [8. Results](#8-results)
- [9. Acknowledgement](#9-acknowledgement)
- [10. Contributing](#10-contributing)
- [11. Citation](#11-citation)
- [12. License](#12-license)

## 1. Introduction 
MECAT is a comprehensive benchmark constructed on **large-scale data** to evaluate machine understanding of audio content through two core tasks:
- **Audio Captioning**: Generating textual descriptions for given audio
- **Audio Question Answering**: Answering questions about given audio

![image](https://cdn.jsdelivr.net/gh/xiaomi-research/mecat@main/src/framework.png)


## 2. Features 
- **Data Source**：Diverse-scenario coverage via the part of ACAV100M dataset
- **Processing Pipeline**:
  - **MetaInfo**: Source video metadata extraction (titles/descriptions)
  - **Content-Specific**: Content-specific feature extraction using 10-20 dedicated models (speech/music/general audio)
  - **Content-Unrelated**: Non-content audio analysis: quality metrics, loudness measurements, reverberation assessment
- **Understanding & Genration**: LLM-powered comprehension & generation with Chain-of-Thought
- **Quality Control**： Multi-stage verification framework
- **Evluation System**: Multi-perspective assessment with progressive difficulty levels
    
## 3. Data Distribution

<table class="tg"><thead>
  <tr>
    <th class="tg-lboi" rowspan="2">Data Code</th>
    <th class="tg-lboi" rowspan="2"> Description </th>
    <th class="tg-lboi" colspan="2">Audio Caption </th>
    <th class="tg-lboi" colspan="2">Audio Question Answering</th>
  </tr>
  <tr>
    <th class="tg-lboi"># Pairs (Train)</th>
    <th class="tg-lboi"># Pairs (Test)</th>
    <th class="tg-lboi"># Pairs (Train)</th>
    <th class="tg-lboi"># Pairs (Test)</th>
  </tr></thead>
<tbody>
  <tr>
    <td class="tg-lboi">000</td>
    <td class="tg-lboi">silence </td>
    <td class="tg-lboi">173</td>
    <td class="tg-lboi">179</td>
    <td class="tg-lboi">865</td>
    <td class="tg-lboi">895</td>
  </tr>
  <tr>
    <td class="tg-lboi">00A</td>
    <td class="tg-lboi">general sound excluding speech and music</td>
    <td class="tg-lboi">837</td>
    <td class="tg-lboi">848</td>
    <td class="tg-lboi">4185</td>
    <td class="tg-lboi">4240</td>
  </tr>
  <tr>
    <td class="tg-lboi">0M0</td>
    <td class="tg-lboi">music</td>
    <td class="tg-lboi">2593</td>
    <td class="tg-lboi">2593</td>
    <td class="tg-lboi">12965</td>
    <td class="tg-lboi">12965</td>
  </tr>
  <tr>
    <td class="tg-lboi">0MA</td>
    <td class="tg-lboi">music and general sound</td>
    <td class="tg-lboi">206</td>
    <td class="tg-lboi">199</td>
    <td class="tg-lboi">1030</td>
    <td class="tg-lboi">995</td>
  </tr>
  <tr>
    <td class="tg-lboi">S00</td>
    <td class="tg-lboi">speech</td>
    <td class="tg-lboi">7839</td>
    <td class="tg-lboi">7839</td>
    <td class="tg-lboi">39195</td>
    <td class="tg-lboi">39195</td>
  </tr>
  <tr>
    <td class="tg-lboi">S0A</td>
    <td class="tg-lboi">speech and general sound</td>
    <td class="tg-lboi">2424</td>
    <td class="tg-lboi">2439</td>
    <td class="tg-lboi">12120</td>
    <td class="tg-lboi">12195</td>
  </tr>
  <tr>
    <td class="tg-lboi">SM0</td>
    <td class="tg-lboi">speech and music</td>
    <td class="tg-lboi">5312</td>
    <td class="tg-lboi">5312</td>
    <td class="tg-lboi">26560</td>
    <td class="tg-lboi">26560</td>
  </tr>
  <tr>
    <td class="tg-lboi">SMA</td>
    <td class="tg-lboi">speech, music and general sound</td>
    <td class="tg-lboi">668</td>
    <td class="tg-lboi">643</td>
    <td class="tg-lboi">3340</td>
    <td class="tg-lboi">3215</td>
  </tr>
</tbody></table>

## 4. Tasks
### 4.1 Audio-Captioning

<table class="tg"><thead>
  <tr>
    <th class="tg-yla0"><span style="font-weight:bold">Type</span></th>
    <th class="tg-yla0"><span style="font-weight:bold">Subtask</span></th>
    <th class="tg-yla0"><span style="font-weight:bold">Category</span></th>
    <th class="tg-yla0"><span style="font-weight:bold">Level</span></th>
    <th class="tg-yla0"><span style="font-weight:bold">Descrption</span></th>
    <th class="tg-yla0"><span style="font-weight:bold">Evaluated Data Abbreviation</span></th>
    <th class="tg-yla0"><span style="font-weight:bold">Sample</span></th>
  </tr></thead>
<tbody>
  <tr>
    <td class="tg-yla0" rowspan="2"><span style="font-weight:bold">Systemtic</span></td>
    <td class="tg-cly1">Short</td>
    <td class="tg-cly1"></td>
    <td class="tg-cly1">🔵 Specialized</td>
    <td class="tg-cly1">Simplified caption over the whole audio within 15 words</td>
    <td class="tg-cly1">000, 00A, 0M0, 0MA<br>S00, S0A, SM0, SMA</td>
    <td class="tg-cly1">20052</td>
  </tr>
  <tr>
    <td class="tg-cly1">Long</td>
    <td class="tg-cly1"></td>
    <td class="tg-cly1">🔵 Specialized</td>
    <td class="tg-cly1">Caption over the whole audio using 1-2 sentences</td>
    <td class="tg-cly1">000, 00A, 0M0, 0MA<br>S00, S0A, SM0, SMA</td>
    <td class="tg-cly1">20052</td>
  </tr>
  <tr>
    <td class="tg-yla0" rowspan="6"><span style="font-weight:bold">Content-Specific</span></td>
    <td class="tg-cly1" rowspan="2">Speech</td>
    <td class="tg-cly1">Clean</td>
    <td class="tg-cly1">🟢 Basic</td>
    <td class="tg-cly1">Caption over clean speech&nbsp;&nbsp;</td>
    <td class="tg-cly1">S00</td>
    <td class="tg-cly1">7839</td>
  </tr>
  <tr>
    <td class="tg-cly1">Mixed</td>
    <td class="tg-cly1">🔴 Complex</td>
    <td class="tg-cly1">Caption over speech with music/sound interference </td>
    <td class="tg-cly1">0MA, S0A, SM0, SMA</td>
    <td class="tg-cly1">8593</td>
  </tr>
  <tr>
    <td class="tg-cly1" rowspan="2">Music</td>
    <td class="tg-cly1">Clean</td>
    <td class="tg-cly1">🟢 Basic</td>
    <td class="tg-cly1">Caption over clean Music&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</td>
    <td class="tg-cly1">0M0</td>
    <td class="tg-cly1">2593</td>
  </tr>
  <tr>
    <td class="tg-cly1">Mixed</td>
    <td class="tg-cly1">🔴 Complex</td>
    <td class="tg-cly1">Caption over music with speech/sound interference</td>
    <td class="tg-cly1">0MA, S0A, SM0, SMA</td>
    <td class="tg-cly1">8593</td>
  </tr>
  <tr>
    <td class="tg-cly1" rowspan="2">Sound</td>
    <td class="tg-cly1">Clear</td>
    <td class="tg-cly1">🟢 Basic</td>
    <td class="tg-cly1">Caption over general sound excluding speech and music</td>
    <td class="tg-cly1">00A</td>
    <td class="tg-cly1">848</td>
  </tr>
  <tr>
    <td class="tg-cly1">Mixed</td>
    <td class="tg-cly1">🔴 Complex</td>
    <td class="tg-cly1">Caption over sound with speech/music interference</td>
    <td class="tg-cly1">0MA, S0A, SM0, SMA</td>
    <td class="tg-cly1">8593</td>
  </tr>
  <tr>
    <td class="tg-yla0"><span style="font-weight:bold">Content-Unrelated</span></td>
    <td class="tg-cly1">Environment</td>
    <td class="tg-cly1"></td>
    <td class="tg-cly1">🔵 Specialized</td>
    <td class="tg-cly1">Caption over acoustic characteristic and environment</td>
    <td class="tg-cly1">000, 00A, 0M0, 0MA<br>S00, S0A, SM0, SMA</td>
    <td class="tg-cly1">20052</td>
  </tr>
</tbody></table>

### 4.2 Audio-Question-Answering
#### Description
<table class="tg"><thead>
  <tr>
    <th class="tg-yla0"><span style="font-weight:bold">Type</span></th>
    <th class="tg-yla0"><span style="font-weight:bold">Subtask</span></th>
    <th class="tg-yla0"><span style="font-weight:bold">Level</span></th>
    <th class="tg-yla0"><span style="font-weight:bold">Description</span></th>
    <th class="tg-yla0"><span style="font-weight:bold">Data Abbreviation</span></th>
    <th class="tg-yla0"><span style="font-weight:bold">Sample</span></th>
  </tr></thead>
<tbody>
  <tr>
    <td class="tg-yla0"><span style="font-weight:bold">Perception</span></td>
    <td class="tg-cly1">Direct_Perception</td>
    <td class="tg-cly1">🟢🟡</td>
    <td class="tg-cly1">Perceive sound types</td>
    <td class="tg-cly1">000, 00A, 0M0, 0MA, S00, S0A, SM0, SMA</td>
    <td class="tg-cly1">20624</td>
  </tr>
  <tr>
    <td class="tg-yla0" rowspan="2"><span style="font-weight:bold">Analysis</span></td>
    <td class="tg-cly1">Sound_Characteristics</td>
    <td class="tg-cly1">🟢🟡🟠🔴</td>
    <td class="tg-cly1">Analyze sound characteristics</td>
    <td class="tg-cly1">000, 00A, 0M0, 0MA, S00, S0A, SM0, SMA</td>
    <td class="tg-cly1">19767</td>
  </tr>
  <tr>
    <td class="tg-cly1">Quality_Assessment </td>
    <td class="tg-cly1">🟢🟡🟠🔴</td>
    <td class="tg-cly1">Analyze sound quality</td>
    <td class="tg-cly1">000, 00A, 0M0, 0MA, S00, S0A, SM0, SMA</td>
    <td class="tg-cly1">18942</td>
  </tr>
  <tr>
    <td class="tg-yla0" rowspan="3"><span style="font-weight:bold">Reasoning</span></td>
    <td class="tg-cly1">Environment_Reasoning </td>
    <td class="tg-cly1">🟢🟡🟠🔴</td>
    <td class="tg-cly1">Reasoning acoustic environment </td>
    <td class="tg-cly1">000, 00A, 0M0, 0MA, S00, S0A, SM0, SMA</td>
    <td class="tg-cly1">18300</td>
  </tr>
  <tr>
    <td class="tg-cly1">Inference_Judgment</td>
    <td class="tg-cly1">🟢🟡🟠🔴</td>
    <td class="tg-cly1">Cross-modal reasoning </td>
    <td class="tg-cly1">000, 00A, 0M0, 0MA, S00, S0A, SM0, SMA</td>
    <td class="tg-cly1">19756</td>
  </tr>
  <tr>
    <td class="tg-cly1">Application_Context </td>
    <td class="tg-cly1">🟢🟡🟠🔴</td>
    <td class="tg-cly1">Semantic understanding </td>
    <td class="tg-cly1">000, 00A, 0M0, 0MA, S00, S0A, SM0, SMA</td>
    <td class="tg-cly1">2871</td>
  </tr>
</tbody></table>

#### Difficulty Distribution
<table class="tg"><thead>
  <tr>
    <th class="tg-cly1">Difficulty</th>
    <th class="tg-cly1">Symbol</th>
    <th class="tg-cly1">Ratio (%)</th>
    <th class="tg-cly1">Description</th>
  </tr></thead>
<tbody>
  <tr>
    <td class="tg-cly1">Basic</td>
    <td class="tg-cly1"><span style="color:#000">🟢</span></td>
    <td class="tg-cly1">25</td>
    <td class="tg-cly1">Direct descriptive questions</td>
  </tr>
  <tr>
    <td class="tg-cly1">Intermediate</td>
    <td class="tg-cly1"><span style="color:#000">🟡</span></td>
    <td class="tg-cly1">35</td>
    <td class="tg-cly1">Analytical questions&nbsp;&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-cly1">Advanced</td>
    <td class="tg-cly1"><span style="color:#000">🟠</span></td>
    <td class="tg-cly1">25</td>
    <td class="tg-cly1">Inferential questions&nbsp;&nbsp;</td>
  </tr>
  <tr>
    <td class="tg-cly1">Complex</td>
    <td class="tg-cly1"><span style="color:#000">🔴</span></td>
    <td class="tg-cly1">15</td>
    <td class="tg-cly1">Comprehensive judgment questions</td>
  </tr>
</tbody></table>

## 5. Example Data

The following examples are from the SMA (Speech, Music and General Sound) domain. You can listen to the audio and browse more samples across all 8 domains on the [**Demo Page**](https://nyd3001.github.io/mecat-demo).

### 5.1 Audio Captioning Example

Each audio clip has 6 caption types (short, long, speech, music, sound, environment), each with 3 paraphrased variants:

```json
{
  "tFg4IwL09Rk_111_64000000000001_121_64": {
    "short": [
      "Electronic music with water splashing and brief speech amid static interference",
      "Dark electronic instrumental with aquatic sounds and momentary vocal utterance",
      "Water splashing noises under brooding synth music featuring short spoken phrase"
    ],
    "long": [
      "A dark electronic instrumental track with water splashing sounds and a male voice briefly speaking, accompanied by persistent background static and mid-frequency noise artifacts.",
      "Moody electronic composition blending synthesized tones with environmental water sounds and fragmented speech, degraded by audio interference",
      "Sustained static underlies a brief male utterance and aquatic noises within a dramatic electronic musical arrangement"
    ],
    "speech": [
      "Male voice briefly uttering 'We over' with cheerful vocal characteristics",
      "Short spoken phrase 'We over' delivered in an upbeat tone",
      "Fragmentary speech segment showing positive vocal affect"
    ],
    "music": [
      "Dark electronic music featuring synthesizer and guitar elements with moderate tempo",
      "Brooding instrumental track combining synthetic textures and guitar tones",
      "Dramatic electronic composition with industrial-inspired rhythmic patterns"
    ],
    "sound": [
      "Prominent water splashing sounds with intermittent static bursts",
      "Aquatic environment noises dominated by liquid movement",
      "Liquid splashing effects accompanied by electrical interference"
    ],
    "environment": [
      "Low-quality audio environment with background static and mid-range distortion",
      "Noisy recording space exhibiting persistent electrical interference",
      "Degraded acoustic conditions with broadband static artifacts"
    ],
    "domain": "SMA"
  }
}
```

### 5.2 Audio Question Answering Example

Each audio clip has 5 QA pairs spanning different cognitive categories and difficulty levels:

```json
{
  "tFg4IwL09Rk_..._b4dfbcf5": {
    "category": "direct_perception",
    "difficulty": "basic",
    "question": "Is speech present in the audio?",
    "answer": "Yes, a male voice briefly says 'We over'",
    "domain": "SMA"
  }
}
```

## 6. Evaluation Metrics

MECAT supports multiple evaluation metrics for comprehensive assessment:
- **Traditional Metrics**: BLEU
- **FENSE**: Fluency Error-based Sentence-bert Evaluation for audio captioning
- **DATE**: Discriminability based Audio Task Evaluation - DATE is particularly effective for audio captioning and question-answering tasks as it considers both the quality of generated text and the model's discriminative capabilities.


## 7. Usage

### 7.1 Installation

```bash
python3 -m pip install mecat
# Or the development 
# pip install git+https://github.com/xiaomi-research/mecat.git
```

### 7.2 Quick Start with Qwen2-Audio Example

This section provides a complete walkthrough of evaluating audio models using MECAT, using Qwen2-Audio as a practical example. The same approach can be adapted for other audio understanding models.

#### 7.2.1 Preliminary Steps: Environment Setup and Model Loading

```python
import torch
from tqdm import tqdm
from transformers import AutoProcessor, Qwen2AudioForConditionalGeneration

# Device setup
device = "cuda" if torch.cuda.is_available() else "cpu"
print(f"Using device: {device}")

# Load Qwen2-Audio model and processor
model = Qwen2AudioForConditionalGeneration.from_pretrained(
    "Qwen/Qwen2-Audio-7B", 
    trust_remote_code=True,
    device_map="auto"
)
processor = AutoProcessor.from_pretrained(
    "Qwen/Qwen2-Audio-7B", 
    trust_remote_code=True
)
```

#### 7.2.2 Audio Caption Evaluation

##### Step 1: Load MECAT-Caption Dataset
```python
from datasets import load_dataset
data = load_dataset(
    'mispeech/MECAT-Caption', 
    split='test', 
)
print(f"Loaded {len(data)} samples from datasets")
```

##### Step 2: Generate and Evaluate Captions

**Method 1: Single Dictionary Approach (for non-instruction-following models)**

*Generation:*
```python
from mecat import evaluate
# Generate general predictions using a single prompt
predictions = {}

for item in tqdm(data, desc="Generating general captions"):
    key = item['__key__']
    audio = item['flac']['array']
    sampling_rate = item['flac']['sampling_rate']
    # Note: the sampling rate of audio provided by MECAT is 16kHz 
    
    # Create general prompt for caption generation
    prompt = "<|audio_bos|><|AUDIO|><|audio_eos|>Generate the caption in English:"

    # Process inputs
    inputs = processor(
        text=prompt, 
        audio=audio, 
        sampling_rate=sampling_rate,
        return_tensors="pt"
    ).to(device)
    
    # Generate response
    with torch.no_grad():
        generated_ids = model.generate(
            **inputs, 
            max_length=512,
            do_sample=False,
            temperature=0.1
        )
    
    # Decode response
    generated_ids = generated_ids[:, inputs.input_ids.size(1):]
    response = processor.batch_decode(
        generated_ids, 
        skip_special_tokens=True, 
        clean_up_tokenization_spaces=False
    )[0]
    predictions[key] = response.strip()

print(f"Generated {len(predictions)} general captions")

# Save single prediction file
import csv
with open('caption_predictions.csv', 'w', encoding='utf-8') as f:
    writer = csv.writer(f, quoting=csv.QUOTE_ALL)
    for key, value in predictions.items():
        writer.writerow([key, value])
```

*Evaluation:*
```python
# Evaluate general predictions across all subtasks
results = evaluate(
    predicted_data=predictions,
    task='caption', 
    metrics=['fense', 'date']
)

print("\nSingle Dictionary Evaluation Results:")
print(results)
```

**Method 2: Multi-Dictionary Approach (recommended for instruction-following models)**

*Generation:*
```python
# Generate task-specific predictions using different prompts
task_prompts = {
    'long': "<|audio_bos|><|AUDIO|><|audio_eos|>Listen to this audio and describe it in 1-2 sentences:",
    'short': "<|audio_bos|><|AUDIO|><|audio_eos|>Listen to the audio and provide a caption for this audio within 15 words:",
    'speech': "<|audio_bos|><|AUDIO|><|audio_eos|>Listen to the audio and provide a caption describing the speech content in this audio:",
    'music': "<|audio_bos|><|AUDIO|><|audio_eos|>Listen to the audio and provide a caption for the music content in this audio:",
    'sound': "<|audio_bos|><|AUDIO|><|audio_eos|>Listen to the audio and provide a general sound excluding speech and music:",
    'environment': "<|audio_bos|><|AUDIO|><|audio_eos|>Listen to the audio and provide a caption for quality or acoustic environment for this audio:"
}

# Generate predictions for each subtask
subtask_predictions = {}

for subtask, prompt_template in task_prompts.items():
    print(f"\nGenerating {subtask} captions...")
    subtask_predictions[subtask] = {}
    
    for item in tqdm(data, desc=f"Generating {subtask} captions"):
        key = item['__key__']
        audio = item['flac']['array']
        sampling_rate = item['flac']['sampling_rate']
        
        # Process inputs with task-specific prompt
        inputs = processor(
            text=prompt_template, 
            audio=audio, 
            sampling_rate=sampling_rate,
            return_tensors="pt"
        ).to(device)
        
        # Generate response
        with torch.no_grad():
            generated_ids = model.generate(
                **inputs, 
                max_length=512,
                do_sample=False,
                temperature=0.1
            )
        
        # Decode response
        generated_ids = generated_ids[:, inputs.input_ids.size(1):]
        response = processor.batch_decode(
            generated_ids, 
            skip_special_tokens=True, 
            clean_up_tokenization_spaces=False
        )[0]
        subtask_predictions[subtask][key] = response.strip()

# Save separate prediction files for each subtask
for subtask, preds in subtask_predictions.items():
    filename = f'{subtask}_caption.csv'
    with open(filename, 'w', encoding='utf-8') as f:
        writer = csv.writer(f, quoting=csv.QUOTE_ALL)
        for key, value in preds.items():
            writer.writerow([key, value])
    print(f"Saved {len(preds)} {subtask} predictions to {filename}")
```

*Evaluation:*
```python
# Evaluate task-specific predictions for optimal performance
results_multisubtask = evaluate(
    predicted_data=subtask_predictions,
    task='caption', 
    metrics=['fense', 'date']
)

print("\nMulti-Dictionary Evaluation Results:")
print(results_multisubtask)
```

##### Step 3: Expected Results

**Expected Caption Evaluation Output:** This result does not represent the actual performance of Qwen2-Audio-7B
```python
   subtask     num_samples  fense  date
 content_long        20052   47.3 40.5
content_short        20052   45.8 41.0 
  pure_speech         7839   30.9 28.5 
 mixed_speech         8593   31.7 27.1 
   pure_music         2593   42.1 50.7
  mixed_music         8593   28.3 33.1
   pure_sound          848   41.2 46.6 
  mixed_sound         8593   16.2 34.1 
  environment        20052   45.4 47.8
score_caption         <NA>   35.2 39.3    
```

**Note**: 
The formulae of `score_caption`: 

$S_{\rm caption} =  0.4\times({0.8S_{\rm long} + 0.2S_{\rm short}}) + 0.4\times(0.6S_{\rm speech} + 0.3S_{\rm music} + 0.1S_{\rm sound}) + 0.2\times S_{\rm environment}$

where $S_{\rm speech}, S_{\rm music}$ and $S_{\rm sound}$ were the average score of pure data and mixed data, e.g., $S_{\rm speech} = \frac{S_{\rm speech,pure}+S_{\rm speech,mixed}}{2}$


#### 7.2.3 Audio Question Answering Evaluation

##### Step 1: Load MECAT-QA Dataset
```python
# Load MECAT-QA test data 
qa_data = load_dataset(
    'mispeech/MECAT-QA', 
    split='test', 
)
print(f"Loaded {len(qa_data)} QA samples from datasets")
```

##### Step 2: Generate and Evaluate Answers

*Generation:*
```python
# Generate predictions for each question-audio pair
qa_predictions = {}

for item in tqdm(qa_data, desc="Generating answers"):
    key = item['__key__']
    audio = item['flac']['array']
    sampling_rate = item['flac']['sampling_rate']
    question = item['json']['question']
    
    
    # Create prompt for QA
    prompt = f"<|audio_bos|><|AUDIO|><|audio_eos|>{question}"
    
    # Process inputs
    inputs = processor(
        text=prompt, 
        audio=audio, 
        sampling_rate=sampling_rate,
        return_tensors="pt"
    ).to(device)
    
    # Generate response
    with torch.no_grad():
        generated_ids = model.generate(
            **inputs, 
            max_length=512,
            do_sample=False,
            temperature=0.1
        )
    
    # Decode response
    generated_ids = generated_ids[:, inputs.input_ids.size(1):]
    response = processor.batch_decode(
        generated_ids, 
        skip_special_tokens=True, 
        clean_up_tokenization_spaces=False
    )[0]
    
    qa_predictions[key] = response.strip()

print(f"Generated {len(qa_predictions)} answers")

# Output the results to csv files
import csv
with open('qa_predictions.csv', 'w', encoding='utf-8') as f:
    writer = csv.writer(f, quoting=csv.QUOTE_ALL)
    for key, value in qa_predictions.items():
        writer.writerow([key, value])
```

*Evaluation:*
```python
# Evaluate using MECAT metrics
qa_results = evaluate(
    predicted_data=qa_predictions, 
    task='qa', 
    metrics=['fense', 'date']
)

print("\nQA Evaluation Results:")
print(qa_results)
```

##### Step 3: Expected Results

**Expected QA Evaluation Output:** This result does not represent the actual performance of Qwen2-Audio-7B
```python
           subtask     num_samples fense date
    direct_perception        20624 44.0 54.0
sound_characteristics        19767 39.0 53.1 
   quality_assessment        18942 18.0 17.8
environment_reasoning        18300 42.0 35.5 
  inference_judgement        19756 51.0 42.0
  application_context         2871 40.0 49.9
             score_qa        <NA>  39.0 42.1
```

**Note**: 
the final score is the average scores of all six subtasks


### 7.3 Command Line Evaluation

You can also use the command line interface for evaluation:

#### 7.3.1 Single File Evaluation

```shell
# Caption evaluation for different audio types (using single dictionary predictions)
python -m mecat.evaluate --prediction caption_predictions.csv --task caption --subtask long   --metrics fense date
python -m mecat.evaluate --prediction caption_predictions.csv --task caption --subtask short  --metrics fense date
python -m mecat.evaluate --prediction caption_predictions.csv --task caption --subtask music  --metrics fense date
python -m mecat.evaluate --prediction caption_predictions.csv --task caption --subtask speech --metrics fense date
python -m mecat.evaluate --prediction caption_predictions.csv --task caption --subtask sound  --metrics fense date
python -m mecat.evaluate --prediction caption_predictions.csv --task caption --subtask environment --metrics fense date

# Batch evaluation across all subsets (using single dictionary predictions)
python -m mecat.evaluate --prediction caption_predictions.csv --task caption --metrics fense date
```

#### 7.3.2 Multi-File Evaluation (Recommended for Caption Task)

For instruction-following models that can generate task-specific captions, you can provide multiple prediction files at once to get comprehensive evaluation results across all caption subtasks:

```shell
# Evaluate multiple caption prediction files in order: long, short, speech, music, sound, environment
python -m mecat.evaluate --prediction \
    long_caption.csv \
    short_caption.csv \
    speech_caption.csv \
    music_caption.csv \
    sound_caption.csv \
    environment_caption.csv \
    --task caption --metrics fense date

# Evaluate with fewer files (will evaluate only available subtasks with warning)
python -m mecat.evaluate --prediction \
    long_caption.csv \
    short_caption.csv \
    --task caption --metrics fense date
```

**Benefits of Multi-File Evaluation:**
- ✅ **Complete Coverage**: Evaluates all caption subtasks with task-specific predictions
- ✅ **Better Performance**: Each prediction file contains responses optimized for specific caption types
- ✅ **Comprehensive Results**: Provides the full evaluation matrix including overall scores
- ⚠️  **File Order Matters**: Files are mapped to subtasks in order: `long → short → speech → music → sound → environment`


#### 7.3.3 QA Task Evaluation

```shell
# QA evaluation for different question types
python -m mecat.evaluate --prediction qa_predictions.csv --task qa --subtask direct_perception     --metrics fense date
python -m mecat.evaluate --prediction qa_predictions.csv --task qa --subtask sound_characteristics --metrics fense date
python -m mecat.evaluate --prediction qa_predictions.csv --task qa --subtask quality_assessment    --metrics fense date
python -m mecat.evaluate --prediction qa_predictions.csv --task qa --subtask environment_reasoning --metrics fense date
python -m mecat.evaluate --prediction qa_predictions.csv --task qa --subtask inference_judgement   --metrics fense date
python -m mecat.evaluate --prediction qa_predictions.csv --task qa --subtask application_context   --metrics fense date

# Batch evaluation across all subsets (recommended)
python -m mecat.evaluate --prediction qa_predictions.csv --task qa --metrics fense date
```

**Prediction File Format:**
```csv
# csv File
"audio_key_1", "Generated caption or answer text"
"audio_key_2", "Another generated response"
"audio_key_3", "More predictions..."
```

**Important Notes:**
- **Audio Captioning Task**
  - **For instruction-following models** (Recommended): 
    - Generate 6 different prediction files using task-specific prompts (one per sub-task). Requires 6 inference passes.
    - **Prompts example:**
      - **long**: "Listen to this audio and describe it in 1-2 sentences"
      - **short**: "Listen to the audio and provide a caption for this audio within 15 words"
      - **speech**: "Listen to the audio and provide a caption describing the speech content in this audio"
      - **music**: "Listen to the audio and provide a caption for the music content in this audio"
      - **sound**: "Listen to the audio and provide a general sound excluding speech and music"
      - **environment**: "Listen to the audio and provide a caption for quality or acoustic environment for this audio"
  - **For non-instruction-following models**: 
    - Evaluate using a single prediction file (single inference pass).
    - The same predictions will be evaluated across all subtasks.
- **Audio Question Answering Task**: 
  - Evaluate all sub-tasks in a single inference pass using the standard method.
  - Single prediction file is sufficient as questions are task-specific.

#### 7.4 Direct Data Evaluation

If you have complete `predicted_data` and `reference_data`, you can directly use them for evaluation without loading from files or datasets:

**Audio Captioning Task Example:**

```python
from mecat import evaluate

predicted_data = [['silence']]

reference_data = [['Extended silence with severe audio distortion and background noise.', 'Persistent quiet period containing heavy signal interference.', 'Continuous silence disrupted by pronounced technical artifacts.']]

results = evaluate(
    predicted_data=predicted_data, 
    reference_data=reference_data, 
    task='caption',
    metrics='bleu',
)

print(results)
```

**Audio Question Answering Task Example:**

Similarly, for QA tasks, you can also provide `predicted_data` and `reference_data` directly:

```python
from mecat import evaluate

predicted_data = [['A woman speaking expressively and dog barks.']]

reference_data = [['A woman speaking expressively and dog barks.']]

results = evaluate(
    predicted_data=predicted_data, 
    reference_data=reference_data, 
    task='qa',
    metrics='bleu',
    subtask='direct_perception',
)

print(results)
```

This approach is useful when:
- You already have the predictions and references in memory
- You want to evaluate custom data that is not part of the MECAT dataset
- You need to quickly test evaluation metrics on specific examples

**Note**: Both `predicted_data` and `reference_data` should be lists of lists, where each inner list contains the predictions or references for a single sample. For reference data, multiple references per sample are supported (as shown in the caption example above).

**Important**: If you want to obtain results for different tasks (e.g., evaluating multiple caption subtasks or QA subtasks), it is recommended to use the methods described in sections 7.1-7.3, as they automatically select the appropriate keys for different tasks and provide comprehensive evaluation results across all subtasks.

## 8. Results

> **Selected Results:** The tables below present a representative selection of models from the Qwen, Kimi, Inkling, and Gemini families.
>
> For complete results and rankings across all evaluated models, see the [🏆 Full MECAT Leaderboard](https://nyd3001.github.io/mecat-demo/leaderboard.html).

### 8.1 Audio-Captioning Task (DATE %, Selected Models)

<table>
<thead>
<tr><th rowspan="3">Model</th><th colspan="2">Systemic</th><th colspan="6">Content-Specific</th><th rowspan="2">Content<br>Unrelated</th><th rowspan="3">Score</th></tr>
<tr><th colspan="2"></th><th colspan="2">Speech</th><th colspan="2">Music</th><th colspan="2">Sound</th></tr>
<tr><th>Long</th><th>Short</th><th>Pure</th><th>Mixed</th><th>Pure</th><th>Mixed</th><th>Pure</th><th>Mixed</th><th>Env</th></tr>
</thead>
<tbody>
<tr><td>Qwen2.5-Omni-7B</td><td>61.1</td><td>56.5</td><td>39.9</td><td>40.9</td><td>32.1</td><td>30.9</td><td>50.7</td><td>23.8</td><td>17.9</td><td>42.6</td></tr>
<tr><td>Qwen3-Omni-Flash-1201</td><td>65.7</td><td>62.5</td><td>59.2</td><td>59.9</td><td>57.4</td><td>32.5</td><td>55.8</td><td>31.6</td><td>27.1</td><td>52.9</td></tr>
<tr><td>Kimi-Audio-7B</td><td>49.5</td><td>54.2</td><td>30.0</td><td>31.3</td><td>27.7</td><td>16.9</td><td>43.1</td><td>16.2</td><td>7.0</td><td>32.8</td></tr>
<tr><td>Inkling-Small-276B-A12B</td><td>69.3</td><td>67.9</td><td>58.5</td><td>59.7</td><td>54.0</td><td>42.4</td><td>45.2</td><td>28.6</td><td>26.3</td><td><b>54.3</b></td></tr>
<tr><td>Gemini-2.5-Flash</td><td>65.6</td><td>63.9</td><td>57.5</td><td>57.5</td><td>52.9</td><td>41.0</td><td>52.2</td><td>28.3</td><td>22.1</td><td>51.6</td></tr>
<tr><td>Gemini-2.5-Pro</td><td>62.3</td><td>62.4</td><td>56.6</td><td>57.5</td><td>53.6</td><td>38.7</td><td>53.4</td><td>29.9</td><td>24.0</td><td>50.6</td></tr>
<tr><td>Gemini-3-Flash</td><td>63.6</td><td>61.9</td><td>59.4</td><td>60.8</td><td>43.1</td><td>32.9</td><td>51.1</td><td>29.7</td><td>25.7</td><td>51.1</td></tr>
<tr><td>Gemini-3-Pro</td><td>64.9</td><td>65.8</td><td>60.5</td><td>62.4</td><td>49.8</td><td>39.8</td><td>55.1</td><td>29.9</td><td>26.1</td><td>53.1</td></tr>
</tbody>
</table>

### 8.2 Audio-Question-Answering (DATE %, Selected Models)

<table>
<thead>
<tr><th rowspan="2">Model</th><th>Perception</th><th colspan="2">Analysis</th><th colspan="3">Reasoning</th><th rowspan="2">Score</th></tr>
<tr><th>Direct<br>Perception</th><th>Sound<br>Characteristics</th><th>Quality<br>Assessment</th><th>Environment<br>Reasoning</th><th>Inference &amp;<br>Judgment</th><th>Application<br>Context</th></tr>
</thead>
<tbody>
<tr><td>Qwen2.5-Omni-7B</td><td>57.8</td><td>52.9</td><td>39.1</td><td>44.0</td><td>53.2</td><td>50.8</td><td>49.6</td></tr>
<tr><td>Qwen3-Omni-Flash-1201</td><td>48.0</td><td>45.9</td><td>29.5</td><td>45.6</td><td>56.7</td><td>54.8</td><td>46.7</td></tr>
<tr><td>Kimi-Audio-7B</td><td>45.6</td><td>39.2</td><td>18.7</td><td>34.6</td><td>48.9</td><td>41.2</td><td>38.0</td></tr>
<tr><td>Inkling-Small-276B-A12B</td><td>56.4</td><td>49.1</td><td>33.1</td><td>49.6</td><td>58.8</td><td>57.1</td><td>50.7</td></tr>
<tr><td>Gemini-2.5-Flash</td><td>56.3</td><td>55.3</td><td>37.7</td><td>46.8</td><td>58.6</td><td>58.0</td><td>52.1</td></tr>
<tr><td>Gemini-2.5-Pro</td><td>55.5</td><td>54.4</td><td>37.7</td><td>47.6</td><td>57.3</td><td>56.6</td><td>51.5</td></tr>
<tr><td>Gemini-3-Flash</td><td>54.3</td><td>51.1</td><td>34.1</td><td>47.2</td><td>57.2</td><td>57.0</td><td>51.0</td></tr>
<tr><td>Gemini-3-Pro</td><td>55.5</td><td>45.5</td><td>25.8</td><td>44.0</td><td>53.2</td><td>52.0</td><td>46.0</td></tr>
</tbody>
</table>

## 9. Acknowledgement

We have referred to the implementation of FENSE for the evaluation

## 10. Contributing

[Yadong Niu](https://github.com/nyd3001)`*` · [Tianzi Wang](https://github.com/Jzmo)`*` · [Heinrich Dinkel](https://github.com/RicherMans) · [Xingwei Sun](https://github.com/xingws) · [Jiahao Zhou](https://github.com/zhoukezi) · [Gang Li](https://github.com/GrantL10) · [Jiahao Mei](https://github.com/NieeiM) · [Jizhong Liu](https://github.com/frankenliu) · [Xunying Liu](https://scholar.google.com/citations?hl=en&user=5_9jk8AAAAAJ&view_op=list_works&sortby=pubdate) · [Junbo Zhang](https://github.com/jimbozhang) · [Jian Luan](https://github.com/jianluan)

`*`: Equal Contribution

## 11. Citation
```bibtex
@article{mecat2025,
  title={MECAT: A Multi-Experts Constructed Benchmark for Fine-Grained Audio Understanding Tasks},
  author={Niu, Yadong and Wang, Tianzi and Dinkel, Heinrich and Sun, Xingwei and Zhou, Jiahao and Li, Gang and Liu, Jizhong and Liu, Xunying and Zhang, Junbo and Luan, Jian},
  journal={arXiv preprint arXiv:2507.23511},
  year={2025}
}
```

## 12. License

The dataset of the project is from the part of ACAV100M undert the **Creative Commons Attribution License 3.0 (CC BY-3.0) license**.

The code of the project is under **Apache License 2.0 license**.
