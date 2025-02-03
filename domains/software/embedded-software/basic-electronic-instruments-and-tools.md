# Common electronic instruments and tools

Electronic instruments every firmware engineer should have and know how to use:
- laboratory power supply
- digital multimeter
- osciloscope
- logic analyzer

## Laboratory power supply
- [laboratory power supply basics](https://www.youtube.com/watch?v=FfI3GRQbV0s)
- usually have banana type connectors
- prefer power supplies that have separate output enable from the device powr on/off switch. This
enables user to set the voltage and current limits before turning the power supply output on
- when setting the voltage and current limits refert to the power supply manual
- power supply channel in general can be connected in parallel to get more current than available on single channel 
- power supply channel in general can be connected in serial to get more voltage than available on single channel 

## Digital multimeter
- [multimeter basics](https://www.youtube.com/watch?v=4lAyzRxsbDc)
- test tool to measure two or more electrical values: current (A), voltage (V) or resistance (R)
- advanced multimeters can measure: capacitors, transistors, diodes, temperatures, etc.
- there are also analog multimeters but they are no longer used that much because they have bare minimum features and
readings are not that precise
- consists of the following parts:
    - display for showing measuring information
    - dial for selecting electrical values and ranges to be meassured
    - ports to connect the component under measure
    - probes that connect to the component and the ports
- multimeters have multiple ports:
    - COM -> the "minus" port wherte the "black" or "-" wire should be connected
    - 10A -> connect the "red" or "+" wire when measuring large currents, > 200mA (value is denoted on the multimeter)
    - uAmA -> connect the "red" or "+" wire  when measuring small currents 
    - Vohm -> connect the "red" or "+" wiret when measuring voltage, resistance, or other supported features

### Measuring voltage
- must be proper voltage type selected: DC voltage or AC voltage
- the voltmeter must be connected in paralele to the circuit it is measurring, if connected 
in series no damage will be done because the multimeter will have very high resistance
- connect the probes to the appropriate ports
- select the proper range for measuring value, if the value range is not known always set to the biggest range
and decrease in steps

### Measuring current
- must be proper current type selected: DC or AC 
- the ampmeter must be connected in series with the circuit it is measuring, if connected 
in parallel damage to the multimeter will happen because it has very little resistance and
high current will pass through it
- connect the probes to the appropriate port
- select the proper range for measuring value, if the value range is not known always set to the biggest range
for the port that is connected to and decrease in steps

### Measuring resistance
- select the resistance measurement
- connect the probes to the appropriate ports
- select the proper range for measuring value, if the value range is not known always set to the biggest range
for the port that is connected to and decrease in steps

### Check continuity
- most multimeters have the feature of measuring the continuity of a circuit
- connect the probes to the appropirate probes
- select the continuity mode, has like a spaker symbol
- touch the part of the circuit with the connected probes, if they are connected there will be a small resistance
which will trigger the buzzing sound


## Oscilloscope
- [oscilloscope basics](https://www.youtube.com/watch?v=1b3ivEZo7hw&list=PL2XuMA5AwNUznkBE46tcZAF3p5Edxgm-z)
- analog and digital exists, mostly digital are in use today because of their precise measuring
- measure voltage or current signals in another dimension, mostly time
- complex pecies of instrumentation, so the focus will be on the basics to enable operating them in everyday work
- like every measuring instrument in real life oscilloscopes has an impendance: 1MOhm in parallel with ~16pF capacitance,
but the actual impedance that affects the signal being measured is a combination of the oscilloscope imendance and the prob
impedance (depends on the probe and if it can be adjusted on probe)
- before measuring make sure to calibrate the probe
- has multiple channels, with the following options:
    - vertical scaling and poissitioning (unit/division)
    - coupling: DC (direct mapping of the input signal DC and AC), AC (only the AC component), GND
    - ration
        - dependent on the probe used
        - usually the oscilloscope voltage probes are 10x, which means they attenuate the signal 10 times (voltage divider)
        - this means the oscilloscope needs to compesate the attenuation by multiplying the amplitude by 10 in this case
    - input
        - input impenance is 1MOhm
        - in some cases, when measuring fast signals, we want to terminate that line in the oscilloscope by switching the 
        input impedance from 1MOhm to 50Ohms
- triggers are available on the oscilloscope to help with capturing signals that are to fast for the naked eye
- triggers are conditions to inform the oscilloscope on when to display captured signal data on the display
- trigger parameters:
    - trigger source -> any input signal channel
    - trigger sweep modes:
        - auto
            - if there is no trigger the display will show any signal present
            - good for initial measurement when we do not know what to expect
            - because there is no trigger the image mighte be unsteady
        - normal
            - if there is no trigger the nothing will be displayed
            - useful when measuring periodic signals, will result in refreshed periodic signal
        - single
            - similar to normal but once the trigger is hit it will display the signal and go to Stop mode
            - useful when we want only specific part of a signal
        - force 
            - used in normal and single mode, acts like a trigger when measurement didn't satisfy any triggers
    - trigger types:
        - edge:
            - can be rising, falling or either polarity edge. The edge is proclaimed once the signal voltage levels pass the
            trigger level
            - mostly used
        - pulse:
            - can be set up to search for high logic level or low logic level pulse, with shorter or longer duration than 
            what is specified
            - "high" and "low" in the above case mean "above" or "below" tirgger level
        - Nth edge:
            - same as edge but the trigger occurs every "N" edge
            - time window and N are separately specified
    - trigger level:
        - threshold used in trigger types
- horizontal mode knobs are related to scaling and positioning the signal in the time axis, where the units are time/division


## Logic analyzer
- mainly digital instrument and represent the data in the same way the oscilloscope does
- it has less precision since it has digital comparators on its input but that is acceptable because only the signal levels
are important to a logic analyzer
- it samples the signal with a specific sampling rate and draws the signal idealistically
- because of its simplicity compared to an oscilloscope it is a smaller device
- applications where logic analyzer is preferred to a oscilloscope:
    - when we are passed hardware design
    - while debugging digital communication protocols
    - analyzing time diagrams on digital communication bus with large number of signals
    - when we want to trigger on specific digital patterns

