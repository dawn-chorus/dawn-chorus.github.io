# Motivation 

Because of the computing power they need, most of today's [additive](https://en.wikipedia.org/wiki/Additive_synthesis) synthesizers are implemented as virtual instruments (VSTs). Thus they are typically run on desktop computers.

This way of working has several drawbacks:
1. [Desktop computers](https://support.apple.com/en-us/HT201918) and [laptops](https://www.mtech.news/article/MacBook-Pro-2021-M1-Max-Power-Consumption-Low-And-High-Power-Mode-175284) are relatively power-hungry
2. This kind of setup is expensive: an entire setup (all software components and the PC itself) could be well over 1000€.
3. A direct access to the parameters of the synthesizer requires screen/mouse interaction (or the previous programming of an external hardware controller). Plus a desktop requires time to boot, and that's a downer.

For those reasons, I have been wanting to harness the parallelization potential of FPGAs to create **a hardware synth capable of matching the performance of desktop CPUs on additive synthesis**.
In the end, my goal was to develop a little additive synth with the following criteria:
- Relatively cheap (goal for my prototype: < 200€).
- Small form factor (easily transportable).
- Reduced power consumption (< 10W).

This design was to be based on Terasic's de10-nano SoC, hence the name **adde10**. 
In the following, I describe the initial requirements that I had for the adde10.
# Specs

I wanted a frequency range of 0.5Hz to 20kHz with 0.005Hz resolution, 8-voice polyphony and the *maximum amount of partials* given the other parameters. 

I also wanted to incorporate cool audio effects operating on the partials such as in the [Loom II](https://www.airmusictech.com/virtual-instruments/loom-ii.htmlhttps://www.airmusictech.com/virtual-instruments/loom-ii.html). 

| Parameter  | Value  |
|---|---|
| Frequency range  | 0.5Hz -> 20kHz with a 0.005Hz resolution  |
| Voices  | 8  |
| Number of partials  | Max, considering other parameters  |
| Spectra  | Harmonic  |