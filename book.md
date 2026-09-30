[__SOURCE](README.md)
# ${cont_model} Controller Function Manual - Plasma Cutting

[__SOURCE](0-about-this-manual/precautions.md)
# Safety Precautions

{% include file="en/precautions.md" %}

[__SOURCE](1-intro/README.md)
# 1. Overview

This chapter explains the basic concepts of plasma cutting and the configuration of the HD Hyundai Robotics plasma cutting system.

[__SOURCE](1-intro/1-definition.md)
# 1.1 Plasma Cutting

Plasma cutting uses a high-temperature plasma arc to cut metal quickly and precisely. This system combines HD Hyundai Robotics robot automation technology with Hypertherm plasma cutting equipment to provide high-quality cutting and improved productivity.

<br>

### (1) Plasma Cutting Principle  
In plasma cutting, compressed gas is electrically ionized into an extremely hot plasma and then directed onto the metal surface. The resulting high-temperature arc instantly melts the metal, while high-velocity gas removes the molten material to produce the cut.

<br>

### (2) System Configuration  
The overall system consists of an HD Hyundai Robotics robot system and plasma cutting equipment. See Section 1.3, System Configuration, for details.
  - Robot and control system (HD Hyundai Robotics): Provides precise path control and repetitive operation.
  - Plasma cutting equipment (Hypertherm): Provides stable arc generation and cutting functions.
  - Communication: Supports cyclic (PDO) and acyclic (SDO) EtherCAT communication.

<br>

### (3) Roles of Plasma Gas and Shield Gas  
- Plasma Gas  
    The gas is ionized by an electric arc to form the high-temperature plasma that performs the cutting.  
    It directly affects cutting speed, cutting force, and cut-surface quality.  
- Shield Gas  
    The shield gas surrounds the plasma arc and protects the cutting area.  
    It blocks ambient air and helps reduce oxidation and slag formation on the cut surface.

<br>

### (4) Main Specifications  

|Item|Specification|Remarks|
|:--:|:--:|:--:|
|Process type|Cutting, marking, gouging||
|Cutting speed|mm/sec|Determined by thickness (up to approximately 100 mm/s)|
|Path accuracy|±1.0 mm||
|Tracking performance|1.5 mm/sec|At a cutting speed of 35 mm/s|
|Cut-surface quality|Passes Hypertherm evaluation|Requires precision tuning of vibration suppression control|
|Gas|Oxygen, air||
|Material|Mild steel||
|Thickness|Up to 500 mm||
|Current|Up to 300 A|Depends on the plasma power supply model|
|Supported Hypertherm models|XPR 170, XPR 300||
|Communication|EtherCAT||

[__SOURCE](1-intro/2-classification.md)
# 1.2 Cutting Classifications

### (1) Classification by Gas Type

In plasma cutting, the combination of plasma gas and shield gas has a significant effect on cutting quality, speed, and consumable life. This system primarily uses oxygen-air (O₂-Air) and air-air combinations. Oxygen-air is most commonly used for carbon steel, while air-air provides excellent versatility and economy.

<br>

|Comparison|Oxygen-Air|Air-Air|
|:--:|:--:|:--:|
|Advantages|Higher cutting speed through the oxygen/metal oxidation reaction<br>Excellent cut-surface quality and reduced slag<br>Can minimize post-processing|Lower operating cost<br>Uses only compressed air without a separate gas supply<br>Simple equipment configuration<br>Applicable to various materials (carbon steel, stainless steel, and aluminum)|
|Disadvantages|The oxidation reaction creates an oxide layer on the cut surface<br>Relatively rapid wear of consumables such as electrodes and nozzles|Lower cutting quality than oxygen plasma<br>Slightly rough cut surfaces and possible slag formation<br>Limited performance when cutting thick material|
|Applications|Carbon steel (such as SS400)<br>Medium plate and structural cutting<br>Productivity-oriented processes|General machining<br>Sites where low maintenance cost is important<br>Thin-sheet cutting|

<br>

### (2) Classification by Workpiece Thickness

Cutting conditions and work methods vary according to workpiece thickness. In this function, the cutting condition is selected based on thickness.

|Comparison|Thin Plate|Medium Plate|Thick Plate|
|:--:|:--:|:--:|:--:|
|Thickness|Approximately 1-6 mm|Approximately 6-25 mm|25 mm or more|
|Characteristics|High-speed, high-productivity cutting<br>Low current and high cutting speed<br>Because heat effects are significant, minimizing deformation is important|Balance between cutting speed and quality is important<br>Most commonly used range in industrial applications|Requires high current and sufficient gas flow<br>Piercing strongly affects quality (spatter and slag)<br>Piercing time and torch-height control are important|

<br>

### (3) Classification by Cutting Start Position

The cutting method differs according to the cutting start position, which is important for both cut quality and equipment protection. Select the method on the condition settings page. Each method uses a different motion sequence.

