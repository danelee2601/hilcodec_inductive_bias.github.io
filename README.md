# Model Specifications

- model size: 4M parameters (16MB)
- kbps (kilobits per sec): 1.35
    - num_tokens/s: 75

Remarks
- the lightest model of all known models with the highest compression rate.
- to have a more fine-grained control over the timesteps, we're planning to relax "num_tokens/s" to 150 (6.7 millisecond per token)
- Once relaxed, it should be possible to have the model size below 8MB due to the relaxed compression rate to enable real-time processing on CPU.


# Results
| Ground Truth (test sample) | Reconstructed Sample |
|------|---------------|
| <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/test/0.wav" type="audio/    | <audio controls><source src="https://github.com/danelee2601/hilcodec_inductive_bias.github.io/raw/refs/heads/main/audio_samples/rec/0.wav" type="audio/mpeg">Your browser does not support the audio element.</audio> |




