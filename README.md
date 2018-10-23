# NPP4R
Notepad++ Settings for R Code. 

1) How to avoid language extension conflict with REBOL.
2) How to enable function list for R code

.R Extension Conflict

The language of REBOL also uses .R or .r as file extension. And it seems that Notepad++ gives a higher prioirty to REBOL. As a result, .R or .r file is intpreted as REBOL by default. To address this issue, the langs.xml file needs to be changed. This file is in C:\Users\[Your Windows User Name]\AppData\Roaming\Notepad++ folder on Windows platform. And a template copy is also in the NPP installation folder such as C:\Program Files\Notepad++.  Just remove the "r" extension from the REBOL record. 

Change the line 
<Language name="r rebol" ext="reb" commentLine=";" commentStart="" commentEnd="">
to 
<Language name="rebol" ext="reb" commentLine=";" commentStart="" commentEnd="">
  
 
R function list

At the same folder, you can find functionList.xml. Add the following parser to the file.

<!-- ========================================================= [ R ] -->
<!-- R - R class and function parser: experimental by Shipeng Sun    -->
<!-- Revised from the JavaScript function parser below.              -->
<parser
		id         ="r_function"
		displayName="R"
		commentExpr="(?x)                                           # Utilize inline comments (see `RegEx - Pattern Modifiers`)
								(?m-s:\#.*?$)                                   # Single Line Comment
							"				
>
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
