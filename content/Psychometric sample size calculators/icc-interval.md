+++
date = '2025-12-22'
draft = false
title = 'ICC reliability interval estimation'
+++


{{< rawhtml >}}


<html>
<script src="https://cdn.jsdelivr.net/npm/jstat@latest/dist/jstat.min.js"></script>


<form name="ICCest">

<table style="font-family: arial;font-size: 11pt"> 
	<tr>
		<td>Expected ICC:</td> <td> <input name="ICC" type="number" value="0.8" min="0" max="1" step="0.01" value="0.80"></td>
	</tr>
	<tr>
		<td>Number of raters (<i>k</i>):</td>
		<td><input name="k" type="number" value="2" min="2" step="1"></td>
	</tr>
		<tr>
		<td>Confidence interval % (1 &#8211; <i>&alpha;</i>):</td>
		<td><input name="ci" type="number" value="95" min="0" max="100" step="1"></td>
	</tr>
	<tr>
		<td>Desired width of the confidence interval (<i>w</i>):</td>
		<td><input name="w" type="number" value="0.2" min="0" max="1" step="0.01"></td>
	</tr>
	<tr>
		<td><input type="button" "type="classic" value="Calculate sample size" onClick="Calculate_ICCest()"></td>
		<td><input type="reset" value="RESET"> </td>
	</tr>
	<tr>
		<td><b> Required sample size (<i>n</i>):</b></td> 
		<td> <input name="result" value="" type="number" readonly style="width: 100px"></td>
	</tr>
</table>
</p>

</form>

<script type="text/javascript">

function Calculate_ICCest() 
	{
	// Input
	icc=Number(document.ICCest.ICC.value);
	k=Number(document.ICCest.k.value);
	w=Number(document.ICCest.w.value);
	ci=Number(document.ICCest.ci.value/100);
	
	// Calculation
	z=jStat.normal.inv(ci + (1 - ci)/2, 0, 1);
	res=Math.ceil( (8*(z**2)*((1-icc)**2)*((1+(k-1)*icc)**2))/(k*(k-1)*w**2) + 1 );
		
	//Result
	document.ICCest.result.value=res;
	}

</script>

<table style="font-family: arial;font-size: 11pt">  
	<tr> 
		<td>
		Approximate number of subjects required to obtain an exact confidence interval of the desired width for an intraclass correlation coefficient (ICC) in one-way and two-way ANOVA models. Power (1 &#8211; <i>&beta;</i>) fixed at 0.80. 
		<p>
		Can be used to estimate the required approximate sample size (<i>n</i>) for inter-rater or test-retest reliability studies. For example: for a reliability study with two raters (or two repeated measurements) and an expected ICC value of 0.8, 51 subjects are needed to obtain a desired width of 0.2 (i.e., the value of ICC is between 0.7 and 0.9) for the 95% confidence interval.
		<br><br><i>Note:</i> for <i>k</i> = 2 and ICCs &#8805; 0.7, the approximate sample size tends to slightly diverge from the correct sample size (<i>n</i><sub>c</sub>). In these special cases the accuracy can be considerably improved by adding (5 * ICC) to the approximate sample size. In the example above: <i>n</i><sub>c</sub> = 51 + (5 * 0.8) = 55.
		<p><b>Reference:</b>
		<br>
		Bonett DG. Sample size requirements for estimating intraclass correlations with desired precision. Stat Med. 2002;21(9):1331-5.</td>
	</tr>
</table>

<br>

</html>



{{< /rawhtml >}}