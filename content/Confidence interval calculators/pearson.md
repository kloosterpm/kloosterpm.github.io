+++
date = '2025-12-21T13:34:02+01:00'
draft = false
title = 'Confidence Intervals for Pearson Correlation'
weight = 1
+++


{{< rawhtml >}}


<form name="rest">

<table>

	<tr>
		<td>Observed Pearson correlation (<i>r</i>):</td> 
		<td><input name="r" type="number" value="0.657" min="-1" max="1" step="0.01"></td> 
	</tr>
	<tr>
		<td>Sample size (<i>n</i>):</td> 
		<td> <input name="n" type="number" value="15" min="0" max="999999" step="1"></td>
	</tr>
	<tr>
		<td>Confidence interval (CI): </td> 
		<td><select name="ci" id="ci">
			<option value="1.28">80%</option>
			<option value="1.44">85%</option>
			<option value="1.64">90%</option>
			<option value="1.96" selected="selected">95%</option>
			<option value="2.58">99%</option>
			</select></td>
	</tr>
	<tr>
		<td><input type="button" value="Calculate confidence interval" onClick="Calculate_rest()"></td>
		<td><input type="reset" value="RESET"></td> 
	</tr>
	
<tr>
  <td><b>Approximate confidence interval:</b></td>  
  <td style="white-space: nowrap;">
    <input name="result1" type="number" readonly>
    to
    <input name="result2" type="number" readonly>
  </td>
</tr>




</table>
</p>

</form>

<script type="text/javascript">

function Calculate_rest() 
	{
	// Input
	r=Number(document.rest.r.value);
	n=Number(document.rest.n.value);
	ci=Number(document.rest.ci.value);
	
	// Calculation
	z=(0.5*Math.log((1.0+r)/(1.0-r)))
	se=1/Math.sqrt(n-3);
	
	llz=(z - (ci*se)); 
	ulz=(z + (ci*se));
	
	llr=(Math.pow(Math.E, (2.0*llz))-1.0)/(Math.pow(Math.E, (2.0*llz))+1.0);
	ulr=(Math.pow(Math.E, (2.0*ulz))-1.0)/(Math.pow(Math.E, (2.0*ulz))+1.0);	

	
	
	res1=llr;
	res2=ulr;
	
	//Result
	document.rest.result1.value=res1.toFixed(5);
	document.rest.result2.value=res2.toFixed(5);
	}

</script>

<table> 
	<tr> <td> 
	Approximate confidence intervals for an observed Pearson <i>r</i> correlation, given the value of <i>r</i> and the sample size <i>n</i>. 
	For example: for an observed correlation of 0.657 and a sample size of 15, the 95% confidence interval ranges from 0.22 to 0.87. 
	<br><br>
	<i>Note:</i> Confidence intervals are based on Fisher&#8217;s <i>r</i> to <i>z</i> transformation.
	</p>
	<p>
	<b>References:</b>
	<br>
	Olkin I, Finn JD. Correlations Redux. Psychol Bull. 1995;118(1):155–64. 
	<br>
	Cohen J, Cohen P, West SG, Aiken LS. Applied multiple regression/correlation analysis for the behavioral sciences. Third edition. Mahwah, NJ: Lawrence Erlbaum Associates; 2003.
	</p>
	</td></tr>
</table>
</font>













{{< /rawhtml >}}