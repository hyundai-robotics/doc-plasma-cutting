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
