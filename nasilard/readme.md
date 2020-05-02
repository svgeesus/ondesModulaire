# Nasilard pulse maker

Its a pulse wave, where the mark part is of a constant, fixed width regardless of frequency and the space part is whatever is needed for the frequency. So as the frequency increases and thus the wavelength decreases, the proportion of mark to space increases. I assume this will produce formants due to the non-harmonic nature of the pulse?

Also, how would you shape this in the analog domain, given a triangle wave input? I assume the circuit would trigger on a rising zero transition, generate the positive pulse, then go low until the next trigger.

(For the curious, this is the Nasillard waveform on an ondes Martenot, which I thought was a fixed 4% mark-space waveform because I only looked at a single frequency. I just discovered that it is not).

2890Hz (and multiples) formants. so 2,890^-1 / 2 = 1.73010380622837E-4 = 173μs pulse

> comparator, then monostable

## 74HCT221 dual retriggerable monostable multivibrator with reset

- B input triggers on voltage level (2V for high) independent of rise time.
- Pulse width = 0.7 C R, 2k < R < 100k.
- 5V rail (4.5 to 5.5)
- SOIC-16 only. Breadboard with a DIP adaptor.

1.73010380622837E-4 / 0.7 / 10,000 = 2.47157686604053E-8 = 24.7nF for 10k
closest is 22nF so R = 1.73010380622837E-4 / 0.7 / 2.2E-8
= 11,234.4403001842 = 11.23kHz. Closest E96 is 11.5k

Vishay / Roederstein MKP1837322161 polypropylene 5mm spacing 1% $1.13/1 7.5x5.5mm case

Also see 12.1   Power-down considerations for protection circuit (Schottky diode across Rext)

Texas CD74HCT221E PDIP $0.77/1