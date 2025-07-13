+++
date = '2025-07-13T09:38:41-07:00'
draft = true
title = ''
+++

# ALT Firmware for Sitka Instruments Gravity

This is a collection of alt firmware made for Sitka Instruments Gravity
using the forthcomming `libGravity` library. This library helps make writing
firmware easier by abstracting away the initialization and peripheral
interactions. Now your firmware code can just focus on the logic and behavior
of the app, and keep the low level code neatly tucked away in this library.


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

The Gravity firmware is a slightly different implementation of the original
firmware. There are a few notable changes; the internal clock operates at
96 PPQN instead of the original 24 PPQN, which allows for more granular
quantization of features like duty cycle (pulse width) or offset.
Additionally, this firmware replaces the sequencer with a Euclidean Rhythm
generator.

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
     External clock input. When Gravity is set to INTERNAL clock mode, this
     input is used to reset clocks.

CV1:
     External analog input used to provide modulation to any channel parameter.
CV2:
     External analog input used to provide modulation to any channel parameter.
```

{{< firmware_button hex="Gravity" buttonText="Flash Alt Gravity Firmware" >}}

