# offsets Eurorack module

Two pitch CV inputs with variable small offset (ultrafine tune) and trimmable 1V/oct gain.

Two untrimmed pich CV inputs,

Switch to null ultrafinee tune, for easy zero offset.

Pitch CV output.

Two sets of pitch CV, with offsets and external CV in, for filters.

## Vref

Use a 6-pin vref board connector for flexibility. +12V, -12V, 5V force, 5V sense, 0v force, 0V sense. Non-kelvin Vrefs can just tie the force and sense together. Allows anything from a cheapo vref to an LM399 board.

### LTLT1236

[LT1236ACN8-5](https://www.mouser.com/ProductDetail/Analog-Devices/LT1236ACN8-5PBF) $7.96/1 A grade 2 ppm/°C 2.5mV error, 20ppm/kHr. But see datasheet fig.G08 _Output Voltage Temperature Drift LT1236-5_

### Vref usage

Inverting plus non-inverting buffers give +5V -5V. Apply across two pots for variable offset voltage. Or is 5V too much? Maybe 3V?

Voltage divider to ultrafine pot, plus larger resistor in input mixer gives maybe +10 to -10mV ultrafine trim (experiment to find useful value) Or wider range with a multiturn pot.

## Op-amps

OPA4192ID 5μV offset, low offset drift (±0.2 µV/°C, typ).

quad, good price/perf tradeoff ($6.25/10).

in TSSOP-14 package. 1/20 inch pin spacing, so easy to hand solder. Needs 8 opamps = 2 quad packages.

### Input gain

Inverting 1.07x 100k input gain stage (2, one per input) = 2 opamps. Voltage divider with trimmer and resistor to bring down to 1V/oct.

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

