# SCM - Safety Circuit Monitor
A Circuit that monitors the Safety Circuit on an FS car and toggles LEDs for the most upstream failure point.

## Detailed Description

The purpose of this device is to display to the driver the current state of the Safety system. The safety system is a set of switches and devices which ensure safe operation and shutdown of the car under specific circumstances, once one of these devices is triggered its important for the driver and any technicians to be aware of where exactly the problem is.

## Working Principle

By monitoring various points along the circuit we can determine the most upstream failure point. The Safety Circuit works by driving 12V through various devices in series, the output of the entire stream feeds into automotive relays which then enable power delivery to critial automotive systems such as the ignition coils, fuel pump, and injectors.

![](<Documents/ShutdownCircuit.png>)

So by monitoring the input and output of each device we can determine if 12V is entering the device and if 12V is being output, if a device is not outputing 12V while its input is active then we know that the device has been triggered.

### Signals

The signals we monitor are:

- **BSPD** (Brake System Plausability Device)
- **Inertia** Switch
- **BOTS** (Brake Over Travel Switch)
- **Cockpit** Shutdown Button
- **Left** Shutdown Button
- **Right** Shutdown Button

Hence the Circuit will require six monitoring circut, each looking at the input and output of one device, however since the devices are in series the output of one device is also the input of the next one. 

## Schematic

![](<Documents/Module.png>)

Each module monitors the input of a device and its output, the basic function is that we use an optocoupler with a pullup, the input of a device acts also as the power source for the module. If we have 12V input into the system we will have a pullup on the output of the optocoupler, which will feed the BJT and sink the external and internal LEDs, showing an error. However if we also have 12V at the output then the pull up sinks to ground via the optocoupler. 

Since the devices are in series, downstream devices wont get any power and no LEDs will be turned on, effectively the system will only light up the most upstream failure point so the driver can focus on reseting it.

## Potential Future Revisions

- Increase of possible devices for future safety systems with more than six devices.
- Decrease power consumption (mainly from constantly sinking current through the optocoupler during normal operation)
- adjustable resistor values for varying external LEDs??