# WaveMix controller

## Intro

This generates eight 0 to 5V CV signals to drive the [WaveMix](../wavemix/) eight-channel CV-controlled mixer.

It corresponds to the left-hand part of an Ondes Martenot *tiroir* which has seven waveform select
switches plus level control sliders (for three of the waveforms) and an "all on" *tutti* switch.
In this implementation each waveform was a slider. The mixer needs 5V for no attenuation, zero for
max attenuation and the volume law is "semi logarithmic".

The controller is intended to go in a tiroir-like controller skiff, with other controllers (pins, touche, and speaker control).

## Details

To avoid glitches caused by the VCAs in the mixer changing attenuation value too fast, when a
waveform switches on or off the microcontroller generates a ramp from the currently selected value
to zero (or from zero to the selected value).

To avoid clipping in the VCAs or in the mixing stage,
the maximum level is monitored and all the levels are reduced if a large number of waveforms are
simultaneously enabled.

Waveform level is determined by measuring the analog voltage across 7 sliders driven from a voltage reference to analog ground.
Waveforms are switched on by seven switches (plus an eighth tutti switch) and their state indicated by eight bicolor
red/green LEDs. Red means disabled, green is enabled and orange is "tutti on".

Because the [WaveMix](../wavemix/) is actually two quad mixers internally (made from a pair of L-1 2180 VCA/mix boards) eight
CVs are needed: four for the first four waveforms (the flat-topped ones, N C G g) which are submixed and sent to the
mixer send. This is normalled to mixer return together with the other three waveforms (O, 8, S) for a second, four
to one mixdown. Therefore the eighth CV is for submix level, and max volume is evaluated separately for the
two four-channel mixers.

## Circuit

In this first prototype, a Teensy 3.0 was used as the microcontroller. Could well be that a Teensy LC is sufficient. Only outer pins on the two long sides, plus the group of three inner through-hole pins (AREF, A10, A11) are used which are common to 3.x and LC. The inner pads (3.x only) are not used.

Unless there are noise issues I plan to use the internal 1.2V AREF
reference to drive the sliders. TEST total current draw on this with all 7 sliders!

Switches use the Bounce library, no hardware debounce circuitry.

The eight bicolor LEDs are controlled with a MCP23017 multiplexer. ([schematic](wavemix_T3_schem.pdf),
[board](wavemix_T3_brd.pdf))

![front](controller%20PCB%20front.png) ![back](controller%20PCB%20back.png)

A separate board holds a TI DAC8568 16-bit octal DAC, and eight unity-gain output buffers (TL074 * 2). For reliable performance, a level
shifter is used on the SPI lines to convert to 5V logic. ([schematic](OctalDAC.pdf), [board](OctalDAC_pcb.pdf))

![octal front](OctalDAC%20PCB%20front.png) ![octal back](OctalDAC%20PCB%20back.png)

In the first iteration, "outside the loop" protection resistors were used (although 47R rather than the typical 1k). This might be good enough, but a two resistors plus capacitor "in the loop" configuration would be better. Maybe switch to SMD or at least smaller resistors for the second iteration. Some thought to mounting holes would also be an improvement :)

Balanced output for reliable transmission of CV between skiff and main rig is planned, but not implemented in this first iteration of the circuit; balanced output on 8 Bantam TRS jacks or on one DB25 for the 8 signals.

## Software Implementation

### enable:

    *  calc new system max
    *  update all channels except the one just enabled, with new max (they get quieter)
    *  fade up new channel from zero to slider level over five milliseconds (avoid thumps)
    *  LED to green

### disable:

    *  fade down new channel from slider level to zero over five milliseconds (avoid thumps)
    *  calc new system max
    *  update all channels except the one just enabled, with new max (they get louder)
    *  LED to red

### fader change

    *  calc new system max
    *  update all channels

### tutti on:

    *  save slider levels and waveswitch state
    *  set system max to tutti max
    *  set 8 N C O G on, g S off
    *  fade all channels from old values to current
    *  update LEDs to orange
    *  now ignore sliders and switches

### tutti off:

    *  read slider levels and switches
    *  calc system max
    *  fade all channels from old values to current
    *  update LEDs based on switch state


## To Do

    * Need to find out how many dB attenuation per volt (complicated, semi-log)
    * ~~Need to find if negative CV needed for fully closed~~ (NO)
    * Measure output of prototype

## Panel

Eurorack-like 3U panel; outputs are on the back panel of a skiff rather than being on the main panel, so all the cables are out the way of the controllers.


7 sliders, 8 switches (7 waveforms plus tutti), 8 bicolor LEDs.