# TransactionFeeSchedule

The fees for a specific transaction or query based on the fee data.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>hederaFunctionality</code>
      </td>
      <td style="text-align:left">&#x200B;<a href="hederafunctionality.md">HederaFunctionality</a>&#x200B;</td>
      <td
      style="text-align:left">A particular transaction or query</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>feeData</code>
      </td>
      <td style="text-align:left">&#x200B;<a href="feedata.md">FeeData</a>&#x200B;</td>
      <td style="text-align:left">
        <p>Resource price coefficients</p>
        <p>[deprecated]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>fees</code>
      </td>
      <td style="text-align:left">repeated <a href="feedata.md">FeeData</a>
      </td>
      <td style="text-align:left">Resource price coefficients. Supports subtype price definition</td>
    </tr>
  </tbody>
</table>

####  <a id="undefined"></a>

