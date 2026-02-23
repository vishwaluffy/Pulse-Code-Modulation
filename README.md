# Pulse-Code-Modulation
# Aim
Write a simple Python program for the modulation and demodulation of PCM, and DM.
# Tools required
 COLAB
# Program
```
1.PULSE CODE-MODULATION
import numpy as np
import matplotlib.pyplot as plt
fs, f, T, L = 5000, 50, 0.1, 16
t = np.linspace(0, T, int(fs*T), endpoint=False)
msg = np.sin(2*np.pi*f*t)
clk = np.sign(np.sin(2*np.pi*200*t))
# Quantization (PCM)
step = (msg.max() - msg.min()) / L
q_msg = np.round(msg / step) * step
plt.figure(figsize=(10,8))
plt.subplot(4,1,1)
plt.plot(t, msg); 
plt.title("Analog Message");
 plt.grid()
plt.subplot(4,1,2)
plt.plot(t, clk); 
plt.title("Clock Signal"); 
plt.grid()
plt.subplot(4,1,3)
plt.step(t, q_msg); 
plt.title("PCM Signal"); 
plt.grid()
plt.subplot(4,1,4)
plt.plot(t, q_msg, '--'); 
plt.title("PCM Demodulation"); 
plt.grid()
plt.tight_layout()
plt.show()
```
```
2.DELTA-MODULATION
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, filtfilt
# Parameters
fs, f, T, delta = 10000, 10, 1, 0.1
t = np.arange(0, T, 1/fs)
msg = np.sin(2*np.pi*f*t)
# Delta Modulation
dm = [0]
bits = []
for s in msg:
    step = delta if s > dm[-1] else -delta
    bits.append(1 if step > 0 else 0)
    dm.append(dm[-1] + step)
demod = np.cumsum([0] + [delta if b else -delta for b in bits])
b, a = butter(4, 20/(0.5*fs), 'low')
filt = filtfilt(b, a, demod)
plt.figure(figsize=(10,6))
plt.subplot(3,1,1)
plt.plot(t, msg); 
plt.title("Original Signal"); 
plt.grid()
plt.subplot(3,1,2)
plt.step(t, dm[:-1], where='mid'); 
plt.title("Delta Modulated Signal"); 
plt.grid()
plt.subplot(3,1,3)
plt.plot(t, filt[:-1], 'r:'); 
plt.title("Demodulated Signal"); 
plt.grid()
plt.tight_layout()
plt.show()
```
# Output Waveform

```
1.PULSE CODE-MODULATION
```
<img width="798" height="633" alt="image" src="https://github.com/user-attachments/assets/b3a90764-04a7-47ea-acc7-9fba2f12cb43" />

2.DELTA-MODULATION

<img width="797" height="474" alt="image" src="https://github.com/user-attachments/assets/3dcc572a-6028-4cb8-9259-b4385987ee88" />

# Results

The analog signal was successfully encoded and reconstructed using PCM and DM techniques in Python, verifying their working principles.


