+++
date = '2025-12-21T13:34:02+01:00'
draft = false
title = 'Confidence intervals for differences between independent R-squares'
weight = 4
+++


{{< rawhtml >}}


<form name="rsquareest">


<table>  
	<tr>
		<td>Observed R-square (<i>R</i><sup>2</sup>):</td> 
		<td><input name="rsquare" type="number" value="0.5032" min="0" max="1" step="0.01"></td> 
	</tr>
	<tr>
		<td>Number of predictors <i>(k)</i>:</td> 
		<td><input name="k" type="number" value="4" min="1" step="1"></td>
	</tr>
	<tr>
		<td>Sample size (<i>n</i>):</td>
		<td><input name="n" type="number" value="62" min="0" max="999999" step="1"></td>
	</tr>
	<tr>
		<td>Confidence interval (CI):</td>
		<td><select name="ci" id="ci2">
			<option value="1.28">80%</option>
			<option value="1.44">85%</option>
			<option value="1.64">90%</option>
			<option value="1.96" selected="selected">95%</option>
			<option value="2.58">99%</option>
			</select></td>
	</tr>
	<tr>
		<td><input type="button" "type="classic" value="Calculate confidence interval" onClick="Calculate_rsquareest()"></td>
		<td><input type="reset" value="RESET"></td> 
	</tr>
	<tr>
		<td><b>Approximate confidence interval:</b></td>  
		<td><input name="result1" value="" type="number" readonly> to <input name="result2" value="" type="number" readonly> </td>
	</tr>

</table>
</p>

</form>

<script type="text/javascript">

function Calculate_rsquareest() 
	{
	// Input
	rsquare=Number(document.rsquareest.rsquare.value);
	k=Number(document.rsquareest.k.value);
	n=Number(document.rsquareest.n.value);
	ci=Number(document.rsquareest.ci2.value);
	
	// Calculation
	sesqrt=((4*rsquare)*((1-rsquare)**2)*((n-k-1)**2)) / ((n**2-1)*(n+3));
	se=Math.sqrt(sesqrt)
	ll=(rsquare - (ci*se)); 
	ul=(rsquare + (ci*se));
	
	
	res1=ll;
	res2=ul;
	
	//Result
	document.rsquareest.result1.value=res1.toFixed(5);
	document.rsquareest.result2.value=res2.toFixed(5);
	}

</script>

<table>  
	<tr> 
		<td>Approximate confidence intervals for an R-square value in a multiple linear regression model, given the value of R-square, the number of predictors, and the total sample size. For example: for an observed R-square of 0.5032, 4 predictors and a total sample size of 62, the 95% confidence interval ranges from 0.35 to 0.66.
		<br><br>
		<i>Note: </i>Confidence intervals are based on large sample theory. Provides adequate approximations for models with >60 degrees of freedom (<i>n</i> &#8211; <i>k</i> &#8211; 1).
		<p>
		<b>References:</b>
		<br>
		Olkin I, Finn JD. Correlations Redux. Psychol Bull. 1995;118(1):155–64. <br>
		Cohen J, Cohen P, West SG, Aiken LS. Applied multiple regression/correlation analysis for the behavioral sciences. Third edition. Mahwah, NJ: Lawrence Erlbaum Associates; 2003.</td>
	</tr>
</table>
<br>
</body>










{{< /rawhtml >}}