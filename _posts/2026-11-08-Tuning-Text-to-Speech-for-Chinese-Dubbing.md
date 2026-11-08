---
layout: single
title: "Tuning Text-to-Speech for Chinese Dubbing"
excerpt: "What it took to make synthetic Chinese voices fit English videos: a timing budget, per-line fitting, voice matching, per-voice speed calibration, a provider switch, and a separate profile for soothing videos."
tags: [Blog]
date: 2026-11-08
---


# Tuning Text-to-Speech for Chinese Dubbing

Nov 8, 2026

## Introduction

Dubbing an English video into Chinese puts a hard constraint on every line: the Chinese audio has to fit the time slot of the English sentence it replaces. If it is too long it overruns the next line. If it is too short the video falls silent while the speaker's lips are still moving. And it still has to sound like a person talking, not a machine reading a list.

This post covers the text-to-speech (TTS) part of a small dubbing tool, and the adjustments that took it from "technically aligned" to "pleasant to listen to". Most of them turned out to be settings and prompt changes, not new architecture.

| Problem | What fixed it | Where |
| --- | --- | --- |
| Long silences after each line | A character budget matched to the voice's real speed, and a prompt that aims for 90–100% of it | Config and translation prompt |
| Lines that run long | Pad, speed up a little, borrow the next gap, or rewrite shorter | Alignment rules |
| A male voice for a female creator | A model listens to the original speaker and picks a voice | Voice matching |
| Daily request limits | Switching to a provider limited per minute, not per day | Provider setting |
| Some voices much slower than others | Measuring each voice once and setting its speed | Per-voice calibration |
| A calm video dubbed like a news report | A slower, softer profile for that one video | Per-video config |

The guiding rule: fix timing in the text before touching the audio. Changing what is said sounds natural; stretching how it is said does not.

## 1. The timing budget

Each line is translated with a limit: the slot length times a target speech rate in Chinese characters per second. The first test clip, a 100-second NASA explainer, had translations written for 4.5 characters per second. The TTS voice actually read at about 5.3. The result was audible: on average each dub filled only 74% of its slot, and one line filled 56%, leaving more than five seconds of silence.

Two changes closed most of the gap.

1. **Match the budget to the voice.** Raising the target from 4.5 to 5.2 characters per second lifted the average fill only to 77%. Long lines got longer, but the model still wrote everything else short.
2. **Change what the prompt asks for.** The prompt had said to aim for 75–100% of the limit and to prefer a looser, shorter translation over an overlong one. It now aims for 90–100%, and when the English carries little information it asks for a fuller spoken sentence: an explicit subject, connecting words. It still must not add facts. Title cards and credits may stay short.

Average fill rose to 83%. The worst line went from 56% to 81%, and several reached 93–98%. Lines that now come out too long are caught by the next step.

The lesson: a number in a config file did little on its own. The model followed the wording of the instruction more than the limit attached to it.

## 2. Fitting each line into its slot

After synthesis, every line goes through the same decision, in this order:

1. **Pad.** If the dub is shorter than the slot, add silence after it.
2. **Speed up.** If it is longer, speed it up with ffmpeg's `atempo`, at most 1.25×.
3. **Borrow.** If that is still not enough, let it run into the pause before the next line, keeping 0.1 s clear.
4. **Rewrite.** If it still does not fit, a small language model rewrites the Chinese to a computed character count, and the line is synthesized again, up to twice.

Speedups are usually small. On a 10.5-minute vlog by a fast talker (about 3.0 English words per second, against 2.6 in the NASA clip), 42 of 125 lines were sped up, by 1.077× on average. Only four went above 1.2×, all of them very short lines of 0.8–1.5 s.

An option reverses steps 2 and 3, borrowing the gap first and speeding up only if needed. Simulated on the same video, it cut sped-up lines from 42 to 26. The cost is that a line can run slightly into the pause before the next one; the next line still starts on time. Because it changes only the alignment, trying it costs nothing in API calls.

## 3. Choosing a voice

A fixed default voice gave the vlog a calm male narrator for a casual young female creator. The fix uses a model that can listen. It hears 30 seconds of the original speaker, taken from the vocals after the music is separated out, and picks a voice from the provider's catalog. Each catalog entry carries the provider's own description, such as gender, age and character.

The choices so far have matched the material:

| Video | What the model heard | Voice picked |
| --- | --- | --- |
| Lifestyle vlog | Female, clear, casual and friendly | A casual female voice |
| Football tactics explainer | Male, steady, magnetic commentator | A middle-aged male announcer |
| Cozy monologue | Female, soft, breathy, introspective | A soft, warm young female voice |
| History explainer | Male, clear, documentary narration | A clear young male narrator |

Each choice is saved in a small file per video, with the model's reasoning, so it can be read and changed by hand. Matching costs about $0.002 per video.

## 4. Switching providers

The first provider, Gemini TTS, sounded good and was cheap. But its paid entry tier allows 100 requests per day per TTS model, and a 10-minute video needs about 125 requests, one per line. A video could not be finished in a day.

Combining several lines into one request would save requests, not money: Gemini bills by the length of the generated audio, at 25 tokens per second. It would also mean cutting the audio back into lines afterwards, which adds a new way to fail.

There was a second problem. When the daily quota ran out, Gemini's newer API did not return an error; the request simply hung. The tool now falls back to the older API after a timeout. That one does report the exhausted quota, and the stage stops in about 20 seconds with a clear message instead of retrying for an hour.

The tool now defaults to MiniMax, whose plans limit requests per minute (10 on the starter plan) with no daily cap. Both providers stay available behind one setting.

