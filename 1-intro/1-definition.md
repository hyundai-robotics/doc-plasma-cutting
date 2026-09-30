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
