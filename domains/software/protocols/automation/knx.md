# KNX

## Basic overview

The foundation of the KNX technology is the bus system. Every device is 
connected to the same bus and can talk to every other device. This
results in fewer wires needed for the communication and if faults
occur on one device it won't generally cause a system wide outtage.

Although the initial cost of bus systems, like KNX, in the long run
the maintenance and utility costs are down because of individual
monitoring and control.

Originally known as European Installation Bus (EIB), developed by EIBA.
In 1991 EIBA, BCI and EHSA joint foces and created KNX. KNX is
compatible with EIB systems.

KNX is a decentralized bus system. It can have a central processing logic
but that is for specific applications. In general every KNX compatible
device has a uCPU. In KNX system there are three types of device:
- system device: power supply, programming interface, etc.
- sensors: gather input and generate events
- actuators: listen for events and generate outputs

The smallest KNX system consists of a sensor and an actuator.

### KNX Communication Media

Media that is used in KNX systems:
- KNX Twisted Pair (KNX TP) - bus comble
- KNX Powerline (KNX PL) - uses the existing 230V mains network
- KNX Radio Frequency (KNX RF) - communication via radio signal
- KNX IP - communication via Ethernet

#### KNX TP

Two wires to carrie that data and power. Cost-effective solution
for projects from scratch, and easy to install.

The bus voltage is by design 24V but tolerates ranges 21V-30V.
The 9V tolerance range compensates for any voltage drops or 
contact resistance. DC voltage is used.

The DC power supply voltage is separated from the AC data
carryinig voltage using a capacitor. A transformer decouples
the data in AC voltage. On the transmitting side the transformer
is also used to superimpose the data on the outgoing voltage.

Nominal data rate is 9600 bits/s (1,2 kB/s). The communication 
is serial one byte at a time, but asynchronously. When logical
'0' is transmitted, the voltage drops for 104us before raising
+Vcc. This is due to inductor effect of the choke.
When logical '1' is transmitted the voltage level doesn't
change.

One important feature of the KNX TP is that the signals are 
coupled symmetrically ontu the bus and it is not referenced
against the ground. This is called differential signaling.
The data is extrapolated by comparing the values on both 
cables at the same time. This tackles the interfirence 
isseus, because it is nullified since it happens on both
cables and only the difference is measured. 


##### Data frame (telegram)

KNX TP telegrams have 4 fields:
- Control field: 1B
    - priority of the telegram
    - was the telegram transmission repeated
- Address field: 5B
    - sender address; individual address
    - destination address; individual or group address
- Data field: 16B
    - can be less than 16B
    - payload of the telegram
- Checksum field: 1B
    - parity checks

##### Bus access method

Access to the bus is random and event driven. Only one 
telegram can be transmitted at a time (half-duplex).
Collisions on the bus are prevented by using the 
CSMA/CA. Logical '1' is idle state of the bus, so the
logical '0' has priority. Transmitter devices constanlty
listens for every bit on the bus as soon as the signal on 
the bus differs from what it has sent an that transmitter 
doesn't have priority (is sending '1' but somebody else 
is sending '0' at the same time) is stops its transmission.

When the higher priority transmission finishes, the terminated
one recommences (starts again from the beginning).

Priority is defined in the control field which is the first 
byte. Lower value has bigger priority. If transmitters with 
the same priority transmit the one with the lower source 
address has priority.

##### Connection of bus devices

Bus devices are connected via components known bus terminals.
Bus terminals are plug in terminals capable to accommodate
up to 4 KNX cables. They enable disconnecting the device 
from the KNX bus without interrupting the bus line.


#### KNX PL (Powerline)

Perfect scenario to retrofit existing electricity cables.
The electricity cables (phase + neutral) are used to transmit
the KNX communication telegrams. The KNX data is superimposed
onto the mains voltage. Since no extra cables need to be laid
this is a cost-effective way to retrofit KNX into an existing 
electroinstallations.

No additional power supply is needed because the main 230V
is used. Phase couplers are used to ensure that the 
communication can take place over all three phases.
Band-stop filters are used to prevent the data signals
to propagate to the mains grid. Instead of phase couplers
system couplers can be used.

