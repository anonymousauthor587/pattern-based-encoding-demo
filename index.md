---
layout: page
title: "Pattern-Based Encoding for Symbolic Music Generation"
---

<style>
.audio-table {
    display: block;
    overflow-x: auto;
    white-space: nowrap;
}

.audio-table table {
    width: auto;
    min-width: 150px; /* Adjust based on your needs */
}

.audio-table td, .audio-table th {
    min-width: 200px; /* Adjust based on the size of your audio players */
    border: 1px solid #ccc;
    text-align: center;
    padding: 8px;
}

.audio-table audio {
    width: 100%; /* Make audio player responsive within the cell */
    min-width: 250px; /* Adjust based on your needs */
}
</style>

[Anonymous Authors](#) &emsp;
[Anonymous Affiliations](#) &emsp;
<br>
anonymous@ismir.net
{:.center}

{% include icon_link.html text="paper" icon=site.icons.paper href="#" %} &emsp;
{% include icon_link.html text="video" icon=site.icons.video href="#" %} &emsp;
{% include icon_link.html text="code" icon=site.icons.code href="#" %} &emsp;
{:.center}

<hr style="border: double 1.35px silver;">

## 1. Proposed Encoding Scheme
---
> **Summary**: We propose a pattern-based encoding method for symbolic music generation. By integrating **voice separation** and **note-level Byte-Pair Encoding (BPE)**, we capture both melodic and harmonic patterns in polyphonic pieces. This approach yields more interpretable tokens and reduces sequence length compared to traditional event-based representations.

<img src="img/01_Encoding.png" style="border: 2px solid grey">
{:.center .larger}

**Key Ideas**  
- **Voice Separation**: Separates melodic vs. chord clusters before encoding, ensuring that distinct voices do not merge unnaturally in the token space.  
- **Note-Level BPE**: Applies BPE to note attributes (pitch intervals, durations, rests) for more musically meaningful “subword” patterns.  
- **Pattern-Based Tokens**: Introduces special tokens marking chordal or melodic segments, facilitating pitch augmentation and capturing longer patterns.

<hr style="border: double 1.35px silver;">

## 2. Experiment Results
---

### 2.1 Recurrence Rate
> We quantify how effectively the model reuses or repeats patterns in generated continuations. This “recurrence rate” is derived from analyzing how often the model revisits the same melodic or chordal patterns.

<img src="tables/02_Experiment_Results_Recurrence_Rate.png" style="border: 2px solid grey">
{:.center .larger}

An example table of **recurrence rate** comparisons (averaged across several test prompts) might look like this:

| Model                   | Melody Recurrence | Chord Recurrence |
|-------------------------|:-----------------:|:----------------:|
| **REMI**                | 0.129 ± 0.166     | 0.291 ± 0.259    |
| **SimpleBPE**           | 0.127 ± 0.193     | 0.251 ± 0.243    |
| **Pattern-Based (Ours)**| 0.184 ± 0.193     | 0.384 ± 0.297    |

> **Observation**: Models using Pattern-Based Encoding generally show **higher pattern recurrence**, indicating better thematic consistency in generated pieces.

<br>

### 2.2 Subjective Listening Test
> In addition to objective metrics, we conducted a listening test where participants rated each generation on overall musical quality and consistency.

<img src="tables/02_Experiment_Results_Subjective_Listening.png" style="border: 2px solid grey">
{:.center .larger}

**Example Results**: Average preference scores (1–5 scale) from 15 participants:

| Model             | Mean Score | Std Dev  |
|-------------------|:----------:|:--------:|
| **REMI**          | 3.667      | 1.111    |
| **SimpleBPE**     | 2.667      | 1.110    |
| **Pattern-Based** | 4.333      | 1.109    |

> **Observation**: Participants showed a clear preference for **Pattern-Based Encodings**, particularly noting their structured and coherent melodic/harmonic development.

<hr style="border: double 1.35px silver;">

## 3. Visualizer
---
> We developed a visual interface to **display separated voices and BPE-segmented patterns**. The `.mov` file below demonstrates how **chord clusters** and **melodic clusters** are annotated in real time.

<video width="720" controls>
  <source src="video/Visualizer_Demo.mov" type="video/quicktime">
</video>

> **Note**: This demo highlights how the resulting JSON data from our pipeline is rendered as a musical score (MEI/SVG) and accompanied by synchronized audio playback.

<hr style="border: double 1.35px silver;">

## 4. Generated Samples
---
> Below are **three** random seed generations for **three models** (total of **nine audio clips**). Each model only receives a start-of-sequence prompt and generates up to N measures. We convert the tokens to MIDI and render the resulting audio.

<div class="audio-table" markdown="block">

|                        | **Sample #1**                                    | **Sample #2**                                    | **Sample #3**                                    |
|------------------------|:------------------------------------------------:|:------------------------------------------------:|:------------------------------------------------:|
| **REMI**               | {% include audio_player.html filename="audio/Listening/REMI/Prompt3_REMI.mp3" %}        | {% include audio_player.html filename="audio/Listening/REMI/Prompt2_REMI.mp3" %}        | {% include audio_player.html filename="audio/Listening/REMI/Prompt2_REMI.mp3" %}        |
| **SimpleBPE**          | {% include audio_player.html filename="audio/Listening/SimpleBPE3000/Prompt1_SimpleBPE.mp3" %}   | {% include audio_player.html filename="audio/Listening/SimpleBPE3000/Prompt2_SimpleBPE.mp3" %}   | {% include audio_player.html filename="audio/Listening/SimpleBPE3000/Prompt3_SimpleBPE.mp3" %}   |
| **Pattern-Based (Ours)** | {% include audio_player.html filename="audio/Listening/Pattern-Based_300_100_with_Dropout/Prompt1_PB.mp3" %} | {% include audio_player.html filename="audio/Listening/Pattern-Based_300_100_with_Dropout/Prompt2_PB.mp3" %} | {% include audio_player.html filename="audio/Listening/Pattern-Based_300_100_with_Dropout/Prompt3_PB.mp3" %} |

</div>

> **Observations**:  
> - **REMI** can sometimes generate longer sequences but may produce repetitive events.  
> - **SimpleBPE** effectively shortens sequences but may suffer from unintuitive token merges.  
> - **Pattern-Based** tends to preserve meaningful chord/melody interplay, yielding more varied and coherent passages.

<hr style="border: double 1.35px silver;">