|Comparison|Edge Start|Piercing Start|
|:--:|:--:|:--:|
|Method|Starts cutting at an outside edge or corner of the workpiece|Pierces the workpiece before starting a cut inside the workpiece|
|Characteristics|No separate piercing process is required<br>Less load on the equipment and consumables<br>Stable cutting quality and fewer defects|The initial arc must pierce the material<br>High-temperature spatter may damage the nozzle or electrode<br>Cutting quality and success depend heavily on the piercing conditions|

<br>

Independently of the start method, additional tool paths may be used to improve the quality of the cut.

|Comparison|Lead-in / Lead-out|
|:--:|:--:|
|Method|Enters or exits outside the actual machining path at the start and end of cutting|
|Characteristics|Improves quality at the start of the cut<br>Prevents notches and overcutting<br>Protects the product profile|

[__SOURCE](1-intro/3-configure.md)
# 1.3 System Configuration

The Hypertherm plasma cutting system and robot controller are integrated as shown below to provide precise cutting quality and automation.

![Figure 1.1 System configuration](../_assets/configure.png)

<br>

### (1) Hypertherm Plasma Power Supply  
The core of the system, this unit supplies high-voltage power to generate the plasma arc.
- Functions: Controls current and gas flow and monitors consumable life (for example, XPR 170).
- Communication: Connects to the robot controller through EtherCAT to exchange cutting parameters in real time.  

### (2) Robot System and Controller  
The drive system responsible for precise torch movement.
- Robot: A six-axis articulated robot with a payload of at least 10 kg is used to accommodate the torch and cable load and perform complex 3D or bevel cuts.
- Robot controller:
    - Sends cutting start/stop signals to the Hypertherm power supply and precisely controls torch position by calculating the travel speed and path.
    - Maintains a constant voltage-based gap between the torch and workpiece to compensate for workpiece warpage or deformation during cutting. Real-time Z-axis height compensation helps maintain a uniform kerf width.

### (3) Gas Console  
Precisely controls the pressure and mixture ratio of cutting and shielding gases such as oxygen, nitrogen, and air.
  - Function: Supplies gas optimized for the material and thickness, helping prevent oxidation and determine cut quality.
  - GCC (Gas Connect Console): Supplies and controls plasma and shield gases, including gas flow, pressure, and switching.

### (4) Torch and Lead Assembly  
Mounted at the end of the robot arm, this assembly performs the actual cutting.
  - Function: Receives coolant, gas, and power from the power supply and generates plasma.
  - TCC (Torch Connect Console): Transfers torch-related signals and power to generate and control the plasma arc.
  - Collision sensor: Immediately stops the robot if the torch contacts the workpiece or an obstacle, protecting the equipment.

### (5) Ground and Work Lead  
A cable connected to the workpiece to complete the circuit from the plasma power supply. Reliable grounding is essential for stable arc generation.

[__SOURCE](2-application/README.md)
# 2. Plasma Cutting Application

[__SOURCE](2-application/1-communication/README.md)
# 2.1 Basic Settings

The plasma cutting application communicates with a Hypertherm XPR plasma cutting system over EtherCAT. It also uses some arc-welding application functions for touch sensing and height control. EtherCAT, block assignment, arc welder, and signal settings must therefore be configured.

[__SOURCE](2-application/1-communication/1-outline.md)
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

[__SOURCE](2-application/1-communication/2-ethercat.md)
## 2.1.2 EtherCAT Settings

General EtherCAT master setup is described in the Industrial Communication Manual. The settings required for this application are described below.

### (1) Hardware Connection and Setup
- Connection port: Connect the dedicated EtherCAT port on the rear of the Hypertherm power supply to LAN port #3 on the robot controller.
- ESI file (EtherCAT Slave Information): The communication map is configured by loading the XML device-description file provided by Hypertherm into the robot controller setup software. Select the corresponding communication device in the industrial communication settings.

![Figure 2.1 EtherCAT master settings](../../_assets/ecat_master.png)

### (2) Block Assignment
- Fieldbus I/O block selection: Select `EtherCAT I/O` for one of the ten available fb blocks. The selected block number is used when configuring the arc signals.

![Figure 2.2 fb block assignment](../../_assets/fb_block.png)

[__SOURCE](2-application/1-communication/3-arcwelder.md)
## 2.1.3 Arc Welder Settings

The arc welder type used by the plasma cutting application is General Welder. Configure the welder as described below.

<br>

### (1) Selecting the Welder

Under `[F2: System > 5: Initialization > 3: Application Settings]`, enable arc welding and enter welder manufacturer number `9` (9: General Welder).  
Press `[Welder Settings]` to open the General Welder settings page.

![Figure 2.3 General Welder settings](../../_assets/gerneral_welder.png)

<br>

