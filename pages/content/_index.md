+++
title= "ALT Firmware for Sitka Instruments Gravity"
layout= "single"

+++

This is a collection of alt firmware made for [Sitka Instruments Gravity](https://sitkainstruments.com/gravity/)
using the open source [`libGravity`](https://git.sitkainstruments.com/awonak/libGravity)
library. This library helps make writing firmware easier by abstracting away
the initialization and peripheral interactions. Now your firmware code can
just focus on the logic and behavior of the app, and keep the low level code
neatly tucked away in this library.

https://git.sitkainstruments.com/awonak/libGravity


{{< firmware_dropdown >}}

```
NOTE: Make sure your Gravity module is disconnected from
the eurorack power and the MIDI expander before flashing.
```

```
WARNING: Flashing this firmware will erase any saved data
from your previously installed firmware!
```

## ALT-GRAVITY

This version of Gravity firmware is a full rewrite that leverages the
`libGravity` hardware abstraction library. The goal of this project was to
create an open source friendly version of the firmware that makes it easy
for users/developers to modify and create their own original alt firmware
implementations.

The `libGravity` library represents wrappers around the
hardware peripherials to make it easy to interact with and add behavior
to them. The library tries not to make any assumptions about what the
firmware can or should do.

The Alt-Gravity firmware is a slightly different implementation of the original
firmware. There are a few notable changes; the internal clock operates at
96 PPQN instead of the original 24 PPQN, which allows for more granular
quantization of features like duty cycle (pulse width) or offset.

{{< youtube BWwTnOQUQrQ >}}

```yaml
ENCODER:
     Press: change between selecting a parameter and editing the parameter.
     Hold & Rotate: change current selected output channel.

BTN1:
     Play/pause: start or stop the internal clock.

BTN2: 
     Shift: hold and rotate encoder to change current selected output channel.

EXT:
     External clock input. When Gravity is set to INTERNAL or MIDI clock
     source, this input is used to reset clocks.

CV1:
     External analog input used to provide modulation to any channel parameter.
CV2:
     External analog input used to provide modulation to any channel parameter.
```


## Euclidean

The Euclidean firmware is an alternative sequencer for the Gravity module that
generates polyrhythmic Euclidean rhythms instead of traditional linear 
sequences. The dual CV inputs can be assigned per  channel to dynamically
modulate clock divisions/multiplications, Euclidean steps, or the number of
hits in real-time. It also includes a menu system accessible via the encoder
and buttons, allowing control over playback, muting, clock routing, external
sync, and saving/loading patterns and settings to hardware EEPROM slots.

```yaml
ENCODER:
     Press: change between selecting a parameter and editing the parameter.
     Hold & Rotate: change current selected output channel.

BTN1:
     Play/pause: start or stop the internal clock.

BTN2: 
     Shift: hold and rotate encoder to change current selected output channel.

EXT:
     External clock input. When Gravity is set to INTERNAL or MIDI clock
     source, this input is used to reset clocks.

CV1:
     External analog input used to provide modulation to any channel parameter.
CV2:
     External analog input used to provide modulation to any channel parameter.
```

## Comparator

The Comparator firmware transforms the Gravity module into a CV rate 
dual-window comparator for analyzing CV signals. It utilizes CV1 and CV2 
as separate inputs, offering an intuitive OLED visualization of both comparator
windows spanning a -5V to +5V bounds. You can quickly toggle between adjusting
the Shift and Size of either comparator using the buttons and rotary encoder.
The module provides six distinct logic outputs based on the voltage
windows: individual Gates for each comparator, combined boolean logic
(AND, OR, XOR), and a Flip-Flop state. 

Additionally, when pressing both buttons, the module enters CV calibration mode
for improving the accuracy of the input's voltage tracking. Exiting calibration
mode automatically saves your calibration settings and will persist across power
cycles.

{{< youtube eGmMma-BIGo >}}

```yaml
CV1:
     Analog input for Comparator 1 in the range of -5V to +5V.
CV2:
     Analog input for Comparator 2 in the range of -5V to +5V.

BTN1:
     Toggles between editing Comparator 1 and Comparator 2 values.
BTN2: 
     Toggles the active parameter between the Shift and Size of the selected 
     Comparator window.
BTN1 + BTN2:
     Switch between Comparator mode and CV input calibration mode.

CH 1 (Gate 1): 
     Outputs +5V while CV 1 is actively inside Comparator 1's bounds.
CH 2 (Gate 2): 
     Outputs +5V while CV 2 is actively inside Comparator 2's bounds.
CH 3 (AND Logic): 
     Outputs +5V only when Gate 1 AND Gate 2 are active simultaneously.
CH 4 (OR Logic): 
     Outputs +5V when either Gate 1 OR Gate 2 (or both) are active.
CH 5 (XOR Logic): 
     Outputs +5V exclusively when either Gate 1 or Gate 2, but not both, 
     are active.
CH 6 (Flip-Flop Logic): 
     Rising edges of the XOR signal toggle the flip-flop on or off.

```

## Parametric Rhythm

The Parametric Rhythm firmware is an alternative sequencer for the Gravity
module that generates complex drum patterns by traversing 2D interpolation
density maps, similar to Mutable Instruments Grids. The dual CV inputs can
be assigned globally to dynamically modulate Kick, Snare, or HiHat densities,
the amount of generated Chaos, or the X/Y interpolation positions in real-time.
CV can also be routed to completely alter the selected pattern preset A-E. 

It includes an intuitive menu system accessible via the encoder and buttons, 
allowing control over playback, clock routing, external sync, pulse out
subdivisions, and saving/loading pattern density settings natively to the
hardware EEPROM. Press and hold the encoder button and rotate to select
different pattern presets.

{{< youtube 6aIP3p6gWdI >}}

```yaml
ENCODER: 
     Press: change between selecting a parameter and editing the parameter value.
     Hold & Rotate: change between the Global Settings menu and Pattern Presets A-E.

BTN1 (PLAY): 
     Play/pause: start or stop the internal clock and reset output gates.

BTN2 (SHIFT): 
     Reset: sets all gates low and returns the sequencer back to the first step.

EXT: 
     External clock input. Advances the sequencer by the selected PPQN amount. When
     Gravity is set to INTERNAL or MIDI clock source, this input is instead used as
     an external sequencer reset.

CV1 & CV2: 
     External analog inputs used to provide real-time modulation to any pattern 
     parameter, or dynamically jump between loaded pattern preset slots A-E.

```

# Feedback

This is a beta release which may contain bugs, or have room for improvement.
Your feedback is crutial to help ensure the new firmware is well received when
it is officially published. We need your help to make this a success!

You can help by submitting Gitea issues [here](https://github.com/awonak/alt-gravity/issues)
for bug reports, feedback, or any ideas you've got. 

https://github.com/awonak/alt-gravity/issues

If you don't want to submit feedback on the public Gitea site, feel free to
shoot me an email at adam.wonak@gmail.com.
