# Fourier Analysis Tutorial
Adapted from [original material](https://ccrma.stanford.edu/~jos/mdft/FFT_Simple_Sinusoid.html) by Julius O. Smith III.

To evaluate, you should press enter after each command.
If you put a semicolon after a command, it is not printed in the command window.

## Part 1: FFT of a DFT-sinusoid

Set parameters:
```matlab
N = 64;              % Must be a power of two
T = 1;               % Set sampling rate to 1
A = 1;               % Sinusoidal amplitude
phi = 0;             % Sinusoidal phase
f = 0.25;            % Frequency (cycles/sample)
n = [0:N-1];         % Discrete time axis
x = A*cos(2*pi*n*f*T+phi); % Sampled sinusoid
X = fft(x);          % Spectrum
```

Plot time data:
```matlab
figure('color','w');
subplot(3,1,1);
hold('on');
plot(n,x,'ok');
ni = [0:.1:N-1];     % Interpolated time axis
plot(ni,A*cos(2*pi*ni*f*T+phi),'-k'); grid off;
title('Sinusoid at 1/4 the Sampling Rate');
xlabel('Time (samples)');
ylabel('Amplitude');
text(-8,1,'a)');
```

Plot spectral magnitude:
```matlab
magX = abs(X);
fn = [0:1/N:1-1/N];  % Normalized frequency axis
subplot(3,1,2);
grid('on');
stem(fn,magX,'ok');
xlabel('Normalized Frequency (cycles per sample))');
ylabel('Magnitude (Linear)');
text(-0.11,40,'b)');
```

Same thing but on a decibel (dB) scale:
```matlab
spec = 20*log10(magX); % Spectral magnitude in dB
subplot(3,1,3);
plot(fn,spec,'--ok'); grid on;
axis([0 1 -350 50]);
xlabel('Normalized Frequency (cycles per sample))');
ylabel('Magnitude (dB)');
text(-0.11,50,'c)');
```

### Part 2: FFT of a not-so-simple sinusoid

Example 2 is Example 1 but with frequency between bins

```matlab
f = 0.25 + 0.5/N;   % Move frequency up 1/2 bin

x = cos(2*pi*n*f*T); % Signal to analyze
X = fft(x);          % Spectrum
...                  % See Example 1 for plots and such
```

Plot the periodic extension of the time-domain signal:
```matlab
plot([x,x],'--ok');
title('Time Waveform Repeated Once');
xlabel('Time (samples)');
ylabel('Amplitude');
```
