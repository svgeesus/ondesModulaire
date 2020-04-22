# Bill of Materials

Transpositeurs v0.1

## ICs, actives

Due to the very small voltages here, offsets are a greater concern so a better specified op-amp makes sense.

- (1) OPA4197ID  ±25μV (typ) ±100μV (max @ 25°C)  Mouser $3.39/10 (IDR version) get 10, use for offsets as well. **$33.90**
- (1) MAX6126AASA30+  0.5mV initial accuracy, 3ppm/°C SOIC-8 Mouser $7.75/1 get 2 **$15.50**
- (1) LTC1658CS8 14bit SPI SOIC-8 $10.27/1 [**GOT**, ordered 13 Sep 2014]

## Passives

Resistor choices highly influenced by actual availability (and low moq). For cheap ones, get several to allow for accidents.

- (1) 35k700 TNPW080535K7BEEN 0.1% 25ppm **$0.92**
- (1) 1k020 RG2012V-1021-P-T1 non-stocked; RN73C2A1K02BTDF 0.1% 10ppm **$0.84**
- (3) 10k Susumu RG2012V-103-P-T1 10k 0.02% 5ppm $2.60/25 [included in offsets order]
- (1) 4k42 Vishay Dale PLTT0805Z4421QGT5 0.02% 5ppm is $7 each! Vishay Dale TNPW08054K42BEEA 0.1% 25ppm **$0.62**
- (1) 9k76 Susumu RG2012N-9761-W-T1 0.05% 10ppm **$1.06**
- (1) 47R Susumu RG2012P-470-D-T5 0.5% 25ppm **$0.22** high tolerance not needed here
- (1) 33R 5% 0.5W Vishay SFR16S0003309JA500 **$0.12**
- (1) 10R 5% 0.25W Vishay CCF0710R0GKE36 **$0.10**

Capacitors non-critical tolerance here, but use C0G; 100nF seem to be 1206 not 0805

- (4) 100n C0G Kemet C1206C104K3GEC7210 25V 100nF 1206 ceramics $0.051/100 = **$5.10** [included in offsets order]
- (1) 33pF 25V C0G C0805C330J3GACTU 0805 $0.14/10 get 10 **$1.40**
- (2) 10μF 25V Nichicon USV1E100MFD  [**GOT**] 5mm diameter!

## Hardware

- (1) Deltron 650-0500 DIN socket, panel mount **$6.38** [**GOT**] look in box to be sure
- (1) 3.5mm jack socket, panel mount [**GOT**]
- (1) twisted-pair, braided screen cable for MIDI
- (1) 2.54mm pitch pin header
- (2) jumpers
- (1) 2x8 Eurorack connector
- (1) 16 to 16 Eurorack power cable
- (6) Shin Chin R13-502MA-05-BB panel-mount momentary pushbutton $4.53/1 **27.18**

## Panels

Front panel (Eurorack-like, 3U but check original tiroir sizing)

Back panel (jacks, 1U)

## PCB

We detected a 2 layer board of 1.17 x 3.96 inches (29.8 x 100.6mm)
3 boards will cost **$23.20**