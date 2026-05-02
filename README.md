# Ideal, Natural, & Flat-top -Sampling
# Aim
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
# Tools required
Google Colab
# Program
# 1.IDEAL SAMPLING:
```import numpy as np
import matplotlib.pyplot as plt

# Original signal
t = np.linspace(0,1,500)
x = np.sin(2*np.pi*5*t)

# Sampling
fs = 100
Ts = 1/fs
n = np.arange(0,1,Ts)
xs = np.sin(2*np.pi*5*n)

# Reconstruction
xr = 0
for i in range(len(n)):
    xr += xs[i]*np.sinc((t-n[i])/Ts)

# Plot
plt.plot(t,x,label="Original")
plt.stem(n,xs,label="Impulse Sampling")
plt.plot(t,xr,'g--',label="Reconstructed")

plt.legend()
plt.grid()
plt.show()
```
# 2.NATURAL SAMPLING:
```import numpy as np
import matplotlib.pyplot as plt

# -----------------------------
# 1. Original Signal
# -----------------------------
t = np.linspace(0, 1, 1000)
f = 5
x = np.sin(2*np.pi*f*t)

# -----------------------------
# 2. Pulse Train
# -----------------------------
fs = 50
Ts = 1/fs
pulse_width = Ts/4

pulse = np.where((t % Ts) < pulse_width, 1, 0)

# -----------------------------
# 3. Natural Sampling
# -----------------------------
sampled = x * pulse

# -----------------------------
# 4. Reconstruction (LPF approx)
# -----------------------------
xr = np.convolve(sampled, np.ones(20)/20, mode='same')

# -----------------------------
# 5. Plot (4 graphs like your image)
# -----------------------------
plt.figure(figsize=(10,8))

# Original signal
plt.subplot(4,1,1)
plt.plot(t, x)
plt.title("Original Message Signal")
plt.grid()

# Pulse train
plt.subplot(4,1,2)
plt.plot(t, pulse)
plt.title("Pulse Train")
plt.grid()

# Natural sampled signal
plt.subplot(4,1,3)
plt.plot(t, sampled)
plt.title("Natural Sampling")
plt.grid()

# Reconstructed signal
plt.subplot(4,1,4)
plt.plot(t, xr, 'g')
plt.title("Reconstructed Message Signal")
plt.grid()

plt.tight_layout()
plt.show()
```
# 3.FLAT-TOP SAMPLING:
```import numpy as np
import matplotlib.pyplot as plt

# 1. Original signal
t = np.linspace(0, 1, 500)
x = np.sin(2*np.pi*5*t)

# 2. Sampling
fs = 50
Ts = 1/fs
n = np.arange(0, 1, Ts)
xs = np.sin(2*np.pi*5*n)

# 3. Flat-top sampling (hold value)
flat = np.zeros_like(t)
for i in range(len(n)):
    flat[(t >= n[i]) & (t < n[i] + Ts/2)] = xs[i]

# 4. Reconstruction (simple smoothing)
xr = np.convolve(flat, np.ones(10)/10, mode='same')

# 5. Plots
plt.figure(figsize=(8,8))

plt.subplot(4,1,1)
plt.plot(t, x)
plt.title("Original Signal")

plt.subplot(4,1,2)
plt.stem(n, np.ones(len(n)))
plt.title("Sampling Instants")

plt.subplot(4,1,3)
plt.plot(t, flat)
plt.title("Flat-Top Sampled")

plt.subplot(4,1,4)
plt.plot(t, xr)
plt.title("Reconstructed")

plt.tight_layout()
plt.show()
```
# Output Waveform
# 1.IMPULSE SAMPLING OUTPUT WAVEFORM:
<img width="739" height="526" alt="image" src="https://github.com/user-attachments/assets/e86d8d3c-b79c-41d4-baf9-40e612092b45" />
# 2.NATURAL SAMPLING OUTPUT WAVEFORM:
<img width="947" height="756" alt="image" src="https://github.com/user-attachments/assets/02108d18-3292-4340-8693-d6469881ea5d" />
# 3.FLAT-TOP SAMPLING OUTPUT WAVEFORM:
<img width="777" height="761" alt="image" src="https://github.com/user-attachments/assets/2de9ac57-325b-4f04-9fd8-b801173a36bc" />

# Results
Thus, the construction and reconstruction of Ideal, Natural, and Flat-top sampling were successfully implemented and the corresponding waveforms were obtained.
