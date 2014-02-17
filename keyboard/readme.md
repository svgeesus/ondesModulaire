Teensy++ 2.0-based keyboard scanner for Fatar 49- and 61-key keyboards, with velocity. This is intended for an Ondes Martenot, using a 5 octave keyboard  and +/- 2 octave switching, giving 9 octaves in total. Output is pitch CV and gate, plus velocity (not needed for Ondes Martenot, but generally useful).

For flexibility, separate boards are used for the microcontroler and keyboard matrix, the pitch CV, velocity CV, and the ADC.

1 V/octave pitch CV in the range -2.5V to +7.5V is created with a highly linear, 16-bit SPI DAC (AD5542) and a precision 2.5V reference (AD780).  This generates bipolar +/- 2.5V via U4a. U4b inverts the 2.5V reference. U3b scales the DAC output by 2, giving +/- 5V. U3a is a summing inverter, used to offset the scaled DAC values to give -2.5 to +7.5V. The range -2V to +7V covers nine octaves, with 0V giving the same pitch as with Doepfer keyboards.

A second SPI DAC board, with dual 12bit DAC, will generate two more CVs in the range 0 to 5V. These could be note-on and note-off velocity, or keyboard shake, or other uses.

A 16bit I2C ADC is also planned, to read the Ondes Martenot 'bague'. This will output pitch CV using the same DAC as is used for the keyboard.