Data rate is 1200 bits/s (0.15 kB/s). Data information is modulated
onto the AC using spread frequency shift keying (S-FSK). A signal
of frequency 105.6 kHz corresponds to logical '0', while a logical '1'
is represented with 115.2 kHz. Thanks to comparating techniques and
corrective procedures, interference doesn't affect the readings.
The key frequenci is 110 kHz, that is why the alias for KNX PL
is PL110.

##### Data frame (telegram)

KNX PL telegrams are extended KNX TP telegrams. KNX PL telegrams
have four fields:
- Training field: 4 bits
    - synchronises and sets the levels of senders and receivers
- 2 Preamble fields: 2B
    - indicate start of transmission
    - control access to the bus 
    - needed to prevent telegrams for colliding
- Complete KNX TP frame: 9B up to 23B
- System ID: 1B
    - ID of a KNX PL system, used for ensurring communicaiton
    of systems with the same ID

##### Bus access method

Like KNX TP, the KNX PL requires the use of bus access method 
to prevent collisions between telegrams. This can only be done
by delaying the sending of telegrams by bus devices. The default 
of all bus devices is receiver mode. Only when certain conditions
are met are they able to switch to sending mode. If a device detects
a bit string of a preamble, this indicates to the device that the bus
is occupied. There is a differentination between Bus occupied and 
Bus blocked. If device receives Bus occupied signal the transmission
is delayed until a later point in time, where the point in time 
is chosen at random from one of seven options.

Devices are connected directly to the 230V mains network.

#### KNX RF (Radio Frequency)

Appropriat KNX communication medium when it is not possible to lay
new cables (i.e.: sensors are not reachable). It is also suitable
for extending existing KNX TP installations. It is possible to have
all technology in a building to be controlled wirelessly but let that
remain an exception and not a rule.

Regarding power supply, KNX RF is suitable for devices that are not
in always ready state and are powered by batteries. For that reason
KNX utilizes an unidirectional communication for RF where the device
only sends telegrams when needed, it does not contain a receiver.
On the other hand KNX RF actuator need to be ready all the time
so they draw power from a 230V mains.

Radio technology works by modulating a carrier wave with information
that needs to be sent. Data modulation is done by modulating the 
carrier signals amplitude, frequency, phase or a combination of 
all the above. The modulated signal is sent to the receiver
that performs demodulation. KNX RF uses frequency modulation.
The important factor of the transmission performance is choosing 
the correct center frequency. There are two upwards-compatibe
KNX RF versions - KNX RF Ready and KNX RF Multi. Center frequency
for KNX RF Ready is 868.3 MHz and only one communication channel 
is available. This is highy vulnerable to interference from other
radio frequencies in the same or adjecent bands. KNX RF Multi overcomes
this interference by enabling devices to switch between the occupied 
channel (F1 in KNX RF F1) to two fast channels (F2, F3) or two slow
channels (S1, S2). Fast channels are for device operated by humans
while the slow channels are for devices that do not need to be 
in receiver mode permanently. Fast channels have data rates 
of 16.348 bits/s and slow channels half of that.
Channel identification is done by utlizing the preamble in 
the telegram. Multi channel devices must be able to downgrade
to single channel. KNX RF Multi enbles verifications that
the telegram has been received using FIACK (Fast IACK).
If no IACK is received telegram is automatically repeated.

##### Data frame (telegram)

Like other communication media in KNX RF the data is sent 
through multicast telegrams, meaning one telegram can be 
received by several bus devices simultaneously.
KNX RF telegrams have 8 fields:
- Synchronization field: ?
- Data Block 1: 10B
    - Control field: length of the telegram, transmission quality,
    battery status of battery-operated devices, unidirectional or not
    - Serial Number/Domain Address: KNX serial number or domain address
    - Checkusm
- Checksum: 2B
- Data Block 2: 16B
    - Synchronization
    - Individual (source) address
    - Individual (target) or group address
    - Control field
    - Data
    - Checskum
- Checksum: 2B
- Data Block
- Checksum
- Synchronization

#### Bus access method

Unidirectonal only send data. Bidirectional check for the radio
channel is free before sending. If it is occupied the device 
waits until it is free before sending.

#### Connection of bus devices

Can be surface mounted, flush mounted or built-in. 

#### KNX IP

