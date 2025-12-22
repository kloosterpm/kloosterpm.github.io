+++
date = '2025-12-21T13:34:02+01:00'
draft = false
title = 'Confidence intervals for differences between independent Pearson correlations'
weight = 2
+++


{{< rawhtml >}}


<form name="rdiffest">


<table> 
	<tr>
		<td></td>
		<td><b>Sample 1</b></td>
		<td><b>Sample 2</b></td>
	</tr>
	<tr>
		<td>Observed Pearson correlation (<i>r</i>):</td> 
		<td> <input name="r1" type="number" value="0.657" min="0" max="1" step="0.01"></td>
		<td> <input name="r2" type="number" value="0.430" min="0" max="1" step="0.01"></td> 
	</tr>
	<tr>
		<td>Sample size (<i>n</i>): <td> <input name="n1" type="number" value="62" min="0" max="999999" step="1"></td>
		<td><input name="n2" type="number" value="143" min="0" max="999999" step="1"></td>
	</tr>
	<tr>
		<td>Confidence interval (CI):</td> 
		<td>	<select name="ci" id="ci">
			<option value="1.28">80%</option>
			<option value="1.44">85%</option>
			<option value="1.64">90%</option>
			<option value="1.96" selected="selected">95%</option>
			<option value="2.58">99%</option></select> </td>
		<td></td>
	</tr>
	<tr>
		<td><input type="button" "type="classic" value="Calculate confidence interval" onClick="Calculate_rdiffest()"></td>
		<td> <input type="reset" value="RESET"></td>
		<td></td> 
	</tr>
	<tr>
		<td><b>Difference between correlations:</b></td>  
		<td colspan="2"><input name="result1" value="" type="number" readonly></td> 
	</tr>
	<tr>
		<td><b>Approximate confidence interval of difference:</b></td>  
		<td colspan="2"><input name="result2" value="" type="number" readonly> to <input name="result3" value="" type="number" readonly> </td>
	</tr>

</table>
</p>

</form>

<script type="text/javascript">

function Calculate_rdiffest() 
	{
	// Input
	r1=Number(document.rdiffest.r1.value);
	n1=Number(document.rdiffest.n1.value);
	
	r2=Number(document.rdiffest.r2.value);
	n2=Number(document.rdiffest.n2.value);
	
	ci=Number(document.rdiffest.ci.value);
	
	
	// Calculation
	ser1=(1 - (r1**2)) / n1;
	
	ser2=(1 - (r2**2)) / n2;
		
	se=Math.sqrt((ser1 + ser2));
	
	rdif=(r1 - r2)
	
	ll=(rdif - (ci*se)); 
	ul=(rdif + (ci*se));
	
	res1=rdif;
	res2=ll;
	res3=ul;
	
		
	//Result
	document.rdiffest.result1.value=res1.toFixed(5);
	document.rdiffest.result2.value=res2.toFixed(5);
	document.rdiffest.result3.value=res3.toFixed(5);
	}

</script>

<table> 
	<tr> 
		<td>
		Approximate confidence intervals for a difference between two Pearson correlations in two independent samples, given the values of the correlations and the total sample sizes. 
		For example: for two observed correlations of 0.657 and 0.430 in samples 1 and 2 and sample sizes of 62 and 143, respectively, the 95% two-sided confidence interval for the difference between the correlations ranges from -0.012 to 0.466. 		Since this confidence interval includes zero, the difference between the correlations is not significant at the <i>&alpha;</i> = 0.05 level.
		<br><br>
		<i>Note:</i> Confidence intervals are based on large sample theory (central limit theorem). Provides adequate approximations only for large samples.
		<p>
		<b>References:</b>
		<br>
		Olkin I, Finn JD. Correlations Redux. Psychol Bull. 1995;118(1):155–64. <br>
		Cohen J, Cohen P, West SG, Aiken LS. Applied multiple regression/correlation analysis for the behavioral sciences. Third edition. Mahwah, NJ: Lawrence Erlbaum Associates; 2003.
		</td>
	</tr>
</table>


</body>

</html>













{{< /rawhtml >}}