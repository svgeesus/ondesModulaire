# Bill of Materials

offsets v0.1

First build a low-cost version for design verification. Build first to ensure circuit works, before blowing a lot of expensive precision resistors on an unproven design. (x:2x) means same for low cost and high-cost versions. Then (if it is okay apart from gain errors) build a high-accuracy version of the rear PCB, with better resistors.  Front PCB, and front panel, is the same. Can re-use Vref board also.

## ICs, actives

Both versions will use OPA4172, because offsets are mostly swamped by oscillator coarse/fine tune and then the 50mV variable offsets from ultrafine, or 5V from filter offset. Gain is much more critical than offset here.

- (1:2) LT1236ACN8-5 Mouser $7.96/1 get 2 = **$15.92**
- (3:6) OPA4172ID Mouser $2.84/10 get 10 = **$29.40**
- (2:4) 1N5817B (already got)

## Passives

Over-ordering on commonly-used 10k and 100k resistors for use in other projects, will be left with around 80 of each.

These are the low-accuracy resistors (only needed for design verification)

- (12) Susumu RG2012N-104-D-T5 100k 0.5% Mouser $0.66/10 $0.267/100 get 20? (check what hi-cost version needs) = **$26.70**
- (18) Susumu RG2012N-103-D-T5 10k 0.5% Mouser $0.66/10 $0.267/100 get 25 = $16.50 or 100 for **$26.70**

Definitely needed high-accuracy resistors! *And critical 100k pairs need to be matched closer.*

- (12) Susumu RG2012N-104-W-T1 100k 0.05%  10ppm 0.753/25 = *$18.25*
- (18) Susumu RG2012V-103-P-T1 10k 0.01% 50ppm $2.60/25 = **$65.00**

Then (these are the same for low cost and high accuracy versions):

- (2:4) Susumu RG2012N-1053-D-T5 105k 0.5% $0.66/10 get 10 = **$6.80**
- (2:4) Susumu RG2012N-6812-D-T5 68k1 0.5% $0.66/10 get 10 = **$6.80**
- (3:6) Susumu RR1220P-331-D 330R 0.5% $0.085/10 $0.035/100 get 100? = **$3.50**
- (2:4) Susumu RG2012N-102-D-T5  1k 0.5% $0.66/10 get 10 = **$6.60**
- (2:4) Susumu RG2012N-222-D-T5   2k2 0.5% $0.66/10 get 10 (in case 1k/100k = 50mV is too small)? = **$6.60**
- (1:2) Susumu RR1220P-105-D 1Meg $0.085/10 get 10 = **$0.85**
- (2:4) Bourns 3296W-1-502LF $1.90/10 get 10 = **$19.00**
- (1:2) Bourns 3590S-4-104L  $22.03/1 get 2 = **$22.03**
- (2:4) 22uF 25V or better electros (already got)
- (6:12) Kemet C1206C104K3GEC7210 25V 100nF 1206 ceramics $0.051/100 = **$5.10**
- (3:6) Kemet C0805C330J3GACTU 33pF 0805 C0G $0.125/10 = **$1.25**

## Hardware

- (1) 10-pin Euro power,
- (1) 10-16 Pin (Long - 25cm), Thonk £1.59/1 = **£1.59**
- (2:4) 12-pin 0.1" socket
- (2:4) 12-pin 0.1" plug
- (1) assorted 0.1" pin strip
- (2) DW4 - DPDT ON-OFF-ON, Thonk £1.33/1 = **£2.66** get 4
- (2) VERTICAL: B10K - 10K Linear Alpha pots, Thonk £1.42/1 = **£2.84** get 2 more, to be sure
- (9) Thonkikon PJ398SM jacks (or older PJ301M-12, same footprint) Thonk £0.40/1 =  **£3.60** (already got)
- (9) Knurled nuts or hex nuts as desired, Thonk £1.50/50 (already got)
- (9) Washers, Thonk £1.50/50 (already got)
- (1) ‘Erica Synths’ style Knobs – 6.35mm Shaft, Large Black, Thonk £0.70/1 = **£0.70**
- (2) Davies 1900h Clone – 6.35mm Round Shaft, Black, Thonk £0.70/1 = **£2.40**