Utilizes the Ethernet, IP and UDP standards and builds the application
layer on top of these layers. Benefits on using Ethernet:
- use the existing network infrastructure for KNX main 
and backbone lines
- buildings can be monitored and controlled via Ethernet
- several locations can be monitored and controlled 
from one location
- KNX installation can be analyzed and programmed remotely
over the internet

KNX uses tunneling and routing, both use the UDP transport protocol.
Tunneling is used to access the bus from a local or remote location
for i.e.: programming a KNX device. Routing on the other hand
is used for exchanging telegrams via Ethernet network. KNX protocols
for this methods are KNXnet/IP routing and KNXnet/IP tunneling.

##### Data frame (telegram)

Contains additional information in addition to the KNX TP telegram:
- Header length: ?
    - always the same size this value is always the same
    - identifies the start of the telegram
- Protocol version: ?
    - used KNXnet/IP protocol version
- KNXnet/IP Service type ID: ?
    - identification of the action to be carried out
- Total length: ?
    - length in B of the KNXnet/IP telegram
- KNXnet/IP - Body: ?
    - contains the body (KNX TP telegram)

### KNX Topology

#### KNX TP

##### Topology

The basic unit of a KNX TP is a line. A line includes
a KNX power supply (including a choke) and no more 
than 64 devices. The line is a twisted pair which
carries the power from the power supply and 
telerams carrying information. A device is added
as a branch to the bus line, and it can be added at 
any time. 

Line repeaters can be added if more than
64 devices are needed to be connected on a line.
Sections added with a line repeater are known as
line segments. A line segment consists of a line 
repeater and then a tipical KNX TP line again.
The maximum number of repeaters in parallel on line
is 3. This meands that the maximum number of 
devices in a line is 255.

A different approach is to use line couplers.
Realistically line repeaters and couplers are the 
same hardware but new lines are created instead of
extending an existing one. Line couplers are used 
more often in real-world applications. More lines 
meands that less telegrams travel along each line, 
because a line coupler will not send a telegram to 
a line for which it is not destined. Up to 15 lines 
can be operated via a line couplers on a line, 
referred to as the main line. The main line can still 
accomondate 64 devices but line repreaters can not be
used if line coupler is used. Each line needs its own
power supply.

Up to 15 areas can be added using an area coupler to 
form a complete system. Like the main line the area 
line can accommodate up to 64 devices. Line coupler
on an area line count as bus devices. Area coupling 
is done by using line coupler parametrised as area 
couplers. The area line is called the backbone and 
it needs its own power supply.

The benefits of separating a system into lines and 
areas:
- more reliable operations because of galvanic
separation; lines and areas have individual power
supplies
- local data traffic is isolated from other lines 
and areas
- topology is logical and manageble for commission
purposes

##### Cable lengths

To to propagation delays and signal formation
these are the limitations to cable length:
- power supply <-> device: max 350m 
- device 1 <-> device 2: max 700m (in a line)
- line segment length: max 1000m 
- power supply 1 <-> power supply 2: manufacturer
specific (in a line)

##### Individual addresses

Every device is assigned an unique, unambiguous address.
Three numbers separated by a dot (.). The number depends 
on the position of the device in the topology:
```
<area>.<line>.<device>
```
Addresses are necessary to identify the device clearly 
and also to program them. Important rule is:
Area and line couplers have their third address number
always a zero (0).

#### KNX PL

## Links and resource
1. [KNX Basics](http://knx.fi/doc/esitteet/KNX-Basics_en.pdf)
2. [Building Automation: Communication systems with EIB/KNX, LON and BACnet](https://www.amazon.com/Building-Automation-Communication-systems-Technology/dp/3319732226/ref=sr_1_1?dib=eyJ2IjoiMSJ9.kDjBkmv0JFpUWnCBBMA6FjVLfOjvf2em7KE_QHcwvgs_Xbv7ZXfUe5EWnvcN-mHBK-m4jKU1Y3jhb9x23HiuSmE5hwM3zqebuz1eSaNx0tN0jzfh4de9Oevlttz6-iS1.tQCs6ZV83LH4T486DTvy_GMuQOjDs7hFPPpdi3f60gE&dib_tag=se&qid=1714415622&refinements=p_27%3AHermann+Merz&s=books&sr=1-1)


