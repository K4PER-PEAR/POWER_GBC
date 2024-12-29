# POWER_GBC

Power supply designed to be a drop-in replacement for the GameBoy Color (GBC) power supply. 

![Picture of PWA](img_PWA_top.png)

This design was motivated due to obsolescence of components on the GBC power supply making the existing supply unrepairable. A power supply failure would therefore brick the GBC, either requiring acquisition of a functional power supply or use of the motherboard for parts. I have acquired multiple GBCs that have failed power supplies, so this seems to be a common failure point, specifically for the transformer on the supply. 

# Design

Full schematic can be found here: [Schematic](schematic_revC0)

The PWA was designed to use the same footprint as the existing power supply. It is split between two switchmode power ICs that generate the output voltages needed. Both supplies are layed out based on the manufacturers suggestions in the component datasheets. 

Top side: +5V power supply

![Picture of Schematic Top PWA](img_5Vsupply.png)

The +5V supply, which powers the microprocessor and most sensors used by the GBC, is generated by the TI TPS61033 boost converter. The boost converter is biased to +5.5V to allow a following linear regulator to generate the +5V. Most revisions of the board were in this design. 

- The linear regulator is required for stable operation of the processor.
- Do not use part TPS7A2050PDBVR for U5! This part is pin-to-pin compatable, but I had issues with the IC disabling the output in use. I am still working to understand why this was occuring, working theory is that the 47uF on the output generated too much current at start up, causing the current protection circuitry to disable the output.
- Capacitors on this side of the board should be 0805 (as currently designed for) or smaller to prevent interference with the GBC shell. 

Bottom side: LCD power supply

![Picture of Schematic Bottom PWA](img_LCDsupply.png)

The circuitry for the original LCD TFT display found in the GBC requires two higher voltage rails for operation: +13.6V and -15V. I selected the Analog Devices (originally Linear Tech) LT1945 as it is specifically designed for providing such voltages for LCD TFT displays. Note that this is the most expensive component in the BOM. I may revisit this design in the future to reduce component cost, but currently this component has been very reliable as LT components in my experience tend to be. 

# Manufacturing




