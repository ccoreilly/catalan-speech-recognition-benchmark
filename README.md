# Catalan Speech Recognition Benchmark

There are not many speech recognition engines/models for the Catalan language. This benchmark aims to collect and compare the available models and serve as reference for projects willing to include catalan speech recognition.

## Table of contents

- [Test data](#test-data)
- [Metrics](#metrics)
  - [Word error rate](#word-error-rate)
  - [Real-time factor](#real-time-factor)
- [Models / Engines](#models--engines)
  - [Col·lectivaT CMUSphinx v0.4.0](#collectivat-cmusphinx-v040)
  - [deepspeech-català v0.7.0](#deepspeech-català-v070)
  - [vosk-model-small-ca-0.4](#vosk-model-small-ca-04)
  - [Google Speech-To-Text](#google-speech-to-text)
- [Results](#results)

## Test data

Two datasets have been initially used to benchmark the different models:

- The test set of the Common Voice dataset from June 2020 ([ca_579h_2020-06-22](https://commonvoice.mozilla.org/en/datasets))
- The crowdsourced high-quality Catalan speech data set (https://www.openslr.org/69/)

As it is not possible to assure that neither of the test datasets has been used when training the evaluated models, a new dataset is in preparation for future tests.

## Metrics

This benchmark considers three metrics: word error rate, real-time factor and model size.

### Word error rate (WER)

Defined as the ratio of the [Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance) between the reference transcript and the prediction, to the number of words in the reference transcript.

### Real-time factor (RTF)

The ratio of the recognition response time to the audio length. The smaller the ratio, the faster it takes to infer speech. This is not considered for cloud-based recognition engines.

As this metric depends on the hardware the model runs, all tests have been executed sequentially on the same machine, an AWS g4dn.xlarge instance:

- 4 vCPU (2nd Generation Intel Xeon Scalable (Cascade Lake) processors)
- 16 GiB Memory
- NVIDIA T4 Tensor Core GPU (16 GiB GPU Mem)

GPU was used when the model supported it.

### Model size

The uncompressed size of the model as needed by the benchmarking scripts.

## Models / Engines

The following models have been tested, if you publish or know of any other speech recognition model for the Catalan language please open an issue!

### Col·lectivaT CMUSphinx v0.4.0

A CMUSphinx based [model](https://cloud.laklak.eu/s/4o2b5MrHckMYCXo) released by Col·lectivaT in November 2018 with AGPL-3.0 license. The model was trained on the ParlamentParla and TV3Parla datasets. More information can be found in their [website](https://collectivat.cat/asr) or [github repository](https://github.com/collectivat/cmusphinx-models).

### deepspeech-català v0.7.0

A [Mozilla DeepSpeech](https://github.com/mozilla/DeepSpeech) based speech recognition [model](https://github.com/ccoreilly/deepspeech-catala), trained on the Common Voice June dataset, ParlamentParla and FestCat.

### vosk-model-small-ca-0.4

A [Vosk-API](https://alphacephei.com/vosk/) compatible lightweight wideband [model](https://alphacephei.com/vosk/models) for Android and RPi for Catalan by [Alpha Cephei](https://alphacephei.com/en/)

### Google Speech-To-Text

The speech recognition service offered by [Google](https://cloud.google.com/speech-to-text). As google converts numbers
and time to their numerical representation (quite well) but the original test data represents them textually, a semi-automatic post-processing step is done before calculating the WER.

## Results

### Crowdsourced google dataset

| Model/Engine                  | WER    | RTF  | Model size |
| ----------------------------- | ------ | ---- | ---------- |
| Col·lectivaT CMUSphinx v0.4.0 | 45,89% | 0,69 | 106 MB     |
| deepspeech-català v0.7.0      | 21,70% | 0,18 | 233 MB     |
| vosk-model-small-ca-0.4       | 11,47% | 0,04 | 91 MB      |
| Google Speech-To-Text         | 10,97% | N/A  | N/A        |

### Common Voice June 2020 Test dataset

| Model/Engine                  | WER    | RTF  | Model size |
| ----------------------------- | ------ | ---- | ---------- |
| Col·lectivaT CMUSphinx v0.4.0 | TBD    | TBD  | 106 MB     |
| deepspeech-català v0.7.0      | 18,41% | 0,18 | 233 MB     |
| vosk-model-small-ca-0.4       | 11,71% | 0,04 | 91 MB      |
| Google Speech-To-Text         | TBD    | N/A  | N/A        |
