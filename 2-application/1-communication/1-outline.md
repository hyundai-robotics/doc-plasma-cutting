## 2.1.1 Communication Overview

This system uses the high-speed industrial Ethernet protocol EtherCAT to exchange real-time data between the robot controller (master) and Hypertherm power supply (slave). This enables precise control of the cutting process and monitoring of diagnostic data.

### (1) Roles and Advantages
- Real-time performance: Synchronizes the robot motion path with the plasma arc state through fast response times.
- Simplified wiring: Integrates all signals into a single Ethernet cable instead of complex analog/digital I/O wiring.
- Integrated data: Sends and receives numerous cutting parameters, including cutting current, gas pressure, and error codes, in real time.

### (2) Main Control and Monitoring Items (Process Data Objects, PDO)
The robot controller performs the following key functions over EtherCAT.
- Control signals (output to plasma)
  - Plasma Start: Signal used to start and stop the cutting arc.
  - Hold Ignition: Activated together with the arc start signal and used to maintain the arc in the pre-flow state.
  - Pierce: Remains ON during the wait period after piercing starts.
  - Request New Process: Intended to change the process ID during cutting, but not currently used.

- Status feedback (input from plasma)
  - Machine Motion: Indicates that robot motion is permitted after the piercing delay.
  - Ready for Start: Indicates that setup is complete after receiving the process ID.
  - Error: Indicates an internal equipment error.
  - Process Ready: Indicates that the system is waiting for a process ID.
  - Ohmic Contact: Indicates contact between the torch and workpiece and is used for touch sensing.
  - Remote Power Status: Indicates the power state of the plasma cutting system.
  - Arc Voltage: Voltage feedback used for height control.
  - System Info: Current error code.

### (3) Status Check and Settings (Service Data Objects, SDO)
 - Cutting condition settings
   - Process ID: Current process ID set in the plasma cutting system.
   - Condition Parameters: Cutting condition parameters such as current and gas pressure.
   - Gas Test: Manual gas output for pre-flow, cut-flow, and pierce-flow.

 - Setting status check
   - Process ID: Current process ID set in the plasma cutting system.

### (4) Hardware Connection and Setup
- Connection port: Connect the dedicated EtherCAT port on the rear of the Hypertherm power supply to LAN port #3 on the robot controller.
- ESI file (EtherCAT Slave Information): The communication map is configured by loading the XML device-description file provided by Hypertherm into the robot controller setup software. Select the corresponding communication device in the industrial communication settings.
