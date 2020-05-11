# Nasilard pulse maker

Its a pulse wave, where the mark part is of a constant, fixed width regardless of frequency and the space part is whatever is needed for the frequency. So as the frequency increases and thus the wavelength decreases, the proportion of mark to space increases. I assume this will produce formants due to the non-harmonic nature of the pulse?

Also, how would you shape this in the analog domain, given a triangle wave input? I assume the circuit would trigger on a rising zero transition, generate the positive pulse, then go low until the next trigger.

(For the curious, this is the Nasillard waveform on an ondes Martenot, which I thought was a fixed 4% mark-space waveform because I only looked at a single frequency. I just discovered that it is not).

2890Hz (and multiples) formants. so 2,890^-1 / 2 = 1.73010380622837E-4 = 173μs pulse

TODO check again the pulse width and dfferent audio frequencies.

> comparator, then monostable

"The inputs to an LM339 can not go beyond their supply pins. If it is powered off of +12v and ground then it's inputs must stay within that range."

"The output of the LM339 is open collector, so requires a pull-up resistor on it's output . It's output voltage goes down to the ground (minus power) pin voltage and goes up to whatever voltage you have the pull-up resistor tied to.

So if it is powered from ground and +12v, and the pull-up is tied to +12v, then the output will go between ground and +12v. Since it's open collector you can tie the pull-up to a different voltage than the positive supply (but it must be more positive than the ground/negative supply pin). So you could power it from +12v and have the pull-up tied to +5v, giving a zero to +5v output. Or power the chip on +5v and have the pullup tied to +12v, giving a zero to +12v output.

Unlike many other comparators, the LM339 can be powered off of large supplies. So it could be powered off of +/-12v or +/-15v and then the input and output would both be bipolar."

## 74HCT221 dual retriggerable monostable multivibrator with reset

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

## LM339 comparator

Run on +12 -12 to allow all possible input voltages. Needs wo 100n bypass caps, from +12 to GND and -12 to GND.
Uh, and this is a quad but we don't need a window so a dual would be better.

Open-collector output pulled up to +5V to feed the 74HCT221

LM339AN is PDIP-14, LM339AD is SOIC-14

For breadboarding, Vref of 2V5 from 1/2 5V rail is enough.

For rising/falling, see [CGS slope detector](https://www.elby-designs.com/webtek/cgs/cgs62/cgs62_sd.html).
The same signal is fed to both inputs of the comparator, but the negative input is fed by a 2k2 - 1M voltage divider to -12V to pull it low. The positive input is fed by an RC network with R = 10k + 1M trimmer, and C = 100n to ground. A rising voltage will be delayed by the RC circuit and rise slower, triggering the comparator. (That circuit assumes the next stage is inverting, so experiment and swap as needed).

## BOM for breadboarding

All through hole, assume enough general resistors, 100n decoupling caps. Buy timing resistor and cap. Assume a general op-amp for output buffer?

- LM339AN * 4 $0.53/1 **$2.12**
- CD74HCT221E * 4 $0.77/1 **$3.08**
- MKP1837322161 * 2 (may well be wrong value) $1.07/1 **$2.14**
- 11.5k 0.1% 15ppm/C YR1B11K5CC  * 5 $0.58/1 **$2.90**

For PCB, usual 16-pin eurorack connector and 3 10uF caps for power connection. Dual pulse output, input 1 normalled to input 2. 2 of the 4 comparators unused.