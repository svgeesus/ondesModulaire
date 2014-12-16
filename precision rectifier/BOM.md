# Precision Rectifier BOM

## Semiconductors

*U1* 	REF195GPZ (medium quality voltage reference)

*IC1*	OPA2134PA (do not substitute 072)

*IC2,3*	TL072P (any grade is fine)

*D1, D2*	1N4148 or similar high-speed signal diodes

## Capacitors

*C1, C2, C3, C5, C8, C9, C11*
	100nF (0.1μF) MLCC ceramic, decoupling capacitor. 
	50V or so is fine. 2.5mm pitch.

*C4*	47pF film (ceramic works too in a pinch)

*C6, C7*	10μF to 22μF 35V or higher electrolytic. 
	Polarity matters

*C10*	1μF film

## Resistors

*R1, R2, R3
	100kΩ 0.1% metal film (app note says to use closely 
	matched values hence 0.1%)

*R4, R5, R6, R7, R9, R10, R11, R13*
	100kΩ 1% metal film

*VR1*	100kΩ linear, Alpha or BI 9mm right-angled pot

## Hardware

*U1, U2, U3*
	[Thonk PJ302M right-angled PCB mount mono 3.5mm jack] (http://www.thonk.co.uk/shop/pj302m/)

*IC sockets*
	four 8pin DIL sockets (or solder ICs directly if you want)

*Euro*
	2x5 pin Eurorack pin connector, 2.54mm pitch
	pin1 is -12V, PCB has -12V red stripe marking also

*power cable*
	Eurorack 10pin to 16pin ribbon cable, red stripe to -12V

*pcb*	See offset_rectifier.brd for Eagle file, 
	front.png and back.png for this board [made by OSH Park] (https://oshpark.com/shared_projects/KNj1dFOE)

*panel*	See precision_rectifier.fpd for Schaeffer/Front Panel Express file

*knob*	Your choice of knob to fit the pot you are using.
	I used [Davies 1911 clone from Thonk] (http://www.thonk.co.uk/shop/knobs-davies-1900h-clone-metal/)

## Construction

Start with the resistors, noting the three close-tolerance ones. Then the small caps, 
diodes (noting the orientation of the diodes, as marked on PCB),
and IC sockets. Add the Euro connector and electrolytic caps, checking orientation:
negative side has a stripe, positive side has a longer leg. 

Without soldering, fit the three jacks and the pot and then put on the front panel, loosely 
bolting the pot and one of the jacks. Now solder the pot and jacks.

With a voltmeter, check for shorts across -12V to GND and GND to +12V.
Bend the pins on the ICs so they are at right angles rather than splayed out.
Fit the op-amps and voltage reference, lastly the power cable.
Check again for power rail shorts.

**Check the orientation of the power cable. This module does not have 
reverse voltage protection.**

Power up the module. 

**Note that this module is DC coupled and typically has a 2.5V DC offset
** *this lets you rectify CVs*
With a voltmeter, check that there is +5.00V on pin 6 of the voltage reference.
Check that the voltage on the central pin of the pot swings between -5V and +5V 
as the pot is turned.

With a sine or triangle into the input, no CV in, and the pot 
in the center position you will hear the octave doubling. This is also clearly 
visible on a scope if you have one.

Moving the pot, or adding a CV (+/- 5V) affects the fold position so the 
folded wave is asymmetric (alternating large and small peaks).