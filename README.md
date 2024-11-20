
<div style="text-align: center;">
  <img src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/blob/main/fig/hac_logo.png?raw=true" alt="method" style="width: 30%;">
</div>

# HANCE Audio Codec (HAC) (ver. 21.10.2024)

An audio codec model consisting of encoder, quantizer, and decoder. Its design principals are 1) light-weight, 2) high compression rate, and 3) high fidelity.



# Model Specifications


### ver. 02 (04.11.2024)
- model size: 4M parameters (8MB in bfloat16, 16MB in float32)
- kbps (kilobits per sec): 1.35
    - number of tokens/s: 75
- codec model components
  - encoder: separable downsampling CNN layers with Snake activation
  - quantizer: binary scalar quantization (a variant of look-up free quantization from the MaskBit paper)
  - decoder: separable upsampling CNN layers with Snake activation
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


### ver. 01 (21.10.2024)
- model size: 4M parameters (8MB in bfloat16, 16MB in float32)
- kbps (kilobits per sec): 1.35
    - number of tokens/s: 75
- codec model components
  - encoder: separable downsampling CNN layers with Snake activation
  - quantizer: binary scalar quantization (a variant of look-up free quantization from the MaskBit paper)
  - decoder: separable upsampling CNN layers with Snake activation
- loss
  - reconstruction loss on
    - waveforms
    - multiple mel-spectrograms
  - GAN loss with
    - multiple STFT discriminator
    - multiple filter band discriminator
  - perceptual loss with Whisper


### Comparison to the Existing Models

| Model | #Params (Million) | kbps |
| ----- | ----- | ----- | 
| EnCodec | 14.9 | 3, 6 |
| DAC | 74.18 | 4, 9 |
| HILCodec | 9.6 | 3, 6 |
| HAC | 4 | 1.35 |


<div style="text-align: left;">
  <img src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/blob/main/fig/table_fig.png?raw=true" alt="method" style="width: 70%;">
</div>


Remarks
- the lightest model of all known models with the highest compression rate.
- to have a more fine-grained control over the timesteps, we're planning to relax "num_tokens/s" to 150 (6.7 millisecond per token)
<!-- - Once relaxed, it should be possible to have the model size below 8MB due to the relaxed compression rate to enable real-time processing on CPU. -->


# Results

| Ground Truth (test sample) | Reconstructed Sample (v2; 103k training step) | Reconstructed Sample (v1) |
| --- |----------------------------|----------------------|
| <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/test/0.wav" type="audio/mpeg">Your browser does not support the audio element.</audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v2_0.wav" type="audio/mpeg">Your browser does not support the audio element.</audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/0.wav" type="audio/mpeg">Your browser does not support the audio element.</audio> |
| <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/test/1.wav" type="audio/mpeg">Your browser does not support the audio element.</audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v2_1.wav" type="audio/mpeg">Your browser does not support the audio element.</audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/1.wav" type="audio/mpeg">Your browser does not support the audio element.</audio> |
| <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/test/2.wav" type="audio/mpeg">Your browser does not support the audio element.</audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/v2_2.wav" type="audio/mpeg">Your browser does not support the audio element.</audio> | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/2.wav" type="audio/mpeg">Your browser does not support the audio element.</audio> |


# Objective Evaluations
PESQ


# Analysis
 
 in my ppt.