### (2) Signal Assignment
The General Welder condition page consists of the Welder, Input Signal Assignment, and Output Signal Assignment tabs. Because the arc welder settings screen is shared, plasma cutting signals are assigned to corresponding arc-welding items.

 - Input signal assignment  
 On the Input Signal Assignment tab, press `[Auto Setup]`. Select the Hypertherm-XPR model from the detailed options, and then enter the start address of the previously assigned FB block.

![Figure 2.4 Input signal assignment](../../_assets/sig_assign_in.png)

 - Output signal assignment  
 On the Output Signal Assignment tab, press `[Auto Setup]`. Select the Hypertherm-XPR model from the detailed options, and then enter the start address of the previously assigned FB block.

![Figure 2.5 Output signal assignment](../../_assets/sig_assign_out.png)

<br>

### (3) Verifying Signal Assignment

Assigned addresses are displayed for items corresponding to the existing General Arc Welder signals. Their states can be checked on the plasma cutting monitoring screen.  
If fb1 is selected during FB block assignment, the addresses are assigned automatically as shown below.

<br>

<table>
  <thead>
    <tr>
      <th style="text-align: center;">Type</th>
      <th style="text-align: center;">Arc Welding</th>
      <th style="text-align: center;">Plasma Cutting</th>
      <th style="text-align: center;">Signal Assignment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center" rowspan="10">Input</td>
      <td align="center">Welder available</td>
      <td align="center">Remote power status</td>
      <td align="center">fb1.9</td>
    </tr>
    <tr>
      <td align="center">Wire stick signal</td>
      <td align="center">Ohmic contact</td>
      <td align="center">fb1.8</td>
    </tr>
    <tr>
      <td align="center">Process active</td>
      <td align="center">Process ready</td>
      <td align="center">fb1.5</td>
    </tr>
    <tr>
      <td align="center">Communication ready</td>
      <td align="center">Ready for start</td>
      <td align="center">fb1.2</td>
    </tr>
    <tr>
      <td align="center">Welder error signal</td>
      <td align="center">Error</td>
      <td align="center">fb1.4</td>
    </tr>
    <tr>
      <td align="center">Machine motion</td>
      <td align="center">Machine motion</td>
      <td align="center">fb1.0</td>
    </tr>
    <tr>
      <td align="center">Error priority level - error</td>
      <td align="center">Error priority level - error</td>
      <td align="center">fb1.10</td>
    </tr>
    <tr>
      <td align="center">Error priority level - failure</td>
      <td align="center">Error priority level - failure</td>
      <td align="center">fb1.11</td>
    </tr>
    <tr>
      <td align="center">Welding voltage</td>
      <td align="center">Voltage</td>
      <td align="center">fb1.16 ~ fb1.31</td>
    </tr>
    <tr>
      <td align="center">Welder error number</td>
      <td align="center">Error number</td>
      <td align="center">fb1.48 ~ fb1.63</td>
    </tr>
    <tr>
      <td align="center" rowspan="3"><strong>Output</strong></td>
      <td align="center">Arc ON</td>
      <td align="center">Plasma ON</td>
      <td align="center">fb1.0</td>
    </tr>
    <tr>
      <td align="center">Hold ignition</td>
      <td align="center">Hold ignition</td>
      <td align="center">fb1.1</td>
    </tr>
    <tr>
      <td align="center">Pierce</td>
      <td align="center">Pierce</td>
      <td align="center">fb1.2</td>
    </tr>
  </tbody>
</table>

[__SOURCE](2-application/2-settings/README.md)
# 2.2 Cutting Condition Settings

Edit the settings associated with the condition number specified by the `plasma on,cnd=#` command. Each added condition is named in the `cnd_#` format. Each condition number contains start, motion, and end conditions.

[__SOURCE](2-application/2-settings/1-start-cnd.md)
## 2.2.1 Start Conditions

These settings are sent to the plasma cutting system when the `plasma on` command is executed. Enter the workpiece thickness and select the process ID appropriate for the operation from the cut chart to display the default settings. The displayed values are the recommended settings for cutting quality, but they may be adjusted for special operating conditions or workpiece conditions.

![Figure 2.6 Start conditions](../../_assets/start_cnd.png)

(1) Process Type  
Cutting is the most commonly used process, but gouging and marking are also supported.

(2) Material  
Currently, only mild steel is supported.

(3) Thickness  
Enter the thickness of the workpiece.

(4) Process ID  
After entering the thickness, the applicable process IDs from the cut chart are listed. To view detailed cutting information, press `[F1: Select Process ID]` to open the cut chart. Select the desired process ID from the table sorted by thickness.

![Figure 2.7 Cut chart](../../_assets/cut_chart.png)

(5) Travel Speed  
The speed at which the robot follows the cutting path after piercing is complete. When the `plasma on` command is executed, the value entered here is stored in the `_plasma[cnd#].speed` system variable. Use this variable as the speed parameter in the job program.

(6) Plasma / Shield  
Selects the gases used for the plasma arc and shielding. When oxygen-air or air-air is selected for mild-steel cutting, this item cannot be edited.

