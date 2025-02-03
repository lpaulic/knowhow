# Basic electronic components

## Resistors
- used in series or parallel
- when connected in series used to:
    - limit current flow
    - reduce EMI
    - improve signal integrity
    - protection in case of multiple signal drivers on the same wire
    - etc.
- when connected in parallel used to:
    - adjust voltage level (voltage divider)
    - terminate the signal level during times when MCU is not initialized

## Inductors
- used in RF antena matching, signal filtering, switching power supply
- most common usecase: connected in series and opposes the current change
through it
- for very slow signals the conductor is seen as a wire

## Ferrit beads
- similar consturction as inductors but not used for the same purpose
- used for filtering out unwanted signals
- for firmware design purposes can be ignored
- on schematic it looks like filled resistor

## Capacitors
- similar to inductors but applied to voltage
- for purposes of inspecting schematics from FW point of view the capacitor
will be connected in parallel to the signal line, sometimes in series to
- for slow or DC circuits it is seen as a open circuit -> no influence on slow signals
- parallel connection provides filtering and noise immunity of the signal, can be ignored
while looking at the sgnal flow
- series connection provides DC decoupling, slow (or DC) signals can not pass through

## Relays
- electromechanical component used for controlling large loads via small signals
- consists of:
    - the coil (form of inductor) -> 2 pins, used for applying current
    - load contact -> can be 2-3 or more pins, depending on the internal switch
- the coil is not electrically connected to the load contacts, relays are also used
in situations where galvanic isolation of control signal from load is required
- two states: deactivated (default) and activated
- most common application: the coil is driven by a transistor (transistor is driven by I/O pin),
the load contacts are connected to an external load that is powerd by high voltage

