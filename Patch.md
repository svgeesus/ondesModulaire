# the Ondes Martenot patch

## Dixie 2

Commercial sine-core oscillator by Intellijel.
Needs accurate tracking over 9 octaves, a pure sine, and a good triangle.

- pitch CV in
- sine out -> mult 1
- tri out -> mult 2

## Mult 1

This is the top half of a dual 4-way passive mult.

- sine in from Dixie
- sine out 1 -> ondesMix O in (Onde)
- sine out 2 -> Precision Rectifier

Optionally, put sine out 1 into a second μVCF whose pitch is 4 octaves above.
Leaves fundamental, second and third harmonics but cuts higher harmonics.

## Mult 2

Bottom half

- tri in from Dixie
- tri out 1 -> Dual Comparator
- tri out 2 -> Optodist

## Dual Comparator

Custom module with dual comparators.

- tri in 1 from mult 2 (Dixie tri out)
- pulse width 1 knob (5%)
- pulse 1 -> ondesMix N in (Nasillard)
- pulse width 2 knob (40%)
- pulse 2 -> mult 3

## Mult 3

Top half of a second  dual 4-way passive mult.

- 45% pulse in from Dual Comparator
- pulse out 1 to ondesMix G in (Gambe)
- pulse out 2 to μVCF

## Optodist

Commercial DIY kit

- tri in from mult 2 (Dixie tri out)
- soft clipping
- out -> ondesMix C in (Creux)

## Precision Rectifier

Custom module for rectification (one level of wavefolding).

- input from mult 1 (Dixie sine)
- offset knob about 2 o'clock
- output -> ondesMix 8 in (Octaviant)

## Offsets

Custom module for pitch CV offset (dual shifted outputs)

- input 1 from pitchCV
- offset knob 1 +5V
- output 1 -> μVCF
- offset knob 2
- output 2

## μVCF

Commercial 12bB/oct clean-sounding filter with good pitch tracking.

- in from mult 3 (40% pulse)
- fm1 from pitch CV offset 1, 5 octave offset
- lpf -> ondesMix g (petit gambe)

## Noise

Commercial noise source from Liivatera. Wide variety of modules suitable here.

pink -> ondesMix S in (Souffle)

## ondesMix

Custom 7-input voltage-controlled mixer. Internally, two
cascaded 4-input mixers so actually needs 8 CVs).

Possibly a need to submix N, C, G g for high-pass phase distortion,
would need a second pitch offset and second, HPF.

- 7 inputs from wave shapers etc
- 8 (balanced) CV inputs o DB-25 connector
- mix output -> VCA for articulation and volume control


## Currently missing

- keyboard with shake (using Roli Seaboard)
- bague (using Roli Seaboard glide)
- touche (using Roli Seaboard aftertouch)
- pins (designed but not yet built)
- soft filter, controlled from tiroir or foot pedal, more of a mellow to sharp tone control
- switching and level controls for the 4 speaker sounds
- palme speaker, or digital emulation of one