(7) Current  
The current applied during cutting. The maximum current is limited by the Hypertherm plasma cutting system specifications (for example, XPR300: max. 300 A).

(8) Voltage  
The voltage applied during cutting. Height control maintains the distance between the torch and workpiece so that this voltage remains constant.

(9) Plasma Flow  
Sets the plasma gas pressure.

(10) Shield Flow  
Sets the shield gas pressure.

(11) Pierce Flow  
Sets the gas pressure used during piercing.

(12) Pierce Delay  
The time to wait at the piercing position until piercing is complete. Robot motion is enabled after this time elapses.

(13) Torch Protection  
Detects electrode failures caused by unstable cutting current to help prevent torch damage.

(14) Ramp-down Error Protection  
Detects the end of cutting and gradually reduces current and gas supply to protect the electrode and extend consumable life.

[__SOURCE](2-application/2-settings/2-motion-cnd.md)
## 2.2.2 Motion Conditions

![Figure 2.8 Motion conditions](../../_assets/motion_cnd.png)

(1) Start Type  
Select either piercing start, which starts by piercing inside the workpiece, or edge start, which begins cutting at an edge without piercing.

(2) Piercing Speed  
The speed used to move to the piercing height.

(3) Cutting Speed  
The speed used to move to the cutting height.

(4) Transfer Height  
Sets the height used for arc transfer.

(5) Pierce Height  
Sets the height at which piercing starts.

(6) Cutting Height  
Sets the height at which cutting travel begins after piercing.

(7) Kerf Compensation  
A path compensation value that accounts for the width of material removed by the plasma arc. Use one-half of the kerf width shown in the cut chart directly as the path correction value.

(8) Torch Angle  
Sets the torch tilt angle relative to the workpiece during gouging. This value is available to job programs through the `_plasma[cnd#].torch_angle` system variable.

(9) Motion Delay  
Sets the time to wait while maintaining the arc at the end of gouging. This value is available to job programs through the `_plasma[cnd#].motion_delay` system variable.

(10) Motion Coordinate System  
Sets the user coordinate system used as the reference when moving to the cutting height during gouging. To account for the torch angle, the torch moves to the cutting height along the selected user-coordinate direction rather than the tool direction.

[__SOURCE](2-application/3-motion/README.md)
# 2.3 Robot Motion

Two robot motion functions are required to achieve good cutting quality: motion control in the tool Z direction to control the distance between the torch and workpiece, and shift motion in the tool Y direction to compensate for the kerf while the robot cuts along the taught path.

[__SOURCE](2-application/3-motion/1-height-ctrl.md)
## 2.3.1 Height Control

During plasma cutting, the distance between the torch and workpiece directly affects cutting quality and consumable life. This system corrects the torch height in real time during cutting by using the relationship between arc voltage and distance.

(1) Principle of Operation  

![Figure 2.10 Torch distance and voltage](../../_assets/height_ctrl.png)

 - Voltage-distance relationship: Plasma arc voltage increases as the distance between the torch and workpiece increases, and decreases as the distance becomes smaller.
 - Feedback loop: The robot controller periodically receives actual arc-voltage data from the Hypertherm power supply over EtherCAT.
 - Correction: The controller compares the measured voltage with the target voltage set by the user and moves the robot up or down along the Z axis in real time according to the difference. This function uses the `heightsen` command provided by the arc-welding application.

(2) Main Control Stages  
 - IHS (Initial Height Sensing): Before cutting starts, the torch is lowered to locate the workpiece surface and establish the correct piercing/cutting start height.  
 - Voltage Sampling: Once cutting has started and the arc has stabilized, the system measures the current voltage.  
 - Tracking and correction: Even if the workpiece is warped or inclined, the torch height is adjusted to maintain a constant measured voltage and uniform kerf width.  

(3) Main Setting Parameters  
 - Set Voltage: The voltage corresponding to the desired cutting height. Set this value based on the Hypertherm cut chart.
 - THC Gain/Sensitivity: The response rate to a voltage difference. If it is too high, the torch may hunt up and down; if it is too low, the torch may not follow workpiece contours.
 - THC Delay: The period after piercing during which height control is suspended until the arc is fully stabilized.

[__SOURCE](2-application/3-motion/2-kerf-ctrl.md)
## 2.3.2 Kerf Compensation

Because the plasma arc has a finite width and removes material as it cuts, compensation motion that offsets the torch center path away from the finished surface is required to produce dimensions that match the design drawing.

(1) Difference in Cut-surface Quality
 - Cause: Plasma gas is rotated by the swirl ring inside the torch as it is discharged. This makes the arc asymmetric and stronger on one side. The resulting difference in energy distribution produces different cut quality on the two sides.
 - Quality difference
   - Good side: High squareness, smooth cut surface, and minimal slag adhesion.
   - Poor side: Beveling, a rough cut surface, and increased slag adhesion.

