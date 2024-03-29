# Nasillard pulse maker

## Problem statement

Its a pulse wave, where the mark part is of a constant, fixed width regardless of frequency and the space part is whatever is needed for the frequency. So as the frequency increases and thus the wavelength decreases, the proportion of mark to space increases. I assume this will produce formants due to the non-harmonic nature of the pulse?

Also, how would you shape this in the analog domain, given a triangle wave input? I assume the circuit would trigger on a rising zero transition, generate the positive pulse, then go low until the next trigger.

(For the curious, this is the Nasillard waveform on an ondes Martenot, which I thought was a fixed 4% mark-space waveform because I only looked at a single frequency. I just discovered that it is not).

2890Hz (and multiples) formants. so 2,890^-1 / 2 = 1.73010380622837E-4 = 173μs pulse

TODO check again the pulse width and different audio frequencies.

> comparator, then monostable

"The inputs to an LM339 can not go beyond their supply pins. If it is powered off of +12v and ground then it's inputs must stay within that range."

"The output of the LM339 is open collector, so requires a pull-up resistor on it's output . It's output voltage goes down to the ground (minus power) pin voltage and goes up to whatever voltage you have the pull-up resistor tied to.

So if it is powered from ground and +12v, and the pull-up is tied to +12v, then the output will go between ground and +12v. Since it's open collector you can tie the pull-up to a different voltage than the positive supply (but it must be more positive than the ground/negative supply pin). So you could power it from +12v and have the pull-up tied to +5v, giving a zero to +5v output. Or power the chip on +5v and have the pullup tied to +12v, giving a zero to +12v output.

Unlike many other comparators, the LM339 can be powered off of large supplies. So it could be powered off of +/-12v or +/-15v and then the input and output would both be bipolar."

## Input voltage conditioning to unipolar

See Application Note snoaa35a for split voltage divider with clamp. Input series resistor R1a 70k and zener diode to ground gives max -600mV; then R1b 20k series and R2 10k to gnd reduces this to -200mV. Positive 10V becomes +1V meanwhile. Might be a bit low for the slope detector?

Or, inverting op-amp mix input tri with +5V (rough, 5V rail is ok) and overall gain 0.5ish to give 0 to -5V signal, then second inverting stage to restore positive signal.

Could either condition input, or condition output of comparator.

## LM339 comparator

Could run on +12 -12 to allow all possible input voltages. Needs two 100n bypass caps, from +12 to GND and -12 to GND. Note that output swings from pull-up voltage when high, to the negative rail voltage when low (17V swing) so will need clamping to 0V before sending to the monostable.

Alternatively, run on +12 0V so output low is 0V, and do the bipolar to unipolar conversion ahead of the comparator. Could use a zener diode, possibly with a voltage follower or two inverting stages.

Uh, and this is a quad but we don't need a window so a dual would be better.

Open-collector output pulled up to +5V to feed the 74HCT221

LM339AN is PDIP-14, LM339AD is SOIC-14

For rising/falling, see [CGS slope detector](https://www.elby-designs.com/webtek/cgs/cgs62/cgs62_sd.html).
The same signal is fed to both inputs of the comparator, but the negative input is fed by a 2k2 - 1M voltage divider to -12V to pull it low. The positive input is fed by an RC network with R = 10k + 1M trimmer, and C = 100n to ground. A rising voltage will be delayed by the RC circuit and rise slower, triggering the comparator. (That circuit assumes the next stage is inverting, so experiment and swap as needed).

LM393A or LM293A (PDIP, dual) comparators may be more suitable, rather than using only two comparators from a quad package. However, max input voltage is only V+ -2V. Maybe incorporate protection clipping to +10V?

Pull-up should give 100 μA to max 1mA current, so for a 5V pull up the resistor should be 4k7 to 47k, with larger resistance values providing a slower rise time.

## 74HCT221 dual retriggerable monostable multivibrator with reset

Needs a TTL-compatible 0V to 5V input.

- B input triggers on voltage level (2V for high) independent of rise time.
- Pulse width = 0.7 C R, 2k < R < 100k.
- 5V rail (4.5 to 5.5)
- SOIC-16 or DIP.

1.73010380622837E-4 / 0.7 / 10,000 = 2.47157686604053E-8 = 24.7nF for 10k
closest is 22nF so R = 1.73010380622837E-4 / 0.7 / 2.2E-8
= 11,234.4403001842 = 11.23kHz. Closest E96 is 11.5k

Vishay / Roederstein MKP1837322161 polypropylene 5mm spacing 1% $1.13/1 7.5x5.5mm case

Also see 12.1   Power-down considerations for protection circuit (Schottky diode across Rext)

Alternative, for breadboarding: Texas CD74HCT221E PDIP-16 $0.77/1

DC Supply Voltage, VCC range -0.5V to 7V and DC Input or Output Voltage, VI, VO 0V to VCC

Use a 1k input resistor for current limiting.

Use voltage follower output buffers to prevent negative inputs at the outputs, or high current drain if an output is shorted.


## BOM for breadboarding

All through hole, assume enough general resistors, 100n decoupling caps. Buy timing resistor and cap. Assume a general op-amp for output buffer?

- LM339AN * 4 $0.53/1 **$2.12**
- CD74HCT221E * 4 $0.77/1 **$3.08**
- MKP1837322161 * 2 (may well be wrong value) $1.07/1 **$2.14**
- 11.5k 0.1% 15ppm/C YR1B11K5CC  * 5 $0.58/1 **$2.90**

For PCB, usual 16-pin eurorack connector and 3 10uF caps for power connection. Dual pulse output, input 1 normalled to input 2. 2 of the 4 comparators unused.