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