## Diodes
- [how do diodes work](https://www.youtube.com/watch?v=Fwj_d3uO5g8)
- [how do Schottky diodes work](https://www.youtube.com/watch?v=bXEyCf1P0UU)
- [how do Zenner diodes work](https://www.youtube.com/watch?v=XhQqtdTlRus)
- [how do LEDs work](https://www.youtube.com/watch?v=O8M2z2hIbag)
- multiple types:
    - general purpose
    - Schottky
    - Zenner
    - TVS diodes
    - LED
- diodes consists of one positively dopped semicondudtor (P) element and one
negatively dopped semiconductor (N) element
- the N side is connected to by a Cathode (K) and the P side is connected to by
a Anode (A)
- can be connected to act as a conductor or an insulator
- the diode acts like a conductor when K is connected to V(-) and A is connected to
V(+) -> forward bias
- the diode acts like a conductor when A is connected to V(-) and K is connected to
V(+) -> backward bias
- electrical schema symbols depict where is the Cathode and Anode:
    - the vertical line at the triangle point symbolises the Cathode (K) -> points to the
    N side
    - Schotky diode has an 's' where the line is 
    - Zenner diode has an slash/backslash on a pipe where the line is
    - LEDs look like general purpose diode but have arrows going pointing away from the triangle 
- I-U diagram shows how diods act in forward and revers bias configuration. In forward 
bias there is a minimum voltage level that needs to be insured for the diode to become a
conductor. There is also a maximum voltege level defined in diode datasheet.
If the voltage passes a certain value in the reverse bias configuratio the diado will 
become a conductor again (burned diode).
- Schotky diode differs from general purpose diodes in the UF (forward voltage drop)
in the way that it is lower then the general purpose ones that are usualo around 0.7V.
Also the switching speed is higher than in general puspose diodes. On higher frequency
the difference is visible on osciloscope, in the sense that the general purpose diode
conducts current in opposite direction before switching off and blocking the current
because for every diode it takes time to switch from conducting to insulating states.
The downside of Schottky diodes is that it has a significant reverse current measuring
form ~10uA to \~1mA depending on the temperature whereas general purpose diodes have 
the reverse current in \~1uA range.
- Zenner diode are used always in reverse bias mode because after a certain U they start
conducting but they limit the voltage to because of their I-U characteristics. Zenner 
diodes are using in overvoltage protection and voltage limiting use cases.
- TVS similarly to Zenner diodes are always used in revers bias mode for overvoltage 
protection.
- LED emit light when in forward bias mode. Available in single color (2-pin) or 
multi color (mulit pins) variants. The cathode is on the physical LED is depicted 
by a dot or flat edge (the bigger metal arm).

## Transistors
- come in two forms:
    - [unipolar](https://en.wikipedia.org/wiki/Field-effect_transistor)
    - [bipolar](https://en.wikipedia.org/wiki/Bipolar_junction_transistor)
- for the purpose of understanding signal logic, both of their functionality is similar

### Uipolar transistors - FET
- two types JFET and MOSFET
- [how do MOSFETs work](https://www.youtube.com/watch?v=rkbjHNEKcRw)
- how do they work:
    - created by doping an semiconductor with elements with more electrons to form 
    elements with electrons as majority carriers (N) or elements with more holes
    to form elements with holes as majoriti carriers (P)
    - categorized in following way
        - enhanced
            - N channel
            - P channel
        - delpeted
            - N channel
            - P channel
- terminal names:
    - gate (G)
    - source (S)
    - drain (D)
    - body (B)
- between S and D there is thin layer of insulater to which the G is connected to.
- MOSFET is simetrical so D and S are interchangeable
- B and S are connected internally in the transistor housing
- current flows in the D->S direction
- electrons flow in the S->D direction
- to flow the current from D to S a channel needs to be created between the D and S,
where the channel type depends on the mosfet type
- the channel is created by adding a voltage between the G and S. The voltage polarity
depends on the element type of the S and G. If the S is a N element and B is a P element
the voltage polarity must be connected like: V(-)->S and V(+)->G. This is for N channel
for P channel it is reversed
- then the UGS is at the right level the electrons flow through the channel
- the amount of current depends on the UGS and gets saturated at some level
because the channel size decreses near the drain because the drain is opposite polarity
of the channel. Before that level the voltage and current follow ohms law when the 
transistor is conducting
- the difference between enhanced and depleted is that depleted are conduction by default
and need voltage level opposite in reverse polarity to decrease the channel and stop electron
flow
- electrical schema symbols depict the transistor type:
    - N channel transistors have the arrow pointed to the gate -> the arrow shows where the electrons go
    - P channel transistors have the arrow pointed away from the gate -> the arrow shows where the electrons go
    - enhanced transistors have separated B, D, S terminals
    - depleted transistors have connected B, D, S terminals
- also referred to voltage regulated transistor

- sitch behaviour quick reference:
    - N channel:
        - UGS > 0V (doesn't have to be 0V, depends on the transistor), switch closed
        - UGS <= 0V (doesn't have to be 0V, depends on the transistor), switch opened 
    - P channel:
        - UGS <= 0V (doesn't have to be 0V, depends on the transistor), switch closed
        - UGS > 0V (doesn't have to be 0V, depends on the transistor), switch opened 

### Bipolar transistor - BJT
- [how do BJTs work](https://www.youtube.com/watch?v=7ukDKVHnac4)
- terminal names: 
    - emmiter (E)
    - collector (C)
    - base (B)
- these trenistors are made by combining two of P dopped elements with one of N dopped element
or vice versa, where the one element of different dopping is in between the two elements of the
same dopping. So we have PNP or NPN
- the logic of getting the transistor in closed or opened state is the same
- the electrical specifications differ
- terminal corenspondences between FET and BJF:
    - E -> S
    - C -> D
    - B -> G
- electrical schema symbols depict the transistor type:
    - PNP transistors have the arrow pointed to the B -> the arrow shows where the electrons go
    - NPN transistors have the arrow pointed away from the B -> the arrow shows where the electrons go
- also referred to as current regulated transistor, has current gains 

- NPN BJTs can be roughly compared to N-channel MOSFETs
- PNP BJT transistors are often found in the configuration where the E is connected to ground and 
the switch is closed by providing a current to B
- PNP BJT trnasistors, complement of NPN, are used in configuration where E is connected to high
potential and the switch is closed by not providing current to B

## Integrated Circuits - ICs
- application specific chips
- they are always labeled with their product number (PN)
- to find the datasheet just search the PN on the internet or ask colleagues
if the datasheet is not publicly available

## Connectors
- provide interface from the module to the user
    - power supply, communication interfaces, indication signals
- common types:
    - terminal blocks (plastic and screw)
    - pin headers
    - FPC - thin, low profile and high signal density connector
- [Well known connectors](https://www.l-com.com/resources/connector-charts)
- [Automotive connectors](https://autoctrls.com/oem-automotive-wiring-connectors)

## Printed circuit board - PCB
- contains all the electroinc comoponents, traces and connection between them
- can be in rigid format, than FR-4 substance is used
- can also be in flexible formant, than polyimide is used
- PCBs can be single and multi layered

## Electronic module
- refers to PCB with soldered electronic components

