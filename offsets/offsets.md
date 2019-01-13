# offsets Eurorack module

Two pitch CV inputs with variable small offset (ultrafine tune) and trimmable 1V/oct gain.

Two untrimmed pich CV inputs,

Switch to null ultrafine tune, for easy zero offset.

Pitch CV output.

Two sets of pitch CV, with offsets and external CV in, for filters.

## Vref

Use a 6-pin vref board connector for flexibility. +12V, -12V, 5V force, 5V sense, 0v force, 0V sense. Non-kelvin Vrefs can just tie the force and sense together. Allows anything from a cheapo vref to an LM399 board.

### LTLT1236

[LT1236ACN8-5](https://www.mouser.com/ProductDetail/Analog-Devices/LT1236ACN8-5PBF) $7.96/1 A grade 2 ppm/°C 2.5mV error, 20ppm/kHr. But see datasheet fig.G08 _Output Voltage Temperature Drift LT1236-5_

Probably good enough in this appplication, but vref socket allows upgrading if needed.

### Vref usage

Inverting plus non-inverting buffers give +5V -5V. Apply across two pots for variable offset voltage. Or is 5V too much? Maybe 3V?

Voltage divider to ultrafine pot, plus larger resistor in input mixer gives maybe +10 to -10mV ultrafine trim (experiment to find useful value) Or wider range with a multiturn pot.

## Op-amps

OPA4192ID 5μV (typ) offset, low offset drift (±0.2 µV/°C, typ).

quad, good price/perf tradeoff ($6.25/10).

in TSSOP-14 package. 1/20 inch pin spacing, so easy to hand solder. Needs 12 opamps = 3 quad packages.

## Resistors

Avoid quad packs, as they are only pairwise matched. Go for single low tempco 0.1% resistors and do any additional matching (the two untrimmed CV inputs vs. the mixer gain resistor is the critical point).

28 of 100k 0.1% 5ppm/C
2 of 105k 1% or better 10ppm/C or better
2 of 70k  1% or better 10ppm/C or better (but check tempco of trimmer)
3 of 330R 1%  20ppm/C


### 100k close tolerance

#### Vishay TNPU0805100KBZEN00

Close tolerance 0805 0.1% resistors.

0.1% 5ppm/C  0.1%/8kHr  $2.50/1 $2.07/25

### Other value resistors

#### Susumu RG2012N-1053-D-T5

105k 0805

0.5% 10ppm/C $0.77/1 $0.66/10

#### Susumu RG2012N-6982-D-T5

69.8k 0805

Non stocked!! Min 5000!!

#### Susumu RG2012N-6812-D-T5

68.1k 0805

0.5% 10ppm/C $0.77/1 $0.66/10

#### Susumu RR1220P-331-D

330R 0805

0.5% 25ppm/C  $0.10/1 $0.085/10


### Input gain

Inverting 1.07x 100k input gain stage (2, one per input) = 2 opamps. Voltage divider with trimmer and resistor to bring down to 1V/oct. 7% was from Dave Jones buffered mult design.

Maybe ±7% adjustment range is too much. 1k output impedance into 4-way passive mult into 4 100k inputs (1k out to 25k in) is -3.8% drop, requiring a 4% compensating boost. Mostly, errors will be a drop not an increase. So an adjustment range of +5% to -2% seems better. Implies an input gain of 5% (use 100k and 105k resistors). With a 5k trimmer, 98 * 5 / 7 = 70k resistor to ground.

E96 value is 69.8k. However Mouser doesn't carry it (min order 5k, non-stocked) but they do have 68.1k. With a 5k trimmer, range is +5% to  105 * 68.1 / ( 68.1 + 5 ) = 97.818 = -2%.


### Vref buffer

One non-inverting unity and one inverting unity for + and - Vref = 2 op-amps.

### Mixers

One inverting mixer for inputs one to four plus  ultrafine offset. Mixer is also the output stage = 1 op-amp.

Two inverting mixers for the two offset stages (pitch CV, ext input). BUT output from the first mixing stage needs to be inverted first = 3 op-amps. And Ext CV also, = 5 op-amps (CV in adds a dual).

### Output stages

None, just straight to the jacks. Single output jacks, can use passive mut if more needed.

## Resistors

Balance of quality (tolerance, drift) and cost. Avoid pricy quad-packs. 0805 size for ease of hand soldering.

Yaego RT0805BRB07100KL 100k 0.1% 10ppm/C thin film, 0805 package.

$0.95/1, $0.682/10, $0.387/100.

Gain trimmers just below ultrafine pot, PC mount.

## Ultrafine control

10-turn Vishay [534B1104JC](https://www.mouser.com/ProductDetail/Vishay-Spectrol/534B1104JC) or Bourns [3590S-4-104L](https://www.mouser.com/ProductDetail/Bourns/3590S-4-104L) panel-mount wirewound or (preferably) plastic/hybrid 100k pot for ultrafine. Probably makes the panel 6HP rather than 4. However Mouser seems to have only wirewound in single-unit quantities; hybriton is MOQ 25.

### 3590 10-turn pot

-4 means sealed, metal bushing, metal shaft, solder lug connectors. $22.03/1.

2.46 to 3.81mm panel, so needs a washer.

10.44  ± .07mm mounting hole. 6.34mm ( (.2497 inch + .0000, - .0009) shaft

22.22mm ± .38 (.875 inch ±.015) diameter = 4.37HP so needs 5 or 6HP. Free panel mounted with wire connections, not PCB.

Tempco ±50 ppm/°C, but ratiometric so should not matter.

### 534B1104JC

$25.17/1.

20 ppm/°C is better than the Bourns, but likely does not matter.

0.875 inch (22.22mm) diameter.

## Offset controls

For the offsets, perhas a regular alpha pot plus a dpdt switch (like C&K [7201SYCQE](https://www.mouser.com/ProductDetail/CK/7201SYCQE)) to go between positive and negative polarity?

Jacks at the bottom of the panel.

## Panel

Large multiturn pot at top of panel, panel mount not PCB.

Below that, tucked in the corners, two front-acessible PCB mount gain trimmers.

Switch to enable/disable ultrafine?

Pot for filter1 plus polarity switch.

Polarity switch for filter2 plus pot.

Jacks:

| PCV1 | PCV2 | PCV3 |
|--|--|--|
| Fin1 | PCV4 | Fin2 |
| Fout1 | Pitch | Fout2 |

## PCB

### Front (Jack and pot) PCB

Avoid flying leads, use a PCB for panel-mounted jacks, pots, trimmers and switches with 0.1" connectors to the rear (electronics) PCB which sits behind it. Panel mount the multiturn wirewound put and provide a circular arc cutout on the front PCB to clear this large pot. The resistive dividers for the ultrafine tune could also conveniently sit here.

### Rear (electronics) PCB

Contains the Eurorack power connector, reverse voltage protection, power filtering. Has the op-amps, resistors and caps. Keep input resistors close to the summing inputs. General layout has input signals on the left, fed from input jacks (6 op amps = 3 halves of 3 quad packages) then the vref buffering/inversion (2 op amps), cv mixing and re-inversion (2 op-amps) and filter cv mixing (2 op-amps).

### Vref PCB

Small, upgradable Vref PCB which takes in a filtered +12V, -12V from the main PCB, houses the Vref chip and any caps, resistors or trimmers that needs and outputs 0V and Vref with both force and sense lines. If the Vref does not provide force and sense, connct them. If the destination does not use force and sense, connect them. Use a standard connector for all future modules that use Vrefs.

### Board connections

Left

- gnd
- cv1buff
- cv3buff
- pcv1
- pcv3
- gnd
- pcv2
- pcv4
- gnd
- fin1
- fin2
- gnd

Right

- gnd
- uftune
- vref+
- vref-
- cvout
- foffs1
- foffs2
- fout2
- fout1
- gnd

Vref

- 0VS
- 0vF
- +12V
- -12V
- VrefF
- VrefS

Top of front board

- divided-down Vref+
- uftune (wiper)
- divided down Vref-

