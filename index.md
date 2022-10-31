Hey ! This is my blog about adde10, the additive synthesizer that I made on the de10-nano. Tag along if you want to know how I created it.

The sources are all available on github.

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

This design was to be based on Terasic's [de10-nano](https://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&CategoryNo=205&No=1046&PartNo=4) SoC, hence the name **adde10**. 
In the following, I describe the initial requirements that I had for the adde10.
# Specs

## Requirements

### Strong requirements

Every parameter of the synthesizer should be [MIDI](https://en.wikipedia.org/wiki/MIDI) controllable. 
I wanted a frequency range of 0.5Hz to 20kHz with 0.005Hz resolution and 8 (detuneable) voice polyphony.

I also wanted to incorporate cool audio effects operating on the partials such as:
- Controllable comb filters
- The reverb or phaser of [Loom II](https://www.airmusictech.com/virtual-instruments/loom-ii.htmlhttps://www.airmusictech.com/virtual-instruments/loom-ii.html)

Given those requirements and the FPGA capability, I want to have *the maximum amount of partials* for each voice.

### Nice to have 

If manageable, I wanted to add support for inharmonic spectrum-- in general, I wanted to cram as many fonctionalities as it is possible in adde10. 

### Summary 

| Parameter  | Value  |
|---|---|
| Frequency range  | 0.5Hz -> 20kHz with a 0.005Hz resolution  |
| Voices  | 8  |
| Effects  | At least one between partial reverb or partial phaser; Comb filters |
| Spectrum  | Harmonic (Inharmonic if possible) |
| Number of partials  | Max, considering other parameters  |

## Hardware and software architecture

The de10-nano architecture allowed me to take advantage of a HPS + FPGA combo to meet my needs.
In this section, I describe how I chose to implement the synthesizer with the previous requirements in mind. 

### Parameter parsing 

An user should interact with the underlying synthesizer engine with physical controls. This is achievable with a MIDI controller. 
For convenience purposes, I chose to develop the software responsible for the parsing of the MIDI from the controller **on the HPS**. 

### Audio generation

Those parameters should then be formatted and transmitted for the FPGA, which is used for audio waveforms generation. 

### Additional components 

- USB to micro-USB adapter (for my MIDI controller)
- HDMI audio splitter 

