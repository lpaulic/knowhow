# GPIO devices

## How is a GPIO built

TODO:

## Possible GPIO configuration

1. Open Drain (OD)
    - Description: In an open drain configuration, the output transistor 
    (usually an N-channel MOSFET) can pull the output pin to ground 
    (low logic level) when activated but cannot drive it high. When the 
    transistor is off, the pin is left floating (high impedance or 
    "disconnected"). To achieve a high state, an external pull-up resistor is 
    required, which pulls the pin up to a positive voltage (e.g., 3.3V or 5V) 
    when the transistor is off.
    - Behavior:
        - Low (0): The pin is actively pulled to ground by the transistor.
        - High (1): The pin is left floating, and an external pull-up resistor 
        brings it to a high voltage.
    - Use cases:
        - I2C communication: The I2C bus uses open-drain pins to allow multiple 
        devices to share the same lines.
        - Interfacing with higher voltage devices: An open-drain configuration 
        can be used to interface between different voltage levels.
        - Driving LEDs: Open drain is useful when controlling devices like LEDs 
        where the circuit needs to sink current.
    - Example: When the pin is configured as open-drain, you would typically 
    use an external resistor (to pull up to a supply voltage). If you want to 
    pull the pin low, you activate the transistor, and to let it float high, 
    you deactivate the transistor.
2. Open Source
    - Description: In an open source configuration (less common than open drain), 
    the output transistor (usually a P-channel MOSFET) can pull the output pin 
    to a high voltage when activated but cannot pull it low. When the 
    transistor is off, the pin is left floating, requiring an external 
    pull-down resistor to bring the pin to a low state.
    - Behavior:
        - High (1): The pin is actively pulled up to the supply voltage by the 
        transistor.
        - Low (0): The pin is left floating, and an external pull-down resistor
        brings it to ground.
    - Use cases:
        - Less common than open-drain, open-source configurations are typically
        used where current sourcing is required, and low logic states are 
        managed by external components.
        - Power control: Open-source pins may be used in power supply control 
        circuits where the device must source current to activate another device.
    - Example:
        When the pin is configured as open-source, an external resistor pulls the
    pin low, and when you want a high state, you drive the transistor to connect 
    it to a high voltage.

Key Differences:
- Open Drain: Sinks current (pulls the pin low), requires an external pull-up 
for high logic.
- Open Source: Sources current (pulls the pin high), requires an external 
pull-down for low logic.

Open Drain is more common, especially in GPIO for devices like I2C buses and LEDs,
where the output transistor only sinks current. Open Source is rarer and is mainly
used when the pin needs to source current for a high logic state.

