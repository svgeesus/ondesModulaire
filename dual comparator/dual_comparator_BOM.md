# Dual Comparator BOM

## Resistors

Generic 1% metal film, no particular requirements for tempco or precision.

- 47R * 2
- 47k *2
- 49k9 * 2
- 10k * 4
- 15k * 2
- 1M0 * 2
- 5k trimmer * 2 (Bourns 3296)
- 100k lin 9mm pot * 3 (Alpha, etc)

## Capacitors

Oordinary decoupling caps and electrolytics.

- 100nF ceramic, 2.5mm * 7
- 1uF ceramic, 5mm * 1
- 22uF 25V electrolytic * 2

## Semiconductors

Mostly generic. However, the op-amp used as comparator needs to be able to recover fast from overload, since it is used without negative feedback and constantly driven into the rails. The LT1213 copes with this while a TL072 would not.

- 1N5817 * 2
- TL074CP * 1
- TL072CP * 1
- LT1213 * 1
- REF195GPZ * 1

## Etc

I socketed the op-amps and voltage reference, up to you. The jacks are panel mount so use whatever you have, no particular PCB footprint although they are fairly closely clustered on the panel.

- 3.5mm jacks * 6
- euro power conn. 10pin * 1
- 8pin DIP socket * 3
- 14pin DIP socket * 1

## PCB

![top](images/top.png)

[Shared on OSH Park](https://oshpark.com/shared_projects/FYjulcN6)

osh:  $22.95 for three.
ordered 07 Mar 2015
