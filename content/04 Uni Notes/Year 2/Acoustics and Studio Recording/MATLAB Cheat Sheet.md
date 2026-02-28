```python
% Function to convolve an Impulse Response (IR) with an Anechoic Recording
% to produce both time-domain and frequency-domain convolution results.
% Developed by Andrew Stanton. This function takes both audio files,
% converts them to mono if they are stereo, and outputs two audio files:
% one for time-domain convolution and one for frequency-domain convolution.
%
% Example usage:
% AudioToConv('ImpulseResponse.wav', 'AnechoicRecording.wav')
%
% Output:
% - TDC_<IR>_<Anechoic>.wav : Result of the time-domain convolution
% - FDC_<IR>_<Anechoic>.wav : Result of the frequency-domain convolution
```