{% hint style="info" %}
The good cut surface is generally on the right side of the direction of travel. Set the teaching and robot motion direction so that the right-hand surface is the finished surface. Kerf compensation must also shift the torch toward the good side.
{% endhint %}

(2) Kerf and Shift Principle  
 - Kerf width: The width of metal actually removed by the plasma arc. It varies according to nozzle size, current, cutting speed, and material thickness.
 - Offset distance: Shift the torch left or right by half of the kerf width. For example, if the kerf width is 2.0 mm, shift the torch center 1.0 mm outward from the taught line.

![Figure 2.11 Kerf compensation](../../_assets/kerf.png)

(3) Tool-coordinate Y-direction Shift (TCP Shift)  
 - The robot controller applies the compensation value relative to the torch travel direction.
 - Left/right offset: The path is shifted by controlling the axis (±Y) perpendicular to the travel direction (+X) in the robot tool coordinate system.
 - Determining the compensation direction
   - Left compensation (-Y): Shifts the torch to the left of the travel direction. This is generally used for counterclockwise outside cutting when the inside surface is used.
   - Right compensation (+Y): Shifts the torch to the right of the travel direction. This is used for inside-hole cutting when the outside surface is used.  

(4) Using the Hypertherm Cut Chart  
 - Kerf information: The Hypertherm manual's cut chart provides an estimated kerf width for each condition. Enter this value in a robot controller register so that the shift distance can be calculated automatically in the program.
 - Compensation value = cut-chart kerf width / 2 + margin (margin = 0)  

(5) Main Settings and Precautions  
 - Importance of the lead-in: Shift motion must be applied gradually along the lead-in before the cutting start point. The full compensation distance must already be established when the torch enters the product profile to prevent a step on the cut surface.
 - Compensation for speed changes: Kerf width increases as cutting speed decreases. If the robot decelerates at a corner or similar section, fine-tune the shift distance or maintain a constant speed.
 - Consumable wear: As the nozzle wears, the arc becomes wider and the kerf increases. Periodically cut and measure a test piece, and then adjust the shift value.

[__SOURCE](2-application/4-programming/README.md)
# 2.4 Robot Programming

A robot cutting job program defines not only the robot motion path, but also a sequence that synchronizes cutting parameters through real-time communication with the Hypertherm power supply.

[__SOURCE](2-application/4-programming/1-system-vars.md)
## 2.4.1 System Variables

![Figure 2.12 System variable list](../../_assets/system_var.png)

<br>

  - `_plasma.process_id`
    - Purpose: Sends a process ID to the plasma cutting system. Select an ID appropriate for the material thickness on the condition settings page.
    - Operation: The entered ID is sent over EtherCAT. When setup is complete, the Ready for Start state turns ON.
    - Usage: Select this system variable on the left side of an assignment statement and enter the process ID on the right side.
    - Example
       ```python
       _plasma.process_id = 1000
       ```

  - `_plasma[cnd#].speed`
    - Purpose: Lets the user easily apply the cutting speed configured for each process ID.
    - Operation: Retrieves the cutting speed configured for the specified cutting condition number.
    - Usage: Use this system variable as the speed parameter of a `move` statement (mm/sec).
    - Example
        ```python
        plasma on,cnd=1
        move P,spd=_plasma[1].speed,accu=0,tool=0
        ```

  - `_plasma[cnd#].kerf`
    - Purpose: Makes it easy to program robot shift motion that compensates for the kerf width.
    - Operation: Retrieves the kerf compensation value configured for the specified cutting condition number.
    - Usage: Use this system variable when defining the target position of a `move` statement (mm).
    - Example
        ```python
        plasma on,cnd=1
        var sft
        sft=Shift(0,_plasma[1].kerf,0,0,0,0,"tool")
        move P,tg=po1+sft,spd=_plasma[1].speed,accu=0,tool=0
        ```

  - `_plasma[cnd#].cutting_height`
    - Purpose: Makes it easy to enter the cutting position during teaching.
    - Operation: Retrieves the cutting height configured for the specified cutting condition number.
    - Usage: Use this system variable when defining the target position of a `move` statement (mm).
    - Example
        ```python
        var cut_hgt=_plasma[1].cutting_height
        var sft_height=Shift(0,0,-cut_hgt,0,0,0,"tool")
        move P,tg=po_cut_srt+sft_height,spd=cut_spd*0.5mm/sec,accu=0,tool=0
        ```

  - `_plasma[cnd#].torch_angle`
    - Purpose: Makes it easy to enter the torch angle required for gouging in a job program.
    - Operation: Retrieves the gouging torch angle configured for the specified cutting condition number.
    - Usage: Use this system variable when setting the torch orientation for gouging (deg).
    - Example
        ```python
        var gouging_angle=_plasma[1].torch_angle
        ```

  - `_plasma[cnd#].motion_delay`
    - Purpose: Makes it easy to enter the required wait time at the end of gouging in a job program.
    - Operation: Retrieves the gouging end delay configured for the specified cutting condition number.
    - Usage: Use this system variable as the wait time of the `plasma off` command at the end of gouging (sec).
    - Example
        ```python
        plasma off,wait=_plasma[1].motion_delay
        ```

