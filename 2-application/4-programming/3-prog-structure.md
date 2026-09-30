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
