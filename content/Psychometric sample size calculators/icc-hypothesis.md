+++
date = '2025-12-21T13:34:02+01:00'
draft = false
title = 'ICC reliability hypothesis testing'
+++


{{< rawhtml >}}


<html>
<script src="https://cdn.jsdelivr.net/npm/jstat@latest/dist/jstat.min.js"></script>


<form name="ICChyp">

<table style="font-family: arial;font-size: 11pt"> 
	<tr>
		<td>Expected ICC:</td> 
		<td> <input name="ICC1" type="number" value="0.8" min="0" max="1" step="0.01"></td>
	</tr>
	<tr>
		<td>Minimum acceptable ICC:</td>
		<td><input name="ICC0" type="number" value="0.6" min="0" max="1" step="0.01"></td>
	</tr>
	<tr>
		<td>Number of raters (<i>k</i>):</td>
		<td><input name="k" type="number" value="2" min="2" max="9999" step="1"></td>
	<tr>
		<td>Desired power (1 &#8211; <i>&beta;</i>):</td>
		<td><input name="power" type="number" value="0.8" min="0" max="1" step="0.01"></td>
	</tr>
	<tr>
		<td>Significance level (&alpha;, two-sided):</td>
		<td><input name="alpha" type="number" value="0.05" min="0" max="1" step="0.01"></td>
	</tr>
	<tr>
		<td><input type="button" value="Calculate sample size" onClick="Calculate_ICChyp()"></td>
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

function Calculate_ICChyp() 
	{
	// Input
	icc1=Number(document.ICChyp.ICC1.value);
	icc0=Number(document.ICChyp.ICC0.value);
	k=Number(document.ICChyp.k.value);
	power=Number(document.ICChyp.power.value);
	alpha=Number(document.ICChyp.alpha.value);
	
	// Calculation
	z_alpha = jStat.normal.inv(1 - alpha/2, 0, 1);
    z_beta = jStat.normal.inv(power, 0, 1);
    theta0 = icc0/(1-icc0);
    theta = icc1/(1-icc1);
	C0 = (1 + k*theta0)/(1 + k*theta);
		
	res=Math.ceil( 1 + (2*((z_alpha + z_beta)**2)*k) / (((Math.log(C0))**2)*(k-1)) );
			
	//Result
	document.ICChyp.result.value=res;
	}

</script>

<table style="font-family: arial;font-size: 11pt">  
	<tr>	<td>
		Approximate number of subjects required to test an intraclass correlation coefficient (ICC) in a one-way ANOVA model with desired power.  
		<br><br>
		Can be used to estimate the required approximate sample size (<i>n</i>) for inter-rater or test-retest reliability studies. For example: for a reliability study with two raters (or two repeated measurements), an expected ICC value of 0.8 and a desired power of 0.8 (80%), 49 subjects are needed to demonstrate that this ICC value is significantly different from a minimum acceptable ICC value of 0.6 at a two-tailed significance level of 0.05.
		<br><br><i>Note:</i> In most cases a one-sided hypothesis test will make more sense. For a one-tailed hypothesis test, multiply the desired significance level by two (e.g., <i>&alpha;</i> = 0.05 * 2 = 0.1). In the example above, for a one-tailed test the required sample size is 39 subjects).
		<p>
		<b>Reference:</b>
		<br>Walter SD, Eliasziw M, Donner A. Sample size and optimal designs for reliability studies. Stat Med. 1998;17(1):101-10.</td>
	</tr>
</table>


</html>




{{< /rawhtml >}}