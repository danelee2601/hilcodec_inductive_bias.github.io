
<div style="text-align: center;">
  <img src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/blob/main/fig/hac_logo.png?raw=true" alt="method" style="width: 30%;">
</div>

# HANCE Audio Codec (HAC) (ver.1, Nov 2024)

A state-of-the-art audio codec model, developed by HANCE, consisting of encoder, quantizer, and decoder. Its design principals are 1) light-weight, 2) high compression rate, and 3) high fidelity.



# Model Specifications

## ver.1.3 (05.12.2024)
- model size: 3.6M parameters (6.9 MB in bfloat16, 13.7 MB in float32)
- kbps (kilobits per sec): 3.6
    - number of tokens/s: 200
- built upon v.1.2
  - main feature of v.1.3 is ligther model size than v.1.2.
  - achieved it by removing a unnecssary convolutional layer in the residual block and adding Global Response Normalization (GRN) layer from the ConvNext-v2 paper.




## Comparison to the Existing Models

| Model | #Params (Million) | kbps |
| ----- | ----- | ----- | 
| EnCodec | 14.9 | {3, 6} |
| DAC | 74.18 | {4, 9} |
| HILCodec | 9.6 | {3, 6} |
| HAC | 3.6 | 3.6 |


<div style="text-align: left;">
  <img src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/blob/main/fig/table_fig.png?raw=true" alt="method" style="width: 70%;">
</div>



# Experiments


## Dataset

The one provided by Peder, I call it Soundly Speech Dataset. It contains 79,997 speech sample pairs (clean speech, noisy speech) with audio length of 11s and sampling rate of 24khz. 
In this experiment, I used 79,838 clean speech samples for training and 159 for validation. 
During training, each audio sample is randmoly cropped into 1s clip and fed into our codec model, HAC -- a standard protocol in the audio codec liteature.



## Results 
<!-- The results presented are from a trained model at a training step of 200k out of 500k with effective batch size of 32.  -->

| Ground Truth (test sample) | Reconstructed Sample (v1.3) | Reconstructed Sample (v1.2) | Reconstructed Sample (v1.1) |
| --- | ---------------------------- | ---------------------------- | ---------------------- |
| <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/test/0.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.3-0.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.2-0.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.1-0.wav" type="audio/mpeg"></audio> |
| <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/test/1.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.3-1.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.2-1.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.1-1.wav" type="audio/mpeg"></audio> |
| <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/test/2.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.3-2.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.2-2.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.1-2.wav" type="audio/mpeg"></audio> |
| <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/test/3.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.3-3.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.2-3.wav" type="audio/mpeg"></audio> |
| <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/test/4.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.3-4.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.2-4.wav" type="audio/mpeg"></audio> |
| <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/test/5.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.3-5.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.2-5.wav" type="audio/mpeg"></audio> |
| <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/test/6.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.3-6.wav" type="audio/mpeg"></audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v1.2-6.wav" type="audio/mpeg"></audio> |


## Metrics

We present PESQ (Perceptual Evaluation of Speech Quality) and SI-SDR (Scale-Invariant Signal-to-Distortion Ratio).
PESQ and SI-SDR scores are typically considered to be quite good when above 2.0, and 5.0, respectively.


| Model | PESQ | SI-SDR |
| ----- | ----- | ----- | 
| HAC v1.3 | 2.5 | 8.9 |
| HAC v1.2 | 2.4 | 8.6 |






***

# Model Specification Histories

### ver.1.2 (20.11.2024)
- model size: 6M parameters (12 MB in bfloat16, 24 MB in float32)
- kbps (kilobits per sec): 3.6
    - number of tokens/s: 200
- codec model components
  - input: waveform
    - before fed into the encoder, a waveform is transformed into a complex spectrogram with STFT.
  - encoder: separable 1d causal convolutional layers with SMU (Smooth Maximum Unit) activation
      - two types of 1d convolutional layers, one sweeping over a frequency dimension and another over a temporal dimension.
  - quantizer: binary scalar quantization (a variant of Look-up Free Quantization from the MaskBit paper)
  - decoder: reverse of the encoder architecture, followed by ISTFT.
- loss
  - reconstruction loss on
    - waveforms
    - multiple STFT spectrograms
  - GAN loss with
    - multiple STFT discriminator
- misc
  - input scaling (z-norm)
  - feature map scaling with standard deviation instead of absolute magnitude
  - scales are computed with EMA


### ver.1.1 (21.10.2024)
- model size: 4M parameters (8 MB in bfloat16, 16 MB in float32)
- kbps (kilobits per sec): 1.35
    - number of tokens/s: 75
- codec model components
  - input: waveform
  - encoder: separable 1d causal convolutional layers with Snake activation
  - quantizer: binary scalar quantization (a variant of Look-up Free Quantization from the MaskBit paper)
  - decoder: reverse of the encoder architecture
- loss
  - reconstruction loss on
    - waveforms
    - multiple mel-spectrograms
  - GAN loss with
    - multiple STFT discriminator
    - multiple filter band discriminator
  - perceptual loss with Whisper