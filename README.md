# NPP4R
Notepad++ Settings for R Code. 

1) How to avoid language extension conflict with REBOL.
2) How to enable function list for R code

# .R Extension Conflict

The language of REBOL also uses .R or .r as file extension. And it seems that Notepad++ gives a higher prioirty to REBOL. As a result, .R or .r file is intpreted as REBOL by default. To address this issue, the langs.xml file needs to be changed. This file is in ```C:\Users\[Your Windows User Name]\AppData\Roaming\Notepad++``` folder on Windows platform. And a template copy is also in the NPP installation folder such as ```C:\Program Files\Notepad++```.  Just remove the "r" extension from the REBOL record. 

Change the line 
```<Language name="r rebol" ext="reb" commentLine=";" commentStart="" commentEnd="">```
to 
```<Language name="rebol" ext="reb" commentLine=";" commentStart="" commentEnd="">```
  
 
# R function list

Although popular R IDE like RStudio can maintain a function list for R, the list is below a long list of global and local variables. Notepad++ provides a much cleaner environment for R function coding. It is much more easier to navigate a large R function definition file in Notepad++. However, Notepad++ does not provide a REGEX parser for R functions.  In the same folder as the aboved mentioned langs.xml, there is a file functionList.xml. Add the following parser to that file. This parser uses REGEX to find R function definitions and adds the full function declaration to the function list.
```
<!-- ========================================================= [ R ] -->
<!-- R - R class and function parser: experimental by Shipeng Sun    -->
<!-- Revised from the JavaScript function parser below.              -->
<parser id ="r_function" displayName="R" commentExpr="(?x)(?m-s:\#.*?$)">
	<function
		mainExpr="((^|\s+|[;\}\.])([A-Za-z_$][\w$]*\.)*[A-Za-z_$][\w$]*\s*([\<][\-]|[=:])|^|[\s;\}]+)\s*function(\s+[A-Za-z_$][\w$]*)?\s*\([^\)\(]*\)[\n\s]*\{"
	>
		<functionName>
			<nameExpr expr="(([A-Za-z_$][\w$]*\s*([\<][\-]|[=:]))|([A-Za-z_$][\w$]*))\s*function(\s+[A-Za-z_$][\w$]*)?\s*\([^\)\(]*\)[\n\s]*" />
			<!-- Enable the following one if only function names are displayed. -->
			<!--nameExpr expr="[A-Za-z_$][\w$]*" /-->
		</functionName>
	</function>
</parser>
```

And an association record for R functions.

```
<association id="r_function" langID="54" />
```
These two files are available for download from this repository. And if everything works out fine, you should be able to see something like this.

![R Functions in Notepad++](./NPP_R_function_list.png?raw=true "R Function List in Notepad++")


