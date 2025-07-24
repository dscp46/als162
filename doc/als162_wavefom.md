# ALS162 Time Signal
> [!WARNING]
> This document is in construction. Accuracy of its content is not guaranteed.

The Allouis time signal, formerly used as France Inter's AM center carrier, is now broadcasted as a standalone signal.

The signal is phase modulated, and is composed as follow (original illustration comes from GRcon23 slideware[^1]):

![ALS162 Waveform](als162_waveform.png)

The 1PPS event happens on the vertical marker, at the zero crossing on the falling edge, prior to the timecode bit time slot (colored in yellow).
The green time slot is defined as the "quiet" time slot, and can be used to measure signal phase.


[^1]: [ALS162 Time Signal SDR Receiver for GNU Radio](https://events.gnuradio.org/event/21/contributions/415/attachments/139/320/ALS162_slides_henningM1r.pdf), Henning Maier
