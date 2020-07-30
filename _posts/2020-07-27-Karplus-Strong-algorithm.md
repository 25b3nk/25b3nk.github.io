---
layout: post
title: Karplus-Strong Algorithm
description: Simple digital feedback algorithm to synthesize musical sounds
tags: maths dsp
last_modified: 2020-07-30 17:30:00 +0000
---

## Introduction
We might want to have a little background on what discrete signals are, then we need to know what finite signals, infinite signals, recursive signals & its frequency are. Discrete signals are photographs of signals taken in certain time interval $$T_s$$, with corresponding sampling frequency $$F_s = 1 / T_s$$. These signals can have a frequency $$f$$ with which it is repeating. Say, if $$M$$ samples for one unique sequence, then $$f = 1 / M T_s$$ or $$f = F_s / M$$.

Let us take a look at the feedback system:

![Karplus-Strong-Feedback-System](/public/images/Karplus-Strong-digital-feedback.png)

In the above diagram, we see that the input is taken as it is and added to delayed output signal. The delay unit $$z^{-M}$$ acts as a memory cell, which stores $$M$$ signals before it outputs back the first signal. This unit is a [`FIFO`](https://en.wikipedia.org/wiki/FIFO_(computing_and_electronics)#:~:text=FIFO%20%E2%80%93%20an%20acronym%20for%20first,the%20queue%2C%20is%20processed%20first.){:target="_blank"}, i.e, the first signal stored in this unit will be the first to be sent out. Then we have the scaling factor $$\alpha$$, which will scale the output of the delay unit. Generally, this would be lesser than to 1, to give the damping effect.

Here, we can observe that, to generate periodic signals, we have to set the delay $$M$$ to be equal to the number of samples in the input signal $$x[n]$$.

Now let us take a finite signal $$x[n]$$ which has $$M$$ samples as input to our feedback system and generate the output periodic signal with the input as constituent.


## Coding Karplus-Strong Algorithm


```python
%matplotlib inline
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
import IPython
```


```python
plt.rcParams["figure.figsize"] = (14,4)
```

We set the sampling frequency which will later be used to play audio.


```python
Fs = 16000 # 16 KHz sampling rate
```

The above sampling frequency means that, there would be 16000 samples of data per second.

In Karplus-Strong (K-S) Algorithm, the period of the output signal is the length of the input finite signal. Say, if we have 50 samples in the input signal, then frequecy will be $$f = F_s / M$$, i.e, 16000/50, which would be $$320 Hz$$. 

Now let us choose an input signal with random values.


```python
x_n = np.random.randn(50)
plt.stem(x_n);
```


![png](/public/images/KS_output_6_1.png)


Now let us define a function which returns output signal generated using K-S algorithm. Here we define the total number of output data points, as in theory, K-S algorithm generates infinite signal.


```python
def KS(x, N, alpha=1):
    M = len(x)
    y = np.zeros(N)
    for n in range(0, N):
        y[n] = (x[n] if n < M else 0) + alpha * (y[n-M] if (n - M) >= 0 else 0)
    return y
```


```python
y = KS(x_n, Fs * 2)  # Fs * 2 will generate two seconds worth of data
```


```python
plt.stem(y[0:500]);  # Cause plotting the whole sequence would hang my device and plot would look clumsy
```

![png](/public/images/KS_output_10_1.png)



```python
IPython.display.Audio(y, rate=Fs)
```

<audio  controls="controls" >
    <source src="/public/audio/KS-1.wav" type="audio/wav"/>
    Your browser does not support the audio element.
</audio>



Now let us generate the output signal with some dampening effect. Let us provide $$\alpha = 0.99$$.


```python
y = KS(x_n, Fs * 2, alpha=0.99)
```


```python
plt.stem(y[0:2000]);
```



![png](/public/images/KS_output_14_1.png)


One can observe the dampening amplitude above.


```python
IPython.display.Audio(y, rate=Fs)
```

<audio  controls="controls" >
    <source src="/public/audio/KS-2.wav" type="audio/wav"/>
    Your browser does not support the audio element.
</audio>


Now, we observe that everytime the initial buffer goes through the loop, it gets multiplied by $$\alpha$$. So we can rewrite the equation as

$$
  y[n] = \alpha^{\lfloor n/M \rfloor} x [n\mod M]
$$

Here, clearly the decay is dependent on $$\alpha$$ and $$M$$.
And this would cause the higher pitched notes to decay faster. So let first see that:


```python
y1 = KS(np.random.randn(50), Fs * 2, alpha=0.99)
IPython.display.Audio(y1, rate=Fs)
```


<audio  controls="controls" >
    <source src="/public/audio/KS-3.wav" type="audio/wav"/>
    Your browser does not support the audio element.
</audio>



```python
y2 = KS(np.random.randn(10), Fs * 2, alpha=0.99)
IPython.display.Audio(y2, rate=Fs)
```


<audio  controls="controls" >
    <source src="/public/audio/KS-4.wav" type="audio/wav"/>
    Your browser does not support the audio element.
</audio>



Here, $$y2$$ is a higher pitched note as the frequency $$f = F_s / 10$$ is higher than that of $$y1$$ which is $$f = F_s / 50$$. And we observe the decay is quite fast in $$y2$$. As, this is not good, let us compensate for this by changing $$\alpha$$. We shall adjust alpha so that all the notes have a decay comparable to that of buffer length of 50. This way the decay timing would match for all the signals.


```python
def KS(x, N, alpha = 0.99):
    REF_LEN = 50
    M = len(x)
    a = alpha ** (float(M) / REF_LEN)
    y = np.zeros(N)
    for n in range(0, N):
        y[n] = (x[n] if n < M else 0) + a * (y[n-M] if n-M >= 0 else 0)
    return y
```

>
Here we are essentially replacing the denominator of power of $$\alpha$$ in the equation with fixed length by multiplying the actual length of the buffer and then dividing by the fixed length, and thereby replacing the denominator.


```python
IPython.display.Audio(KS(np.random.rand(50), Fs * 2), rate=Fs)
```


<audio  controls="controls" >
    <source src="/public/audio/KS-5.wav" type="audio/wav"/>
    Your browser does not support the audio element.
</audio>



```python
IPython.display.Audio(KS(np.random.rand(10), Fs * 2), rate=Fs)
```


<audio  controls="controls" >
    <source src="/public/audio/KS-6.wav" type="audio/wav"/>
    Your browser does not support the audio element.
</audio>



```python
IPython.display.Audio(KS(np.random.rand(100), Fs * 2), rate=Fs)
```


<audio  controls="controls" >
    <source src="/public/audio/KS-7.wav" type="audio/wav"/>
    Your browser does not support the audio element.
</audio>


## Applications


#### References
1. [Coursera's DSP course](https://www.coursera.org/learn/dsp/home/welcome)
