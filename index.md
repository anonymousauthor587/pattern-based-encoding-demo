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
{% include icon_link.html text="video" icon=site.icons.video href="https://youtu.be/uXYK9tqPepQ" %} &emsp;
{% include icon_link.html text="code" icon=site.icons.code href="https://github.com/anonymousauthor587/pattern-based-encoding-demo" %} &emsp;
{:.center}

{% include youtube_player.html id="uXYK9tqPepQ" %}

<hr style="border: double 1.35px silver;">
## Content
---
- [Proposed Encoding Scheme](#encoding-scheme)
- [Experiment Results](#experiment)
  - [Recurrence Rate](#recurrence-rate)
  - [Subjective Listening Test](#listening-test)
- [Visualizer](#visualizer)
- [Generated Samples](#generated-samples)

<hr style="border: double 1.35px silver;">

## Proposed Encoding Scheme {#encoding-scheme}
---
<img src="img/01_Encoding.png" style="border: 2px solid grey">
Comparison of encoding methods.
{:.center .larger}
> __Key Ideas__: <br>**Voice Separation** - Separates melodic vs. chord clusters before encoding, ensuring that distinct voices do not merge unnaturally in the token space.
<br>
**Note-Level BPE** - Applies BPE to note attributes (pitch intervals, durations, rests) for more musically meaningful “subword” patterns.  
<br>
**Pattern-Based Tokens** - Introduces special tokens marking chordal or melodic segments, facilitating pitch augmentation and capturing longer patterns.
<br>

<hr style="border: double 1.35px silver;">

## Experiment Results {#experiment}
---
### Recurrence Rate {#recurrence-rate}
<img src="tables/02_Experiment_Results_Recurrence_Rate.png" style="border: 2px solid grey">
A table of **recurrence rate** comparisons.
{:.center .larger}

> __Note__: We quantify how effectively the model reuses or repeats patterns in generated continuations. This “recurrence rate” is derived from analyzing how often the model revisits the same melodic or chordal patterns.
<br>

---

### Subjective Listening Test {#listening-test}
<img src="tables/02_Experiment_Results_Subjective_Listening.png" style="border: 2px solid grey">
A table of **Mean and Standard Deviation** comparisons.
{:.center .larger}

> __Note__: Below are **three** random seed generations for **three models** (total of **nine audio clips**). Each model only receives a start-of-sequence prompt and generates up to N measures. We convert the tokens to MIDI and render the resulting audio.
<br>

<hr style="border: double 1.35px silver;">

## Visualizer {#visualizer}

{% include youtube_player.html id="uXYK9tqPepQ" %}

<hr style="border: double 1.35px silver;">

## Generated Samples {#samples}

> __Note__: Below are **three** random seed generations for **three models** (total of **nine audio clips**). Each model only receives a start-of-sequence prompt and generates up to N measures. We convert the tokens to MIDI and render the resulting audio.

<div class="audio-table" markdown="block">

|  | __Sample#1__{:.center} | __Sample#2__{:.center} | __Sample#3__{:.center} |
| __REMI__ | {% include audio_player.html filename="audio/Listening/REMI/Prompt1_REMI.mp3" %} | {% include audio_player.html filename="audio/Listening/REMI/Prompt2_REMI.mp3" %} | {% include audio_player.html filename="audio/Listening/REMI/Prompt3_REMI.mp3" %} |
| __SimpleBPE*__ | {% include audio_player.html filename="audio/Listening/SimpleBPE3000/Prompt1_SimpleBPE.mp3" %} | {% include audio_player.html filename="audio/Listening/SimpleBPE3000/Prompt2_SimpleBPE.mp3" %} | {% include audio_player.html filename="audio/Listening/SimpleBPE3000/Prompt3_SimpleBPE.mp3" %} |
| __Pattern-Based (Ours)__ | {% include audio_player.html filename="audio/Listening/Pattern-Based_300_100_with_Dropout/Prompt1_PB.mp3" %} | {% include audio_player.html filename="audio/Listening/Pattern-Based_300_100_with_Dropout/Prompt2_PB.mp3" %} | {% include audio_player.html filename="audio/Listening/Pattern-Based_300_100_with_Dropout/Prompt3_PB.mp3" %} |

</div>
<hr style="border: double 1.35px silver;">