# WaveMix controller

## Intro

This generates eight 0 to 5V CV signals to drive the WaveMix eight-channel CV-controlled mixer.

It corresponds to the left-hand part of an Ondes Martenot *tiroir* which has seven waveform select
switches plus level control sliders (for three of the waveforms) and an "all on" *tutti* switch.
In this implementation each waveform was a slider. The mixer needs 5V for no attenuation, zero for 
max attenuation and the volume law is "semi logarithmic".

## Details

To avoid glitches caused by the VCAs in the mixer changing attenuation value too fast, when a 
waveform switches on or off the microcontroller generates a ramp from the currently selected value 
to zero (or from zero to the selected value). 

To avoid clipping in the VCAs or in the mixing stage,
the maximum level is monitored and all the levels are reduced if a large number of waveforms are 
simultaneously enabled.

Waveform level is determined by measuring the analog voltage across 7 sliders driven from a voltage reference to analog ground.
Waveforms are switched on by seven switches (plus an eighth tutti switch) and their state indicated by eight boicolor
red/green LEDs. Red means disabled, green is enabled and orange is "tutti on".

Because the WaveMix is actually two quad mixers internally (made from a pair of L-1 2180 VCA/mix boards) eight
CVs are needed: four for the first four waveforms (the flat-topped ones, N C G g) which are submixed and sent to the 
mixer send. This is normalled to mixer return together with the other three waveforms (O, 8, S) for a second, four 
to one mixdown. Therefore the eighth CV is for submix level, and max volume is evaluated separately for the 
two four-channel mixers.

## Circuit

A Teensy 3.0 is used as the microcontroller. Unless there are noise issues I plan to use the internal 1.2V 
reference to drive the sliders. Switches use the Bounce library.

The eight bicolor LEDs are controlled with a MCP23017 multiplexer.

A separate board holds a TI DAC8568 and eight unity-gain output buffers (TL074 * 2). For reliable performance, a level 
shifter is used on the SPI lines to convert to 5V logic.

## Implementation

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