[__SOURCE](2-application/4-programming/2-cmd.md)
## 2.4.2 plasma on/off Command

   - Moves the torch to the specified height and starts or stops the plasma arc.
   - Syntax

        ```python
        plasma on/off,cnd=<condition number>,wait=<wait time>
        ```

   - Parameters

        |Item|Input|Function|
        |:--:|:--:|:--:|
        |Plasma start|on|Moves to the configured height and starts the arc|
        |Plasma stop|off|Stops the arc after the specified delay|
        |Condition number|1-1024|Specifies the cutting condition|
        |Wait time|0-30 sec|Specifies the cutting controller wait time|

   - Example

        ```python
        plasma on,cnd=1
        move P,spd=_plasma[1].speed,accu=0,tool=0
        plasma off,cnd=1
        ```

   <br>

   ### Detailed Sequence
   ---
   The following describes the internal sequence performed by the `plasma on` command. In addition to turning on the plasma arc, the command moves the torch to the heights specified by the condition, performs piercing, and then waits in a state ready for cutting travel.

   (1) Checking the Process ID  
   The system compares the condition number entered as `cnd=#` with the condition set in the plasma cutting system. If they differ, send the process ID first.

   (2) Robot Motion and Arc ON  
   The `plasma on` command must always start with the torch at the workpiece contact position. After the command is executed, robot motion differs according to the cutting start method. The cut chart defines all heights and wait times for each process ID.

   - Piercing start  
   Because cutting starts inside the workpiece, piercing must be performed first. Cutting can begin after additional height movements that stabilize the plasma arc.

     ![Figure 2.12 Robot motion sequence for piercing start](../../_assets/pierce_start.png)

     - Move to ignition height: The transfer height is used as the ignition height.
     - Arc ON: Generates the plasma arc.
     - Move to pierce height: Starts full piercing after the arc stabilizes.
     - Pierce delay: Waits until piercing is complete.
     - Check motion signal: Checks the Machine Motion signal.
     - Move to cutting height: Moves to the cutting height and starts cutting.

   - Edge start  
     Because cutting starts at the edge or corner of the workpiece, no piercing process is required. The torch moves directly to the cutting height and starts ignition. Cutting motion can begin after the plasma arc has stabilized.

     ![Figure 2.13 Robot motion sequence for edge start](../../_assets/edge_start.png)

     - Move to ignition height: The cutting height is used as the ignition height.
     - Arc ON: Generates the plasma arc.
     - Wait: Waits for the arc to stabilize.

[__SOURCE](2-application/4-programming/3-prog-structure.md)
## 2.4.3 Basic Program Structure

