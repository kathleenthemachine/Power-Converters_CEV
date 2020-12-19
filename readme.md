# Power Converters 2020-21
by Eric Kahn, Kathleen Wang

[Project Repository](https://github.coecis.cornell.edu/Resistance-Racing/Power_Converters_20_21)
+ [Summary](#Summary)
  - [System Description](#system-description)
+ [Research and Requirements](#research-requirements)
  - [Background Research](#background-research)
  - [Key Parameters](#key-parameters)
  - [Terminology](#terminology)
  - [Potential and Selected Designs](#potential-designs)
+ [12V Buck Converter (Eric)](#12VEric)
  - [Design Overview](#12Vdesign-overviewEric)
  - [Detailed Design](#12Vdetailed-designEric)
  - [Component Selection](#12Vcomponent-selectionEric)
+ [12V Buck Converter (Kathleen)](#12VKathleen)
  - [Design Overview](#12Vdesign-overviewKathleen)
  - [Detailed Design](#12Vdetailed-designKathleen)
+ [5V Buck Converter](#5V)
  - [Design Overview](#5Vdesign-overview)
  - [Detailed Design](#5Vdetailed-design)
+ [Mounting and Packaging](#mounting-packaging)  
+ [Bill of Materials](#BOM)
+ [Manufacturing/Testing Plan](#manufacturing-plan)
+ [Project Reflection and Future Work](#project-reflection)
+ [References](#references)
## Summary
### System Description <a name="system-description"></a>
Our power converters are used to convert the voltage from our 24V Lipo battery down to lower voltages for other subsystems of the car at their specified current levels. The design of these efficient DC-DC converters must also take into account, among other things, the ability to regulate voltage, the ability to operate over various input voltages from 22-26V, the size/weight of the board, the cost of the components, the isolation provided, and the voltage/current ripple on the output. We would like these converters to operate with an efficiency greater than commercially available options (and hopefully at a lower cost). 

## Research and Requirements <a name="research-requirements"></a>  
### Background Research <a name="background-research"></a> 
Background research mainly involved knowledge acquired from ECE 4560: Power Electronics. Ask Kathleen, Eric, or Robby if you want the slides from that class in order to learn the material. You should know the basics of what a switching converter is and also how a buck converter, boost converter, and flyback converter work.  

For a brief background, a very basic DC-DC converter would be a voltage divider. However, due to the fact that you are essentially burning power through one of your resistors, these are extremely simple and cheap, have poor efficiency, have poor isolation, and do not work for variable inputs. 
![Voltage divider](img/volt_divider.png)

Additionally, there are linear regulators where you can think of the regulating device as being made to act like a variable resistor. You continuously adjusts a voltage divider network needed to maintain an output voltage. 
![Linear regulator](img/linear_regulator.png)

In terms of linear regulators vs switching regulators, we can compare them as shown below:
| Linear regulators | Switching regulators |
| -------- | ------- |
| Simple | More complicated |
| Cheap |  More expensive |
| Responds quickly to changes in load voltage |  Might respond slower |
| No switching noise | Switching noise| 
| Can only step down voltage| Can step down/step up voltages depending on topology|
| NOT EFFICIENT :(( | Much more efficient! | 

Switching converters are much more efficient than linear regulators, and some are able to increase as well as decrease voltage. They convert one DC voltage level to another by storing the input energy temporarily in either inductors, transformers, and capacitors, and releasing this energy to the output at a different voltage.

Buck converters are one of the simplest switching topologies and can decrease voltage. Flyback converters utilize a transformer and can increase or decrease voltage.
![Buck flyback](img/buck_flyback.png)

Most of our converters are buck converters because our batteries operate at 24V and all of our boards operate at less than 24V. In addition, buck converters are one of the simplest designs and can be highly efficient. However, we may use a flyback converter for our high power electronics such as the Jetson and Xavier instead of a buck converter. Flyback converters use a transformer to help control the output voltage and current. In addition, the transformer allows for galvanic isolation between the batteries and the electronics. If the battery was to explode, the other side of the transformer would be somewhat protected because it is not directly connected. The downside of a flyback converter is that it is more complex to design because it requires us to choose a transformer or a core that we can wrap wire around to create our own transformer. Choosing a core or transformer becomes a very complex process when trying to optimize efficiency.


### Key Parameters <a name="key-parameters"></a>  
Each converter has certain requirements for their output voltage and max currents as specified below:
| Voltage | Subsystems | Current | Ripple |
| ---- | ------- | --- | ---- |
|24V → 5V | BMS, DAQ, MC | Low | 3% |
|24V → 5V | USB Hubs | Up to 0.9A for each USB 3.0 port | 5% |
|24V → 5V | Automation | 1-3 A (TBD) | TBD |
|5V → 3.3V | Sensors | Low | 3-5% |
|24V → 12V | Horn | 6A | Can be medium-high |
|24V → 19V | Jetson/Xavier | ~9A | 3-5% |
|24V → TBD | Lighting/safety system | TBD | TBD |

Most of the converters work with the 24V from the battery and convert it down to a lower voltage. The one converter that does not do this is the 5V -> 3.3V converter that takes in the output of the 24V -> 5V converter. 

### Terminology <a name="terminology"></a>  
- Buck regulator: switching converter that only steps down voltage. 
- Capacitor: component that acts like an open circuit in DC and a short circuit in AC mode. Used for filtering ripples in voltage.
- FET: field effect transistor, can be used as an imperfect electrical switch
- Inductor: component that acts like a short circuit in DC and an open circuit in AC mode. Used for filtering ripples in current.
- Linear regulator: converter that steps down voltage by burning power through a resistor
- IC: integrated circuit, semiconductor circuit that performs some concentrated task in a small area
- PCB: printed circuit board
- Transformer: passive electrical component that converts electrical energy from one value to another. Operates on the principles of electromagnetic induction in the form of mutual induction. 

### Previous and Potential Designs <a name="potential-designs"></a>  
In terms of previous converters, Logan designed a buck converter for the 12V output and a flyback converter for the 5v output. The converters didn’t work ideally because of a problem he had with a comparator in his design.
Leo also designed a buck converter for the 5V output which works, though only for small-medium currents. Logan's advice was to buy an IC that could handle the control loop. It would make the design much easier as well as the cheapest, smallest, most customizable option which would still be capable of delivering large amounts of power reliably and very efficiently. 

For the reasons stated in the Background Research section and also from Logan's advice on choosing an IC that takes care of the control loop, both of us have chosen to go with using buck regulator ICs for most of our converters. These allow for customization based on the output current & output current ripple, the input voltage range, the output voltage and its peak-to-peak voltage, as well as other factors such as the switching frequency.

## 12V Buck Converter (Eric) <a name="12VEric"></a> 

### Design Overview <a name="12Vdesign-overviewEric"></a>

### Detailed Design (Schematic & Layout) <a name="12Vdetailed-designEric"></a>

### Component Selection <a name="12Vcomponent-selectionEric"></a>


## 12V Buck Converter (Kathleen) <a name="12VKathleen"></a> 

### Design Overview <a name="12Vdesign-overviewKathleen"></a>
![12V Schematic - K](img/04.png)
I ended up selecting the LM3150 as my buck controller since it was an IC that was capable of providing up to 12A of output current in a typical application (more than enough for the 6A the horn needed). Additionally, I selected a controller that operated with an input voltage ranging from 6-42V and had an adjustable output voltage that could be configured to 12V, along with an adjustable switching frequency ranging from 0.1-1 MHz.

I chose a switching frequency of 0.288MHz as well as parameters of a 22-26V input voltage, a 12V output voltage, and a ~8A max output current level. The output voltage could be set by two external resistors (how to calculate them is shown below), and the IC also had features such as a regulation comparator, an overvoltage comparator, and current limit detection that could be set through an external resistor Rlim. This IC also required the use of two external FETs for my switching waveform (which is more efficient than simply using a diode and a MOSFET, though it is more expensive). There are high-side and low-side gate control signals for the switches. 

### Detailed Design - Schematic <a name="12Vdetailed-designedKathleen"></a>

![12V Schematic - K](img/kathleen_12Vschematic.PNG)

In terms of the individual values of the components connected to the IC, these could be calculated according to the datasheet for my IC. To properly size the components for the application, you need the following parameters: the input voltage range (22-26V), the output voltage (12V), the typical output current (6A), the max output current (8A), and the required switching frequency (288 KHz).

I will now go through the most important parts of the selection process and calculations for the components.

#### Calculation 1 - Feedback resistors
The first step is to pick the two external feedback resistors (Rfb1 and Rfb2 in the schematic) that allow you to set the output voltage by connecting the node in the middle of the feedback resistor divider to the FB pin (Pin 4), between the output and ground. This is internally connected to the regulation, voltage, and short-circuit comparators with a setting of 0.6V at the pin.

  - I first chose a standard resistance of 10 kOhms for Rfb1. I then used Rfb2 = Rfb1 (Vout/Vfb - 1) to find Rfb2 = 191 kOhms. 

#### Calculation 2 - Ron and Switching frequency
The next step was then to determine Ron and fs. The available frequency range for a given input voltage range was determined by the duty cycle D (since D = Vout/Vin in a buck converter) as well as the minimum ton and toff times of the IC. 

  - Dmin = Vout/Vin_max = 12V/26V = 0.4615

  - fsmax = Dmin / 200 ns = 0.4615 / 200 ns = 2.308 MHz

  - Dmax = Vout/Vin_min = 12V/22V = 0.54545

  - toff = (1 - Dmax) / fs_max = (1-0.5454) / 2308000 = 197 ns

  - toff should meet the following criteria: toff > 725 ns

  - At the maximum switching frequency of 2.308 MHz, which is limited by the minimum on-time, the off-time of 197 ns is less than 725 ns. Therefore the switching frequency should be reduced and meet the following criteria: fs < (1 - Dmax) / 725 ns = 752 kHz. I chose 288 kHz since this allowed for reasonably sized components and was also under the required frequency. 

  - I could then set the high-side switch time using Ron, where Ron = [(Vout x Vin) - Vout] / (Vin x K x fs) + Rgnd where Rgnd = - [(Vin - 1) x (Vin x 16.5 + 100)] - 1000. This results in Ron = 274 kOhm. 

#### Calculation 3 - Inductor
Inductor: chose a 8.6uH one (the 7443630860) according to the nomograph giving by the datasheet. This was also rated for the voltage and was also rated for 17A (sufficient for the current drawn by the horn). It is also higher than the nominal current to account for the peak-to-peak current ripple). 

  I could definitely have sized down the inductor while also maintaining the specs as shown above, since the horn could have a decent amount of noise. Part of the reason I did not was due to the lack of knowledge about the Altium Library Loader since other inductor footprint options were not present in the Altium vault. With the introduction of this library loader, many more options are open and easy to drop into your PCB designs.

#### Calculation 4 - Cff
I also chose a feed-through capacitor at the output of the inductor (and at the top node of the feedback resistor divider) in order to provide more stability and reduce the output capacitance. 

  - Cff = Vout/(Vin_min x fs x Zfb) where Zfb = (Rfb1 x Rfb2) / (Rfb1 + Rfb2) = 270 pF 

#### Calculation 5 - FETs and Rlim
MOSFETS: The high-side and low-side FETs must have a VDS rating of at least 1.2 x Vin = 31.2 V. The FETs chosen were the FDD8647L’s, which were N-channel MOSFETs rated at 40V and 14A. 

  - I checked the primary loss in the low-side MOSFET from conduction loss to be given by: Pdl = Iout x Rds(on) x (1-D) = 6 x 0.01 x (1-0.5) = 0.18W

  - The current limit resistor (Rlim) is calculated by estimating the Rds(on) of the FET at 100 degrees Celsius. Then the following calculation is Rlim = I_curr_limit x Rds_max(on) / (Ilim(th)) = 2.21 kOhms. 
  
#### General Component Selection
For notes on general component selection, I chose resistors and capacitors with the values specified, as well as components that were rated for the sufficient voltage levels (>26V at the input) and (>15Vin other places on the board) as well as the sufficient current levels (>10A instead of 6A because I was taking into account ripples that the inductor would then smooth out). 

I could have chosen a smaller footprint for most of my resistors/capacitors (0603’s instead of 0805’s). I thought we were switching to 0805's (but apparently not rip).  

### Detailed Design - Layout 
![12V Schematic - K](img/kathleen_12Vlayout.PNG)

In terms of lessons learned and takeways from this board, when picking an IC with a thermal pad at the center for either a ground reference or for heat dissipation, you can add in methods of making this easier to solder. The typical method is putting solder or solder paste on the pad, centering the component, and heating it from above with your hot air gun. However there are alternative ways as well that could work, especially if you don't have a rework station. For example, you could add in a larger via in the center of your thermal pad so it's possible to insert solder through that hole and more easily solder the thermal pad on. Additionally, some people have added a pad onto the bottom of their board (under the IC) in order to make it easier to heat the board up from the bottom and solder the iC on.

Also, a lesson learned is not to forget the mounting holes near the corners of the board. Selecting components using the Altium Library Loader is also helpful as well, since it allows you not to have to manually create some footprints yourself. Due to learning this after submitting my board, I could have saved room on my board by choosing a smaller footprint for my inductor, which took up quite a bit of space on my board.
In terms of the layout, it’s good practice to prioritize making the loop between the input capacitors and the source of the low-side FET to be very small. You also ideally want one continuous ground pour polygon to tie everything together, having as much opposed copper as possible for input/output/ground as well as also including multiple vias to dissipate power. 

The switch node, on the other hand, should be made only as large as required to handle the load current. Because of the fast, high-frequency, voltage transitions at that node, the switch node could become an antenna and cause switching noise throughout the board. 

## 5V Buck Converter  <a name="5V"></a> 

### Design Overview <a name="5Vdesign-overview"></a>
For the 5V converter, I also chose to go with a buck converter and chose the LMR36520 regulator, with an input of 22-26V, an output of 5V with low output voltage ripple (around 3 mV), a max output current of 2A, a switching frequency of 400 kHz, and an under voltage lockout condition of 17.9V for the input. 

### Detailed Design <a name="5Vdetailed-design"></a>
![5V](img/5V_schematic.PNG)
In terms of specifics on the design, the IC is able to automatically switch from PFM to PWM depending on the load when it's put in auto mode. For light loads, the mode is PFM with diode emulation, allowing DCM (discontinuous current mode) due to the low average current at that load. The high-side MOSFET is turned on in a burst of one or more pulses to provide energy to the load (the burst depending on how long it takes the inductor current to reach IPEAK-MIN). This helps optimize efficiency and provides good light-load efficiency which we want with a low-load 5V converter that mainly supplies power to MCUs and ICs (which have low current). 

For heavy loads, the device operates in PWM at a constant switching frequency. This has goof regulation and also a lower output voltage ripple than PFM mode. 

The output voltage of the IC is externally adjustable with a resistor divider network (Rfbt and Rfbb). The converter holds the voltage at the FB pin to be equal to the internal reference voltage Vref (1V), keeping the output at a consistent value. I calculated a standard value of 100 kOhms for Rfbt and then found Rfbb to be Rfbt / (Vout/Vref - 1) = 24.9 kOhms. 

When selecting the inductor, I first estimated the percentage of inductor current ripple (K) to be around 0.8. The parameters for picking the inductor are the inductance and saturation current with the inductance being based off the peak-to-peak ripple current. I then used L = ((Vin - Vout) / (fsw * K * Iout,max)) * (Vout / Vin) = 12 uH. 

When selecting the output and input capacitors, I selected them to have low output and low input voltage ripples and good load transient performance. My calculated values (the process detailed in the datasheet) were 4.7 uF and 47 uF for the input and output capacitors respectively. The datasheet advised having more lower capacitances rather than one giant one, so I added 3 to the output and 2 for the input for each board. This was because large values of output capacitance can affect start-up behavior. For the input capacitance, I chose mine to reduce the input voltage ripple with low ESR capacitors. 

I then had to choose values for certain components like my bootstrap capacitor connecting the BOOT and SW pins to store energy required to supply the gate drivers for the power MOSFETs. I also chose a capacitor for the VCC pin to regulate the control circuits of the internal LDO of the IC. 

#### Detailed Design (Layout)
In terms of the lauout, there were specific guidelines to follow. You want to minimize the loop formed by the input capacitors and ground since they can cause large transient voltages. Additionally, you want your input caps as close as possible to your VIN and GND terminals, your voltage feedback resistor divider to be as close as possible to the FB pin to be as accurate as possible, and wide paths/pours for VIN, VOUT, and GND. Additionally, the datasheet advised at least one ground plane in one of the middle layers to help with heat dissipation and also to act as a noise shield for certain signals to ensure an accurate output voltage. Because of this and since the boards were sponsored, I ordered a 4 layer PCB to incorporate these middle layers. 

## Mounting and Packaging <a name="mounting-packaging"></a>
There are multiple options for mounting our power converters on the car. One option (as done in previous years) is to mount the boards using their mounting holes on top of other boards such as the DAQ and BMS (in a mother-daughter board configuration). Another option would be to mount them all together, basically creating a centralized power distribution board somewhere on the board as opposed to having multiple boards in different areas on the bulkhead. 

This is the plan for power converters this year/next year. However, the eventual goal is to have power converters as part of our existing PCBs (such as the BMS, MC, and DAQ), essentially just requiring members to copy-and-paste our power converters onto their boards in Altium. This will hopefully be more space efficient and require no additional external mounting. It will also cut down on the number of PCBs we will need printed. 

## Bills of Materials <a name="BOM"></a>  
BOMs for 12V, 5V, and 19V converters:

https://docs.google.com/spreadsheets/d/10i5qxnwdUmL1qU_4K43A65jEikZmG6pZHVZ2kQKUVQM/edit#gid=0

The most expensive components are typically the ICs or the inductor, especially if the inductor is large, with resistors and capacitors seeming to be the cheapest components. 

## Manufacturing/Testing <a name="manufacturing-plan"></a>
Our boards are being manufactured all through the year since we have multiple converters. We have manufactured and successfully tested a 12V converter, and we have also gotten back the second 12V board and the 5V board. The 3.3V board should also be sent out for fabrication relatively soon. 

Since these are power converters that have no programmable element, assembling and testing for the converters primarily involves soldering the IC and all the other components (and confirming in particular the IC is soldered on correctly) before plugging in the converter to the battery or a power supply and testing the output with a load. We haven’t tested a converter that doesn’t work, but in that case, we will probe certain pins to confirm they are at the correct levels and also use a scope to test the voltages and currents at certain points in the circuit as well. We will test converters both in no load and loaded conditions. 

## Project Reflection and Future Work <a name="project-reflection"></a>
In terms of the status of the power converters, we are on a different timeline from the other projects. Since we have many different converters, we do not have one long, cumulative project throughout the year. Instead, we have multiple mini-projects that involve us always being in either the design or testing stages. 

Both of us initially started working on the horn converter since this was the one that could have the most amount of noise. The horn is also resistant to damage so in case we made mistakes, the outcome wouldn't be as destructive to the car. the next priorities are the 5V and 3.3V converters (since these are necessary for the MCUs on the boards). Next, the 19V and 5V converters for the Jetson/Xavier and USB hubs for the cameras will be 

Currently, Kathleen's horn converter is working and Eric's horn converter should also work (and will be finished sometime before the spring semester). Kathleen is going to solder the 5V board & test that system and is starting on creating the 19V converter (which might be a flyback converter instead of a buck converter). Eric is working on the 3.3V board (which will hopefully be finished before Jan 1) and also on soldering his horn converter so it can be tested. 

Our current aim is to just get converters for the horn and MCUs finished near the beginning of spring, before moving on to converters for the 19V and 5V converters. Miscellaneous converters for automation and the lighting system are TBD. 

Reflecting on the semester, if we were to redesign converters, there are several things that we may consider.

Both of us created horn converters. While I think it was helpful to go through the entire design process and give both of us the learning experience of designing converters (since it's kind of difficult to work on the same layout on Altium), it would probably have been more time-efficient to work on the same first converter together. Taking Power Electronics at the same time though is very helpful and we highly recommend doing this, since you can understand the datasheets much better and also can ask Prof. Afridi for help as well. 

Additionally, if redesigning converters, we could consider having flyback converters instead of buck converters as well as doing more research into alternative buck ICs.

## References <a name="references"></a>
Datasheet for 12V Buck Controller IC: https://www.ti.com/lit/ds/symlink/lm3150.pdf?HQS=TI-null-null-digikeymode-df-pf-null-wwe&ts=1608011015645

Datasheet for 5V IC: https://www.ti.com/lit/ds/symlink/lmr36520.pdf?HQS=TI-null-null-digikeymode-df-pf-null-wwe&ts=1607969132132


