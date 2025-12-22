+++
date = '2025-12-21T13:34:02+01:00'
draft = false
title = 'Pearson’s r interval estimation'
+++


{{< rawhtml >}}


<html>


<form name="rest">

<table style="font-family: arial;font-size: 11pt"> 
	<tr>
		<td>Expected correlation:</td> <td> <input name="cor" type="number" value="0.8" min="0" max="1" step="0.01" value="0.80"></td>
	</tr>
	<tr>
		<td>Number of control variables:</td> <td> <input name="s" type="number" value="0" min="0" max="9999" step="1"></td>
	</tr>
	<tr>
		<td>Significance level (for 1 &#8211; <i>&alpha;</i> confidence interval):</td> <td> <input name="alpha" type="number" value="0.05" min="0" max="1" step="0.01"></td>
	</tr>
	<tr>
		<td>Desired width of the confidence interval (<i>w</i>):</td> <td> <input name="w" type="number" value="0.2" min="0" max="1" step="0.01"></td>
	</tr>
	<tr>
		<td><input type="button" value="Calculate sample size" onClick="Calculate_rest()"></td>
		<td><input type="reset" value="RESET"></td>
	</tr>
	<tr>
		<td><b>Required sample size (<i>n</i>):</b></td>
		<td><input name="result" value="" type="number" readonly></td>
	</tr>
</table>
</p>

</form>

<script type="text/javascript">

function Calculate_rest() 
	{
	// Input
	cor=Number(document.rest.cor.value);
	s=Number(document.rest.s.value);
	alpha=Number(document.rest.alpha.value);
	w=Number(document.rest.w.value);

	// Calculation
	z=jStat.normal.inv(1 - alpha/2, 0, 1);
	n1=Math.ceil(4*(1 - cor**2)**2 * (z/w)**2 + s + 3);
	zr=Math.log((1 + cor)/(1 - cor))/2;
	se=Math.sqrt(1/(n1 - s - 3));
	ll0=zr - (z*se);
	ul0=zr + (z*se);
	ll=(Math.exp(2*ll0) - 1) / (Math.exp(2*ll0) + 1);
	ul=(Math.exp(2*ul0) - 1) / (Math.exp(2*ul0) + 1);

	res=Math.ceil((n1 - s - 3)*((ul - ll)/w)**2 + 3 + s);

		
	//Result
	document.rest.result.value=res;
	}

</script>

<table style="font-family: arial;font-size: 11pt">  
	<tr>
		<td>Approximate number of subjects required to obtain a confidence interval of the desired width for a planning estimate of the population (partial) Pearson correlation coefficient (<i>r</i>). 
		Significance level (<i>&alpha;</i>) = 0.05 translates to a 95% confidence interval, <i>&alpha;</i> = 0.01 to a 99% confidence interval. 
		<br><br>Can be used to estimate the sample size (<i>n</i>) required to test a hypothesis regarding the planned value of a Pearson correlation with desired power. For example: for an expected Pearson <i>r</i> of 0.8, 56 subjects are needed to obtain a desired 95% confidence interval width of 0.2 (i.e., the value of Pearson <i>r</i> is between 0.7 and 0.9).
		<br><br><b>Reference:</b>
		<br>
		Bonett DG, Wright TA. Sample size requirements for estimating Pearson, Kendall and Spearman correlations. Psychometrika. 2000;65(1):23-28.</td>
	</tr>
</table>

<br>


</html>



{{< /rawhtml >}}