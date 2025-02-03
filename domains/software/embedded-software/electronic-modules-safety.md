# Safety Precautions while Working with Electronic Modules

Precautions need to be taken, especially by firmware engineers,
when hadnling electronic modules to prevent:
- ESD damage
- physical damage
- heat and humidity
- electrical damage

## Electrical static discharge - ESD
- [ESD basics](https://www.youtube.com/watch?v=pWhtyz-UFZc)
- damage that can occur when objects get electrical charge 
when in contact it another chareged object
- humans can not detect ESD less than 3000V
- electronics that is ESD sensitive is often abrevated with ESDS
- there are components with ESD sensitivity of 10V
- the smaller the device the greater the ESDS
- the ESD Association has two models to use when dealing with ESD:
    - Human body model - HBM
    - Charged device model - CDM
- the Ansi/ESD S20.20 protects:
    - standard sensitivity parts:
        - >= 100 HBM
        - >= 200 CDM
    - highly sensitive parts:
        - < 100 HBM
        - < 200 CDM
- we can have catastrophic failures (burned components) or latent failures
(not visible, failures are slow to manifest especially after repeted exposure)
- to protect remove any unnecessary things from ESD area, wear grounding gear
when interacting with exposed electronic modules, store exposed electronic 
modules in ESD safe storage (bags, boxes, etc.)
- **NO HUMAN TOUCH** is permitted on the pins and leads of ESDS components or 
ESDS circuits


## Physical damage
- damage by misshandling or environemental stress, intentional or unintentional
- dropping, bending the module might cause in the PCB to break, PCB lines or ICs
to break as well
- bending wires, resoldering a point to much might cause connectios to wear off
- when handling modules disconnect all connections to it

## Heat and humidity damage
- causes termal stress which can lead to damaged components and soldering joints
- watter damage when the module is powered off can cause oxidation of soldering 
joints on ICs and passive components
- watter damage when the module is powered on can cause shortening

## Electrical damage to electronic modules
- faulty components
- voltage surgase or short circuits
- wrongly assumed and connected polarity of electronic modules
- wrongly assumed voltage levels
- improper soldering joints that cause short circuits between lines
- if in doubt about voltage level and polarity, soldering joints contact hardware or
production department