A cutting job program generally consists of the following sequence.

 (1) Approach  
 Move the robot from the standby position to the safe point near the work start position.

 (2) Touch Sensing  
 Detect the workpiece surface with the torch to establish the correct start height (IHS, Initial Height Sensing).

 (3) plasma on  
 Move to the cutting position, turn on the plasma, and prepare for cutting travel.
  * Reference manual  
  [`touchsen` statement](https://hrbook-hrc.web.app/#/view/doc-arc-weld/en/2_Command/13_touchsen?cont_model=${cont_model})

 (4) heightsen on  
 Perform height control using voltage feedback.
  * Reference manual  
  [Height sensing](https://hrbook-hrc.web.app/#/view/doc-arc-weld/en/8_Application_function/4_Height_sensing/README?cont_model=${cont_model})  
  [`heightsen on` statement](https://hrbook-hrc.web.app/#/view/doc-arc-weld/en/2_Command/9_hsenson?cont_model=${cont_model})

 (5) Lead-in  
 Enter the actual cutting line smoothly from outside the product profile, if required.

 (6) Cutting  
 Follow the product profile while maintaining the configured speed and voltage (THC).

 (7) Lead-out  
 Move away from the profile at the end of cutting to avoid leaving a mark, if required.

 (8) heightsen off  
 Stop height control.
  * Reference manual  
  [`heightsen off` statement](https://hrbook-hrc.web.app/#/view/doc-arc-weld/en/2_Command/10_hsensoff?cont_model=${cont_model})

 (9) plasma off  
 Turn off the plasma arc.

 (10) Retract  
 Move upward to the next cutting position or standby position.

{% hint style="warning" %}
If the workpiece height is uniform and touch sensing is not required, touch sensing may be omitted. However, `plasma on` must always be executed at the workpiece contact position. Move to the taught contact pose before executing `plasma on`.

```python
move P1    # Move to the contact position (P1: global variable saved by touchsen)
plasma on,cnd=1
```
{% endhint %}

### Program Example

```python
_plasma.process_id = 1000                  # Send process ID
move                                       # Start position
move                                       # Position near the plate
touchsen, P1                               # Detect the workpiece position
plasma on,cnd=1                            # Turn on the plasma arc
heightsen on                               # Start height control
move P,spd=_plasma[1].speed,accu=0,tool=0 # Start cutting
...
heightsen off                              # Stop height control
plasma off                                 # Stop the plasma arc
move                                       # Return position
```

[__SOURCE](3-workflow/README.md)
# 3. Work Procedure

[__SOURCE](3-workflow/1-scenario.md)
# 3.1 Setup Sequence

The cutting operation is prepared in the following order: establish communication, select the General Arc Welder, edit conditions, and create the program. After the initial settings are complete, subsequent operations require only condition editing and program creation.

Special care must be taken when selecting the process ID. The plasma cutting system and robot controller share a cut chart that contains cutting conditions for different materials, thicknesses, and quality requirements. Select the appropriate process ID for the work environment. Because this cutting function is limited to mild steel, cutting conditions are classified by workpiece thickness. Select one of the process IDs listed for the workpiece thickness. After an ID is selected, operating conditions such as current, voltage, and speed are displayed automatically. Some values in the cut chart can be edited by the user and are sent to the plasma cutting system when the `plasma on` command is executed. If the same process ID is already set, sending `_plasma.process_id` may be omitted. However, if the ID set in the plasma cutting system differs from the ID of the condition specified by `plasma on`, a process ID mismatch error occurs.

<br>

|Step|Description|Remarks|
|:--:|:--:|:--:|
|1|Configure EtherCAT communication|Refer to the Industrial Communication settings|
|2|Select the arc welder<br>(for touch-sensing setup)|Refer to Arc Welder Settings|
|3|Set Accuracy|Level 0: tool-end position 0 mm / orientation 0 deg<br>(consider the workpiece-to-torch distance of several millimeters or less)|
|4|Configure plasma cutting application conditions|Enter the workpiece thickness|
|5|Select the process ID for the thickness|Default conditions are set when an ID is selected<br>All but certain items can be edited|
|6|Teach and create the job program<br>- `_plasma.process_id`<br>- `touchsen`<br>- `plasma on`<br>- `heightsen`<br>- `move`<br>- `plasma off`|Refer to Section 2.4, Robot Programming|
|7|Turn the Work button ON|Keep it ON during operation|
|8|Start automatic operation|Perform cutting|
|9|Monitor status|Important data is updated in real time|
|10|Complete the operation|Check cutting quality|

<br>

![Figure 3.1 Signal I/O and operation sequence between the plasma cutting system and controller](../_assets/interaction.png)

[__SOURCE](3-workflow/2-implement.md)
# 3.2 Executing Cutting

After all basic settings and teaching are complete, repeat the following procedure to perform cutting operations.

<br>

|Step|Description|Remarks|
|:--:|:--:|:--:|
|1|Turn on the robot controller and plasma cutting system|Check communication status|
|2|Turn the Work button ON||
|3|Check the values on the monitoring screen|Verify communication and plasma cutting system status|
|4|Turn the motors ON|Prepare for operation|
|5|Start automatic operation||
|6|Monitor status|Verify that important data is updated in real time|

[__SOURCE](4-additional/README.md)
# 4. Additional Functions

[__SOURCE](4-additional/1-manualout.md)
# 4.1 Manual Gas Output

Use this function before starting an actual cutting operation to check the gas supply lines and verify that gas pressure and flow match the cutting conditions. Each gas stage can be activated manually through the robot controller interface or Hypertherm gas console.

<br>

![Figure 4.1 Manual gas output buttons](../_assets/test_button.png)

<br>

(1) Manual Pre-flow Output  
  - Definition: A preliminary gas flow supplied immediately before the plasma arc starts. It purges air from inside the torch and helps ensure stable ignition.  
  - Purpose: Used to purge contaminants or moisture from the gas line before cutting. It also verifies that the pressure of the initial ignition gas, such as nitrogen or air, reaches the set value.  
  - Button operation: Turn the `Pre-flow Test` button ON to discharge gas.

(2) Manual Cut-flow Output  
  - Definition: The main cutting-gas flow that forms the high-energy plasma arc and blows away molten metal during cutting.  
  - Purpose: Verifies that the pressure and flow of the main gas, which determines final cut quality, match the cut chart. It can also test the flow capacity of the gas supply equipment, such as a tank, for long cutting operations.  
  - Button operation: Turn the `Cut-flow Test` button ON to discharge gas.

(3) Manual Pierce-flow Output  
  - Definition: Gas supplied at the moment the workpiece is pierced to protect torch consumables and control molten-metal spatter.  
  - Purpose: Checks in advance whether sufficient piercing pressure is available when cutting thick plate. It also helps identify possible consumable damage caused by sudden gas-pressure changes during piercing.  
  - Button operation: Turn the `Pierce Test` button ON to output pierce-flow gas.

<br>

{% hint style="info" %}
- Each button operates as a toggle. Its ON/OFF state is maintained after it is pressed.
- The three manual output buttons cannot be enabled simultaneously.
- After a test is selected, plasma pressures A and B and shield pressure S are displayed in the button area (unit: psi).
{% endhint %}

[__SOURCE](4-additional/2-monitoring.md)
# 4.2 Monitoring

To verify cutting-process stability and equipment status, the system sends internal power-supply data to the robot controller in real time. This lets the operator immediately identify abnormal equipment conditions and monitor the cutting operation.

Use the following menu path to select the plasma cutting monitoring panel:  
`[Window Control] - [F1: Select] - Plasma Cutting`

<br>

![Figure 4.2 Monitoring screen](../_assets/monitoring.png)

<br>

|Item|Description|State|
|:--:|:--:|:--:|
|Machine Motion|Cutting motion is permitted after piercing is complete|on/off|
|Ready for Start|Process ID setup is complete|on/off|
|Error / Code|Error state and error code|`-` (no error) /<br>error code|
|Process Ready|Indicates whether a process ID is set|on/off|
|Ohmic Contact|Torch contact with the workpiece|on/off|
|Remote Power Status|Power state of the plasma cutting system|on/off|
|Voltage|Voltage value (V)|~ V|
|Current|Current value (A)|~ A|
|Process ID|Process ID set in the plasma cutting system|#|
|Stand-off|Distance between the torch and workpiece|mm|

[__SOURCE](4-additional/3-checkplay.md)
# 4.3 Test Run

For ease of operation, the system provides an operation mode that performs actual cutting and a test mode that does not output a plasma arc.

<table>
  <thead>
    <tr>
      <th style="text-align: center;">Item</th>
      <th style="text-align: center;">Operation Mode</th>
      <th style="text-align: center;">Test Mode</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">Function</td>
      <td align="center">Performs actual cutting, marking, or gouging</td>
      <td align="center">Dry run</td>
    </tr>
    <tr>
      <td align="center">Setting</td>
      <td align="center">Automatic operation &amp; gun key ON</td>
      <td align="center">Not in operation mode</td>
    </tr>
    <tr>
      <td align="center">Output signals</td>
      <td align="center">Arc ON, Pierce ON</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td align="center" rowspan="3">Conditions</td>
      <td align="center">Plasma cutting system process ID set: O</td>
      <td align="center">Plasma cutting system process ID set: O</td>
    </tr>
    <tr>
      <td align="center">Cutting condition process ID match: O</td>
      <td align="center">Cutting condition process ID match: O</td>
    </tr>
    <tr>
      <td align="center">Ready for Start: O</td>
      <td align="center">Ready for Start: X</td>
    </tr>
    <tr>
      <td align="center">Wait</td>
      <td align="center">Machine Motion signal: O</td>
      <td align="center">Machine Motion signal: X</td>
    </tr>
  </tbody>
</table>

<br>

{% hint style="warning" %}
- If any condition in the Conditions row above is not satisfied, the corresponding error occurs.
- After outputting the arc, the `plasma on` command waits for the Machine Motion signal. If this signal is not received within the specified time, the plasma cutting system reports an error.
{% endhint %}

[__SOURCE](5-error/README.md)
# 5. Warnings and Errors

This chapter describes the main errors that may occur while using the plasma cutting function and explains how to correct them.

## Error List

|Type|Number|Error Name|Description|Corrective Action|
|:--:|:--:|:--|:--|:--|
|Error|E1563|Process ID Mismatch|The process ID currently set in the plasma cutting system does not match the process ID in the cutting condition.|Set the plasma cutting system process ID to the same ID as the cutting condition.|
|Error|E1564|Waiting for Plasma Cutting System Ready|The `plasma on` command cannot be executed because the plasma cutting system is not ready to start.|Set the process ID, and then verify that the Ready for Start signal is received from the plasma cutting system.|
|Error|E1565|Plasma Cutting System Process ID Not Set|A process ID has not been set in the plasma cutting system, or the set value is invalid.|Set a process ID appropriate for the cutting condition in the plasma cutting system.|
|Error|E1566|Plasma Cutting System EtherCAT Communication Failure|The plasma cutting slave cannot be found, or an EtherCAT SDO communication error occurred while sending cutting conditions.|Check the EtherCAT slave-node settings, cable connections, and communication status, and then retry.|
|Error|E1567|Hypertherm Plasma Cutting System Internal Error|An internal error signal was received from the Hypertherm plasma cutting system. The detailed error number sent by the plasma cutting system is displayed as `ErrCode`.|Check the displayed `ErrCode` and correct the error according to the Hypertherm plasma cutting system manual.|

<br>

{% hint style="info" %}
The `ErrCode` displayed with E1567 is the detailed error number received from the plasma cutting system, not an error number generated by the robot controller.
{% endhint %}
