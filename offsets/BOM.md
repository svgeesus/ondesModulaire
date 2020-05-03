# Bill of Materials

offsets v0.1

I'm first builing a low-cost version for design verification. Build first to ensure circuit works, before blowing a lot of expensive precision resistors on an unproven design. Then (after measuring performance, and if it is okay apart from gain errors) build a high-accuracy version of the rear PCB, with better resistors.  Front PCB, and front panel, is the same. Can re-use Vref board also.

"(x:2x)" means these components are the same for low cost and high-cost versions. You need only x of them if building just one version.

"get x" means what I plan to order for the first prototype, taking into account quantity price breaks and my estimate of my likelihood of using the same component in the future.

## ICs, actives

Both versions will use OPA4172, because the ±200μV (typ) op-amp offsets are mostly swamped by oscillator coarse/fine tune and then the 50mV variable offsets from ultrafine, or 5V from filter offset. Gain is **much** more critical than op-amp offset here. For low quality version maybe use SOIC TL074 even.

- (1:2) LT1236ACN8-5 Mouser $9.07/1 get 2 = **$18.14**
- (3:6) OPA4172ID Mouser $2.84/10 get 10 = **$28.40** but no, use OPA4197ID same as transpositeurs
- (2:4) 1N5817B (already got)

**$44.32** for actives

## Passives

Over-ordering on commonly-used 10k and 100k resistors for use in other projects, will be left with around 80 of each.

These are the low-accuracy resistors (only needed for design verification) but useful for other projects.

- (12) Susumu RG2012N-104-D-T5 100k 0.5% Mouser $0.77/10 $0.267/100 get 100? (check what hi-cost version needs) = **$26.70**
- (18) Susumu RG2012N-103-D-T5 10k 0.5% Mouser $0.77/10 $0.267/100 get 25 = $16.50 or 100 for **$26.70**

Definitely needed high-accuracy resistors! *And critical 100k pairs need to be matched closer.*

- (12) Susumu RG2012N-104-W-T1 100k 0.05%  10ppm 0.768/25 = *$19.20*
- (18) Susumu RG2012V-103-P-T1 10k 0.02% 5ppm $2.57/25 = **$64.25**

Then (these are the same for low cost and high accuracy versions):

- (2:4) Susumu RG2012N-1053-D-T5 105k 0.5% $0.66/10 get 10 = **$6.80**
- (2:4) Susumu RG2012N-6812-D-T5 68k1 0.5% $0.66/10 get 10 = **$6.80**
- (3:6) Susumu RR1220P-331-D 330R 0.5% $0.085/10 $0.035/100 get 100? = **$3.50**
- (2:4) Susumu RG2012N-102-D-T5  1k 0.5% $0.66/10 get 10 = **$6.60**
- (2:4) Susumu RG2012N-222-D-T5   2k2 0.5% $0.66/10 get 10 (in case 1k/100k = 50mV is too small)? = **$6.60**
- (1:2) Susumu RR1220P-105-D 1Meg $0.085/10 get 10 = **$0.85**
- (2:4) Bourns 3296W-1-502LF $1.90/10 get 10 = **$19.00**
- (1:2) Bourns 3590S-4-104L  $22.03/1 get 2 = **$22.03** _NO only needed if making a trimmable vref_
- (2:4) 22uF 25V or better electros (already got)
- (6:12) Kemet C1206C104K3GEC7210 25V 100nF 1206 ceramics $0.051/100 = **$5.10**
- (3:6) Kemet C0805C330J3GACTU 33pF 0805 C0G $0.125/10 = **$1.25** got 20

**$215.18** for passives.

## Hardware

- (1) 10-pin Euro power [**GOT**]
- (1) power cable, 10-16 Pin (Long - 25cm), [**GOT**] Thonk £1.59/1 = **£1.59**
- (2:4) 12-pin 0.1" socket Amphenol 76308-112LF 12-pos $3.83/1 got 4
- (2:4) 12-pin 0.1" plug Amphenol 10129378-936002BLF 36-pin $1.00/1
- (1) assorted 0.1" pin strip, for the Vref and multi-turn pot connections. JST connectors could also be used.
- (1) 0.1" pin socket, ideally 90-degree for the Vref connection, cable mount for the pot connection
- (2) DW4 - DPDT ON-OFF-ON, Thonk £1.33/1 = **£2.66** get 4
- (2) VERTICAL: B10K - 10K Linear Alpha pots, Thonk £1.42/1 = **£2.84** get 2 more, to be sure
- (9) Thonkikon PJ398SM jacks (or older PJ301M-12, same footprint) Thonk £0.40/1 =  **£3.60** (already got)
- (9) Knurled nuts or hex nuts as desired, Thonk £1.50/50 (already got)
- (9) Washers, Thonk £1.50/50 (already got)
- (1) ‘Erica Synths’ style Knobs – 6.35mm Shaft, Large Black, Thonk £0.70/1 = **£0.70**
- (2) Davies 1900h Clone – 6.35mm Round Shaft, Black, Thonk £0.70/1 = **£2.40**

## PCB

**$55.65** (for 3) for PCB

Vref PCB is just a DIP socket on a scrap of veroboard, plus connectors to the main board. Only use a single gnd connection point.

## Panel

**$72.49** for panel

## Order status

OSH Park order Jan 27 2019 **pcb's arrived**

FrontPanel Express order Feb 11 2019 **panel arrived**

Thonk order Feb 15 2019 **arrived**

Mouser order _not yet made_
