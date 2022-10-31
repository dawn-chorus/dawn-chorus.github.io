# Motivation 

Because of the computing power they need, most of today's [additive](https://en.wikipedia.org/wiki/Additive_synthesis) synthesizers are implemented as virtual instruments (VSTs). Thus they are typically run on desktop computers.

This way of working has several drawbacks:
1. Desktop computers are relatively power-hungry. Laptops consume around 70W on average.
2. This kind of setup is relatively expensive: an entire setup (all software components and the PC itself) could be well over 1000€.
3. A direct access to the parameters of the synthesizer requires screen + mouse interaction (or the previous programming of an external hardware controller). Plus a desktop requires time to boot, and that's a downer.

For those reasons, I have been wanting to harness the parallelization potential of FPGAs to create a hardware synth capable of matching the performance of desktop CPUs on additive synthesis. 
My goal was to develop a little additive synth with the following criteria:
- Relatively cheap (goal for my prototype: < 200€).
- Small form factor (easily transportable).
- Reduced power consumption (< 10W).

# Specs