| Provider and model | Billed by | TTS cost for a 10.5-minute video |
| --- | --- | --- |
| Gemini, flash TTS | Seconds of audio | About $0.12 (actual) |
| MiniMax, speech-2.8-turbo | Characters | About $0.36 (estimate) |
| MiniMax, speech-2.8-hd | Characters | About $0.59 (estimate) |

One detail matters for estimates: MiniMax counts each Chinese character as two billed characters. With that rule, the estimate for a set of 12 test lines was 986 billed characters, against 990 actually charged.

Switching providers also showed that voice names and styles do not carry over between providers. Each provider therefore keeps its own voice catalog and its own saved voice choices per video.

## 5. Per-voice speed calibration

MiniMax voices differ widely in natural speed. Reading the same sentence at speed 1.0, the 32 Mandarin system voices ranged from 3.79 to 6.51 characters per second. A single character budget cannot suit all of them. With a 5.2 budget, a female news-anchor voice at 4.37 overran its slot on four of six test lines.

MiniMax has its own speed parameter, and native speed control sounds better than stretching audio afterwards. So each voice is measured once, and its speed is set when it is used:

> speed = target rate ÷ (measured rate × 0.9), limited to 0.9–1.2

The factor 0.9 corrects a bias: the calibration sentence reads faster than real dialogue, by a ratio of 0.87–0.93 on the test lines. Calibrating all 32 voices cost $0.26.

| Voice | Rate at speed 1.0 | After calibration | Lines over their slot after calibration |
| --- | --- | --- | --- |
| Female news anchor | 4.37 | 4.97 (speed 1.16) | 1/6 (was 4/6) |
| Male executive | 5.14 | 5.05 (speed 1.04) | 1/6 |

The gap between the two voices fell from 15% to 2%. That is about as precise as it gets, because MiniMax's speed varies by roughly ±5% between generations of the same line; the alignment step absorbs what remains. In the first full video on MiniMax, a naturally slow announcer voice received speed 1.16 automatically and landed at 5.11 characters per second, close to the 5.2 target.

Two limits are worth knowing. The rates are measured per model, so a model change needs a new calibration. And the speed cap of 1.2 cannot rescue the slowest voices: the slowest one only reaches about 4.1 characters per second.

## 6. A different profile for soothing videos

One test video was a slow, cozy monologue close to ASMR. The dub came out bright and brisk. Nothing was broken: every default had been chosen for explainer videos, and several of them worked against this style.

- **The style text was ignored.** Voice matching had written a fitting style note, gentle and introspective, but MiniMax has no natural-language style input, so the voice read in its default tone.
- **Emotion was automatic.** Left to choose, the model leaned cheerful on lines about food and treats.
- **The translations were too full.** Written for 5.2 characters per second, the dub filled a median 98% of each slot, leaving no room to slow down or breathe.
- **The mix was broadcast-loud.** Normalizing the voice to standard loudness removed some of the closeness of the original. This mattered least.

A small style test made the main cause clear. Truly soothing deliveries are slow:

| Version | Speech rate (characters/s) |
| --- | --- |
| Current dub | 4.6–5.2 |
| MiniMax 2.8, calm emotion, softer intensity | 4.2–4.6 |
| MiniMax 2.6, whisper emotion | 3.4–3.6 |
| Gemini voices with an ASMR style prompt | 3.1–3.2 |

At the slowest rates, the existing translations ran 40–60% past their slots. No voice could sound relaxed with that much text to fit.

The chosen fix is a per-video config file that overrides the global one for this video only.

| Setting | Explainer default | Soothing profile |
| --- | --- | --- |
| Translation budget | 5.2 characters/s | 4.3 characters/s |
| Emotion | Automatic | Calm |
| Intensity | 0 | −50 (softer) |
| Speed | Calibrated per voice | 0.9, calibration off |

| Result | Before | After |
| --- | --- | --- |
| Speech rate | 4.90 characters/s | 4.49 characters/s |
| Total Chinese characters | 1091 | 910 |
| Lines sped up | 12 | 3 |
| Median fill of each slot | 98% | 88% |

The trade-off is real. Translations are about 17% shorter, so some lines lost detail, and one line shrank so far that it lost its object and had to be fixed by hand. For this kind of video, slower delivery was worth more than completeness.

## 7. Re-dubbing only what changed

Tuning means many small re-runs, and each TTS request costs money. Every generated line therefore stores a hash of everything that affects its sound: provider, model, voice, speed, volume, pitch, emotion, voice adjustments and the Chinese text. On a re-run, only lines whose hash changed are synthesized again.

A bug showed why the hash alone was not enough. After one line's translation was edited, a re-run skipped TTS entirely, because the stage was marked as done. Now each stage first checks whether its output is out of date, and the log names the lines that changed. Editing one line and re-running costs one request and re-runs only the steps after it.

## 8. What the tuning taught

Most of the gains came from the text, not the audio. Matching the translation budget to the voice, and telling the model to fill it, removed more awkward silence than any audio processing could. When a style still sounded wrong, the cause was again the amount of text. Speed calibration and alignment then only had to handle small differences, which they do inaudibly. The next step is to detect the style automatically: when the voice is chosen, the same listening model could also tell an explainer from a soothing monologue and pick the matching profile.

## References

**Methods**

- Time-stretching audio: [ffmpeg `atempo` filter](https://ffmpeg.org/ffmpeg-filters.html#atempo)
- Loudness normalization: [ffmpeg `loudnorm` filter](https://ffmpeg.org/ffmpeg-filters.html#loudnorm)

**Tools**

- [Gemini API: speech generation](https://ai.google.dev/gemini-api/docs/speech-generation)
- [MiniMax API platform](https://platform.minimax.io/docs)
- [Demucs](https://github.com/facebookresearch/demucs) (separating vocals from music)
