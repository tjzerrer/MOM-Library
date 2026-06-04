# MyOpenMath Codex Reference

This file summarizes the MyOpenMath documentation for use when generating, editing, or reviewing MyOpenMath problems in this repository.

Codex should use this file together with:

* `style-guide/MOM-style-guide.md`
* `standards/texas/algebra-1-teks-summary.md`
* working examples in `examples/working-problems/`

The goal is not to reproduce the full MyOpenMath documentation. The goal is to preserve the syntax, patterns, macros, and common pitfalls most important for creating reliable Algebra 1 MyOpenMath problems.

---

# 1. Basic MOM Question Structure

A MyOpenMath question is built from several parts.

## Main Parts

* **Description**: Internal description. Students do not see this.
* **Use Rights**: Controls who can use or modify the question.
* **License**: Permission license for the question.
* **Library Assignments**: Where the question is stored.
* **Question Type**: Number, calculated, multiple choice, multipart, drawing, function, etc.
* **Common Control**: Main code area. Defines variables, randomization, answers, feedback, graphs, tables, and behavior needed for both display and scoring.
* **Question Text**: HTML-based display shown to students. Can include variables from Common Control.
* **Detailed Solution**: Optional solution shown in answer key or popup written example.
* **Image Files**: Static images uploaded and assigned to variables.
* **Help Buttons**: Links or help resources shown below the question.
* **Accessible Alternative**: Used only when the original question cannot reasonably be made accessible.

## Repository Rule

For this repo, prefer placing almost all code in **Common Control** unless there is a clear reason not to.

Recommended file structure for each problem:

```text
common-control.txt
question-text.html
student-guide.html
notes.md
```

---

# 2. Basic Control Syntax

MOM control code is PHP-like.

Variables begin with `$`.

Examples:

```php
$a = 3
$b = 3*$a
$graph = showplot("x^2")
$n = rand(-5,5)
```

Common assignment types:

```php
$var = number
$var = calculation
$var = function
$var = randomizer
$var = string
$var = array
$var = boolean
```

## Variable Types

### Number

```php
$a = 15
$b = 3^2
```

### Array

Arrays are zero-indexed.

```php
$a = array(6,8,10)
$b = [6,8,10]
```

Access values like:

```php
$a[0]
$a[1]
```

### Associative Array

```php
$a = ['x'=>3, 'y'=>5]
$xval = $a['x']
```

### String

```php
$str = "hi there"
$frac = "2/3"
```

Strings are not numbers. A string such as `"3/4"` cannot be multiplied as a number unless evaluated or separately represented numerically.

### Boolean

```php
$flag = true
```

---

# 3. String Rules and Pitfalls

## Double Quotes Interpolate Variables

```php
$a = 3
$b = 5
$str = "What is $a/$b"
```

This becomes:

```text
What is 3/5
```

## Single Quotes Do Not Interpolate

```php
$str = 'What is $a/$b'
```

This stays literal.

## Negative Number Pitfall

If:

```php
$a = -4
$b = "$a^2"
```

then `$b` becomes:

```text
-4^2
```

This may not mean what you intend. Use parentheses when needed:

```php
$b = "($a)^2"
```

## Concatenation

Use `.` to join strings.

```php
$a = "string one "
$b = "string two"
$both = $a . $b
```

## Long Lines

Use `&` to continue a long code line.

```php
$questions = array("choice 1",&
"choice 2")
```

Use `&&` inside display strings to continue and insert an HTML line break.

```php
$showanswer = "Do this first. &&
Then do this."
```

This displays like:

```html
Do this first.<br/>Then do this.
```

---

# 4. Comments

Use `//` for comments.

```php
// This is a comment.
$a = rand(1,10) // inline comments are possible, but separate lines are cleaner
```

Repository preference:

* Use comments to explain non-obvious randomization and feedback logic.
* Do not over-comment obvious arithmetic.

---

# 5. Conditionals

## `where`

`where` repeats the previous assignment or code block until the condition is met.

Example:

```php
$a,$b = diffrands(-5,5,2) where ($a+$b!=0)
```

Important:

* MOM gives up after about 200 tries.
* Use `where` only when the condition has a reasonable chance of success.
* Ideally the condition should succeed at least about 10% of the time.
* Use fallback values when appropriate.

Fallback example:

```php
$a = rand(1,100) where (gcd($a,$b)==1) else ($a = 7)
```

Block example:

```php
{
  $a = rand(-5,-1)
  $b = rand(1,5)
} where ($a+$b !==0)
```

Block with fallback:

```php
{
  $a = rand(-5,-1)
  $b = rand(1,5)
} where ($a+$b !==0) else {
  $a = -3
  $b = 5
}
```

## `if`

Use `if` for conditional assignments.

```php
$a = rand(0,1)
$b = "sin(x)" if ($a==0)
$b = "cos(x)" if ($a==1)
```

Use `==` to test equality. A single `=` assigns a value and is usually wrong inside a condition.

Block form:

```php
$a = rand(0,1)
if ($a==0) {
  $b = 1
  $c = 2
}
```

Alternative block form:

```php
$a = rand(0,1)
{
  $b = 1
  $c = 2
} if ($a==0)
```

`elseif` and `else` are supported:

```php
$a = rand(0,5)
if ($a==0) {
  $b = 1
} elseif ($a==2) {
  $b = 3
} else {
  $b = 2
}
```

## Ternary Syntax

For simple if/else:

```php
$b = ($a > 0) ? "increasing" : "decreasing"
```

## `ifthen`

Friendlier alternative:

```php
$b = ifthen($a > 0, "increasing", "decreasing")
```

## `cases`

Use `cases` for several value-based branches.

```php
$a = rand(0,5)
$b = cases($a, [0, 2], ["AA", "BB"], "CC")
```

## Comparison Operators

```text
==    equal to
!=    not equal to
>     greater than
<     less than
>=    greater than or equal to
<=    less than or equal to
&&    and
||    or
isset($v) checks whether variable exists
```

---

# 6. Conditionals in Question Text

Question text can conditionally display blocks using `[if ...][/if]`.

Use this only for larger display blocks. For short text, define the string conditionally in Common Control instead.

Example:

```html
[if graphdispmode==0]
Given f(x)=$func, estimate f'(x) at x=$x. $answerbox
[/if]

[if graphdispmode>0]
$graph
Given the graph above, estimate f'(x) at x=$x. $answerbox
[/if]
```

Important:

* Do not include the `$` in the variable name inside `[if]`.
* Simple comparisons are allowed.
* Avoid complex expressions inside question-text conditionals.
* It is okay to put answerboxes inside conditionals if only one answerbox displays at a time.

---

# 7. Loops

## `for`

```php
for ($i=a..b) { action }
```

Example:

```php
$f = 0
for ($i=1..5) {
  $f = $f + $i
}
```

Array example:

```php
$a = rands(1,5,5)
$b = rands(1,5,5)
for ($i=0..4) {
  $c[$i] = $a[$i]*$b[$i]
}
```

## `foreach`

Use for associative arrays.

```php
$arr = ['red' => 3, 'green' => 5, 'blue' => 2]

$str = ''
foreach ($arr as $color=>$num) {
  $str .= "There are $num balls that are $color. "
}
```

## `where` as Loop

```php
{
  $a = rand(1,10)
  $b = rand(-10,-1)
} where ($a+$b != 0)
```

## `while`

```php
$index = 0
$a = $str[$index]
while ($a == '') {
  $index = $index + 1
  $a = $str[$index]
}
```

## Loop Pitfall

This works:

```php
for ($i=1..5) {$a = $a+$i if ($i>2) }
```

This does not work:

```php
for ($i=1..5) {$a = $a+$i} if ($a>2)
```

Use explicit blocking:

```php
{for ($i=1..5) {$a = $a+$i} } if ($a>2)
```

`break` and `continue` work inside loops.

---

# 8. Randomizers

All randomizer bounds are inclusive.

## Single-Result Randomizers

```php
rand(min,max)
rrand(min,max,p)
nonzerorand(min,max)
nonzerorrand(min,max,p)
randfrom(list or array)
randname()
randmalename()
randfemalename()
randnamewpronouns([option])
uniqid()
```

Examples:

```php
$a = rand(-5,5)
$b = rrand(2,5,.1)
$c = nonzerorand(-9,9)
$d = randfrom("2,4,6,8")
```

`randnamewpronouns()` returns:

```php
$name,$heshe,$himher,$hisher,$hishers,$himherself = randnamewpronouns()
```

Use neutral pronouns:

```php
$name,$heshe,$himher,$hisher,$hishers,$himherself = randnamewpronouns('neutral')
```

`uniqid()` is useful for giving unique IDs to HTML elements.

## Array Randomizers

```php
rands(min,max,n,[order])
rrands(min,max,p,n,[order])
nonzerorands(min,max,n,[order])
nonzerorrands(min,max,p,n,[order])
randsfrom(list/array,n,[order])
jointrandfrom(list/array,list/array,[list/array,...])
diffrands(min,max,n,[order])
diffrrands(min,max,p,n,[order])
diffrandsfrom(list/array,n,[order])
nonzerodiffrands(min,max,n,[order])
nonzerodiffrrands(min,max,p,n,[order])
jointshuffle(list/array1,list/array2,[n1,n2])
singleshuffle(list/array,[n])
randnames(n)
randmalenames(n)
randfemalenames(n)
randcity([country])
randcities(n,[country])
randstate([country])
randstates(n,[country])
randcountry()
randcountries(n)
randpythag([min,max])
```

Ordering can be:

```text
'inc'
'dec'
```

But sorted random arrays can still contain duplicate values unless the macro specifically says different.

Use `diffrands` or `diffrandsfrom` when values must be unique.

---

# 9. Tables and Graphs

## Table Macros

### `showarrays`

Creates a table from arrays.

```php
$table = showarrays("x",$xvals,"y",$yvals)
```

Alternative form:

```php
$table = showarrays($headers, $dataarrays, $options)
```

Options may include alignment and caption.

```php
$opts["align"] = "c"
$opts["tablealign"] = "center"
$opts["caption"] = "Table title"
```

Use alignment strings like:

```text
"rcc"
```

to align each column differently.

### `showdataarray`

Displays one array, optionally over multiple columns.

```php
$table = showdataarray($data)
$table = showdataarray($data,3)
```

### `horizshowarrays`

Displays arrays as rows. Use only for small data sets because it does not text wrap well.

### `showrecttable`

Creates a 2x2 table.

```php
$table = showrecttable($data,$columnlabels,$rowlabels)
```

---

# 10. `showplot`

Basic syntax:

```php
$graph = showplot(funcstrings,[xmin,xmax,ymin,ymax,labels,grid,width,height])
```

`funcstrings` may be a single string or an array.

Basic function string format:

```text
function,color,min,max,startmarker,endmarker,width,dash
```

Examples:

```php
$graph = showplot("cos(x),red")
$graph = showplot("x^2,,-2,2,open,closed")
$graph = showplot("[t^2,t/3],blue,0,5,,,2,dash")
$graph = showplot("1/x,black,-5,5!0")
$graph = showplot("x=1,red,,,,,,dash")
```

## Function Part

Can be:

* a function of `x`, such as `cos(x)`
* a parametric function of `t`, such as `[sin(t),cos(t)]`
* a vertical line, such as `x=1`

## Colors

Supported colors include:

```text
black, red, orange, yellow, green, blue, purple
```

## Markers

Start and end markers can be:

```text
open
closed
arrow
none/blank
```

## Dashed Lines

Use `dash` in the final field.

## Excluding Discontinuities

Use `!` inside the min/max part.

```php
"1/x,black,-5,5!0"
```

means graph from -5 to 5 excluding 0.

---

# 11. Dots and Labels in `showplot`

## Dots

Format:

```text
dot,x,y,style,color,label,labelloc
```

Examples:

```php
"dot,3,4"
"dot,1,1,open"
"dot,3,3,,blue,A"
```

Style:

```text
open
closed
```

Label locations include:

```text
above, below, left, right, aboveleft
```

## Text Labels

Format:

```text
text,x,y,label,color,location,angle,graphassoc
```

Examples:

```php
"text,2,4,Cars"
"text,4,0,Hours,below"
```

`graphassoc` links the label to a graph for accessible alt text.

---

# 12. Graph Window and Labels

`showplot` arguments:

```php
showplot(funcstrings,xmin,xmax,ymin,ymax,labels,grid,width,height)
```

Defaults:

```text
xmin = -5
xmax = 5
ymin = -5
ymax = 5
labels = 1
grid = 1
width = 200
height = 200
```

Use `"off"` or `0` for no labels or no grid.

Different x/y label spacing:

```text
"xlbl:ylbl"
```

Axis names:

```text
"xlbl:ylbl:xname:yname"
```

Different x/y grid spacing:

```text
"xgrid:ygrid"
```

First-quadrant-style spacing trick:

```text
"0:-n"
```

for xmin or ymin. This keeps grid labels after 0 while still using negative spacing.

---

# 13. Graph Helper Macros

```php
mergeplots($plot1,$plot2,...)
invertplot($plot)
addfractionaxislabels(plot,step,[axis])
addlabel(plot,x,y,label,[color,loc,angle,size,alt])
addlabelabs(plot,x,y,label,[color,loc,angle,alt])
addplotborder(plot,left,[bottom,right,top])
adddrawcommand(plot,commands)
showasciisvg(string,[width,height,alttext])
replacealttext(image or graph, alttext)
changeimagesize(image or graph,width,[height])
textonimage(img,text,left,top,...)
addimageborder(image,[border width,margin])
arraystodoteqns(xarray,yarray,[color])
connectthedots(xarray,yarray,[color,thickness,startmarker,endmarker])
arraystodots(xarray,yarray)
getsnapwidthheight(xmin,xmax,ymin,ymax,drawing width,drawing height,snaptogrid)
```

Repository rules:

* Prefer `showplot`, `connectthedots`, `arraystodoteqns`, and `replacealttext` for generated graphs.
* Avoid raw `showasciisvg` unless necessary.
* Always provide useful alt text for graphs or images.
* If using `invertplot`, manually replace alt text because auto-generated alt text may become inaccurate.

---

# 14. Drawing-Question Data Macros

Use these to extract student-created drawing data.

```php
gettwopointlinedata(stuans,[window/size args])
gettwopointdata(stuans,type,[window/size args])
gettwopointformulas(stuans,type,[window/size args])
getdotsdata(stuans,[window/size args])
getopendotsdata(stuans,[window/size args])
getlinesdata(stuans,[window/size args])
getineqdata(stuans,[type/window/size args])
```

Curve types for `gettwopointdata` and related macros include:

```text
line, lineseg, ray, parab, halfparab, horizparab, sqrt, cubic, cuberoot,
rational, exp, genexp, log, genlog, sin, cos, abs, vector, circle, ellipse
```

Special notes:

* For `parab`, the first point is the vertex and the second point is another point.
* For `genexp` and `genlog`, output may include asymptote information.
* `circlerad` can return center and radius.
* `ellipserad` can return center and radii.
* For `horizparab`, formulas may be in terms of `y`.
* For circle and ellipse, formulas may be implicit equations.

For Algebra 1, drawing macros are most useful for:

* graphing a line
* graphing inequalities
* plotting points
* drawing a system
* identifying a student-drawn line from two points

---

# 15. Formatting Macros

Use these for cleaner student-facing display.

```php
makepretty(string or array)
makeprettydisp(string or array)
polymakepretty(string)
polymakeprettydisp(string)
makexxpretty(string)
makexxprettydisp(string)
makepretynegative(string)
numtowords(number,[options])
fractowords(numerator,denominator,[options])
numtoroman(number,[uppercase])
prettyint(number)
prettyreal(number,decimals,[comma])
prettyreal_instring(string,decimals,[comma])
round_instring(string,[decimals])
prettysmallnumber(number,[space])
prettysigfig(number,sigfigs,[options])
prettysigfig_instring(string,sigfigs,[options])
makescinot(number,[decimals,format])
prettytime(value,informat,outformat)
dispreducedfraction(numerator,denominator,[doubleslash,variable])
makereducedfraction(numerator,denominator,[doubleslash,variable])
decimaltofraction(decimal,[format,maxden])
htmldisp(string,[variables])
formatcomplex(real,imag)
rawurlencode(string)
```

Important:

* `prettyint`, `prettyreal`, and similar macros return strings for display, not numbers for calculations.
* `dispreducedfraction` is good for `$showanswer`.
* `makereducedfraction(...,'parts')` can return reduced numerator and denominator as an array.
* `decimaltofraction` works only up to a maximum denominator, default 5000.
* Use `makexxpretty` carefully; it can sometimes produce unexpected output.
* `polymakepretty` is best for simple polynomials.

Repository preference:

* Use display macros for answer explanations.
* Use numerical variables for calculations.
* Do not calculate with display strings.

---

# 16. String Macros

```php
stringappend(value,string)
stringprepend(value,string)
today([format])
stringpos(needle,haystack)
stringlen(string)
stringclean(string,[mode])
substr(string,start,[length])
strtoupper(string)
ucfirst(string)
strtolower(string)
lcfirst(string)
substr_count(haystack,needle)
str_replace(search,replace,string)
preg_match(pattern,subject,[matches])
preg_match_all(pattern,subject,[matches,flags,offset])
preg_replace(pattern,replacement,subject,[limit])
```

`stringclean` modes:

```text
0 = trim leading/trailing whitespace
1 = remove all whitespace
2 = remove all non-alphanumeric characters
```

Use string macros for:

* checking student explanations
* cleaning user input
* building display strings
* creating feedback messages

---

# 17. Array Macros

```php
listtoarray(list,[tonum])
calclisttoarray(list)
explode(symbol,string)
arraytolist(array,[space])
joinarray(array,[symbol,ksort])
stringtoarray(string,[tonum])
fillarray(value,num,[start])
consecutive(min,max,[step])
arraysetvalues(array,keyarray,value/valuearray)
sortarray(list/array,[type,maxkey])
jointsort(array,array,...)
calconarray(array,calculation)
multicalconarray(calculation,varslist,var1array,var2array,...)
calconarrayif(array,calculation,ifcondition)
keepif(array,condition)
subarray(array,params)
splicearray(array,offset,length,[replacement])
mergearrays(array,array,...)
unionarrays(array,array)
intersectarrays(array,array)
diffarrays(array1,array2)
array_unique(array)
array_values(array)
array_keys(array)
count(array)
is_array(variable)
sumarray(array)
in_array(needle,haystack)
arrayfindindex(needle,haystack)
arrayfindindices(needle,haystack)
array_flip(array)
print_r(array,[return])
```

Important:

* `array_unique` does not re-index arrays. Use `array_values` after it if consecutive indexes are needed.
* `print_r($array,true)` can be used for debugging and displayed in question text if needed.
* `jointsort` is useful for sorting x-values and keeping y-values matched.
* `jointshuffle` is useful when shuffling choices while preserving pairings.
* `calconarray` and `multicalconarray` are useful for generating table values.

---

# 18. General Macros

```php
ifthen(condition,trueval,falseval)
cases(testvalue,comparearray,outputarray,[defaultoutput,tolerance])
formhoverover(label,tip)
formpopup(label,content,[width,height,style,scrollbars])
forminlinebutton(label,content,[style,outputstyle])
makenumberrequiretimes(array/list)
ABarray(start,num)
getntupleparts(string,[expected components,checknumeric])
scoremultiorder(stua,answer,swap,type,[weights,options])
scoreperiodic(answer,stuanswer,variable,[tolerance])
setupmathquillfillin(asciimath format, alt format)
```

Use cases:

* `ifthen`: simple conditional value
* `cases`: many possible outputs based on a value
* `formhoverover`: vocabulary hints
* `formpopup`: written examples or extra help
* `forminlinebutton`: reveal hidden content
* `makenumberrequiretimes`: require numbers to appear in a student answer
* `ABarray`: generate `[AB#]` answerbox placeholders
* `scoremultiorder`: allow answers to be correct in different orders
* `scoreperiodic`: help score equivalent periodic trig solution forms
* `setupmathquillfillin`: create fill-in blanks inside a static math expression

Repository preference:

* For Algebra 1, most common useful macros are `ifthen`, `cases`, `ABarray`, `makenumberrequiretimes`, `forminlinebutton`, and `scoremultiorder`.
* Avoid advanced macros unless the problem requires them.

---

# 19. Math Macros

```php
sin(t), cos(t), tan(t), sec(t), csc(t), cot(t)
arcsin(v), arccos(v), arctan(v), atan2(y,x)
abs(v)
sqrt(t), root(n)(t)
gcd(a,b,...)
lcm(a,b,...)
sign(a,[option])
sgn(a)
hexdec(a)
dechex(a)
v!
evalfunc(func,vars,val1,val2,...,[falseonerror])
evalnumstr(expr,[complex])
```

`sign(a,[option])`:

* default returns `1` or `-1`
* `true` returns `"+"` or `"-"`
* `"onlyneg"` returns `"-"` if negative, otherwise empty string

Use `evalfunc` to evaluate generated expressions.

Example:

```php
$val = evalfunc("x^2*y","x,y",2,3)
```

Use `evalnumstr` only when you have a string expression that must be evaluated.

Avoid using `evalnumstr` when direct calculation is possible.

---

# 20. Conditional Test Macros

```php
getstuans($stuanswers,$thisq,[part number])
stuansready($stuanswers,$thisq,array of part numbers,[anstypes,answerformat])
comparenumbers(a,b,[tol])
comparenumberswithunits(a,b,[tol])
comparecomplex(a,b,[tol])
comparentuples(a,b,[tol],[option])
comparefunctions(a,b,[vars,tol,domain])
comparesameform(a,b,[vars])
comparelogic(a,b,vars)
isset($var)
is_numeric(str)
are_numeric(v1,v2,...)
is_nan(val)
scorestring($answer,$showanswer,words,$stuanswers,$thisq,[partn,highlight])
checkanswerformat(string,answerformat)
getsigfigs(value,[expected sigfigs])
```

## Student Answer Safety

Use:

```php
getstuans($stuanswers,$thisq,part)
```

instead of directly accessing `$stuanswers[$thisq][part]` when possible.

Use:

```php
stuansready($stuanswers,$thisq,[0,1,2],$anstypes)
```

before using student answers in feedback or conditional display.

This prevents undefined-value errors.

## Tolerance

Many compare macros accept tolerance.

Relative tolerance:

```text
0.001
```

Absolute tolerance:

```text
|0.1
```

## Function Comparison

```php
comparefunctions($stu,$correct,"x",0.001,"-10,10")
```

Can restrict domain:

```text
"xmin,xmax"
"xmin,xmax,integers"
```

## Same Form

`comparesameform` is stricter than `comparefunctions`.

Use only when the exact form matters.

---

# 21. Feedback Macros

Feedback macros return strings that can be placed in question text.

## Basic Feedback

```php
getfeedbackbasic(correct msg, incorrect msg, $thisq, [partnum])
```

Multipart part example:

```php
$fb = getfeedbackbasic("Correct.", "Try again.", $thisq, 0)
```

For multiple parts:

```php
$fb = getfeedbackbasic("All correct.", "Check your work.", $thisq, [0,1])
```

## Multiple Choice Feedback

```php
getfeedbacktxt(stuans, feedbacktxt, ans)
```

Use with:

```php
$stu = getstuans($stuanswers,$thisq,0)
$feedback = getfeedbacktxt($stu,$feedbacktxt,$answer[0])
```

`$feedbacktxt` should align with `$questions`.

## Essay Feedback

```php
getfeedbacktxtessay(stuans, feedbacktxt)
```

This does not evaluate the response; it only checks that something was entered.

## Number Feedback

```php
getfeedbacktxtnumber(stuans, partialcredit, feedbacktxt, defaultfeedback, [tol])
```

Partial credit format:

```php
$partialcredit = array(wronganswer1,score1,wronganswer2,score2)
```

Scores range from 0 to 1.

## Calculated Feedback

```php
getfeedbacktxtcalculated(stuans, stuansval, partialcredit, feedbacktxt, defaultfeedback, [answerformat, requiretimes, tol])
```

Use `$stuanswersval` for calculated answers.

## Function Feedback

```php
getfeedbacktxtnumfunc(stuans, partialcredit, feedbacktxt, defaultfeedback, [vars, requiretimes, tol, domain])
```

Use for algebraic expression/equation answer types.

Repository preference:

* Define specific wrong-answer variables.
* Use feedback to identify likely misconceptions.
* Feedback should guide but not give the final answer too early.
* `$showanswer` gives full answer after the problem is complete.

---

# 22. Loading Other Macro Libraries

If the site has extra macro libraries installed, load them at the start of Common Control.

```php
loadlibrary("stats")
loadlibrary("stats,misc")
```

Only use external macro libraries if you know they are installed in the target MOM environment.

---

# 23. Math Entry

MOM uses ASCIIMath for math display.

In question text or display strings, wrap math in backticks.

```html
`x^2 + 3x - 4`
```

Useful calculation syntax:

```text
* / + -        arithmetic
^              powers
e, pi          constants
%              integer modulus
mod(p,n)       modulus with positive results for negatives
fmod(p,n)      decimal modulus
!              factorial
sqrt           square root
sin, cos, tan  trig functions
arcsin, etc.   inverse trig
ln             natural log
log            common log
abs            absolute value
round(n,d)     round to decimal places
roundsigfig(n,s)
floor, ceil
min, max
```

Use:

```php
sin(2)
```

not:

```php
sin 2
```

For display only, broader ASCIIMath and limited LaTeX are available.

---

# 24. Solver

The Solver can help solve, differentiate, integrate, plot, or simplify expressions while writing a question.

Useful Sage syntax examples:

```python
x,y,a,b,c,d = var('x,y,a,b,c,d')
solve(y==(a*x+b)/(c*x-d), x)
diff(3*x^4, x)
plot(-x^2+4, (x,-10,10))
simplify(5*x+7*(-3*x-4))
```

Repository note:

* Solver is useful during development but should not appear in final MOM code.
* Use it to verify formulas before saving them in `common-control.txt`.

---

# 25. Accessibility

Prefer making the original question accessible rather than using an alternative question.

Accessibility patterns:

* Add meaningful alt text to images and graphs.
* Use `replacealttext` for generated graphs.
* For non-interactive JSXGraph visuals, use description options.
* For visual-only content, consider hiding the visual from screen readers and adding a screen-reader-only text description.
* Use accessible alternatives only when the original cannot reasonably be made accessible.

Accessible alternative options include:

```text
visual alt
mouse alt
visual or mouse alt
```

Repository rule:

* Every graph, table, image, or diagram should have an accessibility note in `notes.md`.

---

# 26. Hints

For single-part questions:

```php
$hints[0] = "This will show on first display"
$hints[1] = "This will show after one missed attempt"
$hints[2] = "This will show on later attempts"
```

Place in question text:

```html
$hintloc
```

For multipart per-part hints:

```php
$hints[0][0] = "Hint for part 0 on first display"
$hints[0][1] = "Hint for part 0 after one missed attempt"
```

Place:

```html
$hintloc[0]
```

Conditional hint based on attempts or correctness on previous parts:

```php
$hints[2][1] = array("Use your answer from Part A.", [0,1])
```

Change hint label:

```php
$hintlabel = "Need help?"
```

---

# 27. Help Text

Define:

```php
$helptext = "Help resource or link goes here."
```

This appears at the bottom of the question and is controlled by the same assessment setting as hints.

---

# 28. Referencing Student Answers

Student answer variables:

```php
$stuanswers[N]
$stuanswers[N][P]
$stuanswers[$thisq][P]
$stuanswers[$thisq-1]
$stuanswersval[$thisq]
$stuanswersval[$thisq][P]
$stulastentry
$stulastentry[P]
```

Important notes:

* Questions are not zero-indexed when referencing question number: `N=1` means question 1.
* Multipart part indexes are usually zero-indexed.
* `$stuanswersval` contains numerical values for Calculated question types.
* `$stulastentry` can include autosaved entries before submission.
* If unanswered, `$stuanswers[N] === null`.
* Dropdowns may return `"NA"` when no selection is made.
* If null is used in an equation, it may behave like 0, which can create errors or exploits.

Safe pattern:

```php
$a = getstuans($stuanswers,$thisq,0)
if ($a===null) {
  $a = rand(1,100)
  $warning = "You must answer Part A before this part."
}
```

If using student answers in strings, use curly braces:

```php
$str = "Your answer was {$stuanswers[$thisq][0]}"
```

If using directly in calculations, use parentheses.

Repository rule:

* Use `getstuans` and `stuansready` whenever building feedback or conditional logic from student answers.
* Custom define `$showanswer` when using `$stuanswers` in answer logic.

---

# 29. Display-Only Reference Variables

These are available on display, not scoring.

```php
$scorenonzero[$thisq]
$scoreiscorrect[$thisq]
$attemptn
$partattemptn[part number]
$requestclearla
```

Common meanings:

* `$scorenonzero`: unanswered, zero, or above-zero score status
* `$scoreiscorrect`: unanswered, perfect, or not perfect
* `$attemptn`: current attempt number
* `$partattemptn`: attempt number by part

Use these for conditional feedback/display, not scoring.

---

# 30. Important Question Types for Algebra 1

The full documentation includes many question types. For this Algebra 1 repo, the most useful types are:

* Number
* Calculated
* Multiple Choice
* Multiple Answer
* Matching
* Function / Algebraic Expression
* String
* Essay
* Drawing
* N-Tuple / Calculated N-Tuple
* Interval / Calculated Interval
* Multipart
* Conditional

Less likely for Algebra 1:

* Chemical Equation
* Chemical Molecule Drawing
* File Upload
* Complex Matrix types
* Algebraic Matrix types

---

# 31. Number Question Type

Use when the expected answer is a fixed number.

Good for:

* slope
* intercept
* solution value
* rate of change
* simple numeric result

Common setup:

```php
$answer = 5
```

Use feedback macros such as:

```php
getfeedbacktxtnumber(...)
```

Use tolerances when appropriate.

---

# 32. Calculated Question Type

Use when the student may enter an equivalent numerical expression.

Good for:

* fractions
* decimals
* expressions like `3/4`
* calculated values with tolerance

Use `$stuanswersval` when checking calculated student responses.

Feedback:

```php
getfeedbacktxtcalculated(...)
```

Common options:

* `answerformat`
* `requiretimes`
* tolerance

Repository preference:

* Use Calculated instead of Number when students may enter equivalent numeric forms.
* Use `answerformat` if the answer must be a fraction, decimal, integer, etc.
* Use `requiretimes` when specific numbers or structures must appear.

---

# 33. Multiple Choice

Use when students choose one answer.

Typical variables:

```php
$questions = array("Choice A","Choice B","Choice C","Choice D")
$answer = 2
```

The answer is usually the index of the correct choice.

Use `getfeedbacktxt` for choice-specific feedback.

Repository preference:

* Shuffle choices when appropriate.
* Ensure choices are unique.
* Distractors should reflect real student errors.
* Avoid “all of the above” unless instructionally necessary.

---

# 34. Multiple Answer

Use when students select more than one correct answer.

Good for:

* identify all equivalent expressions
* identify all true statements
* select all functions
* select all points on a line

Repository preference:

* Use only when multiple selections are mathematically meaningful.
* Give clear instructions such as “Select all that apply.”
* Use targeted feedback carefully because many wrong combinations are possible.

---

# 35. Matching

Use when students pair items.

Good for:

* equations to graphs
* vocabulary to definitions
* forms of linear equations
* scenarios to function types

Repository preference:

* Keep matching sets short.
* Avoid ambiguous pairs.
* Use clear labels.

---

# 36. Function / Algebraic Expression Question Type

Use for algebraic expressions or equations.

Good for:

* writing equations
* writing functions
* equivalent expressions
* recursive or explicit formulas
* solving literal equations

Important options often include:

```php
$variables = "x"
$answer = "2x+3"
```

Use:

```php
comparefunctions(...)
```

for equivalence.

Use:

```php
comparesameform(...)
```

only when the exact form matters.

Use:

```php
$requiretimes
```

when the student answer must contain required components.

Repository preference:

* Be very clear whether students should enter the full equation or only the expression.
* For function answers, specify variables.
* For equations, test multiple equivalent forms if needed.
* Use wrong-answer detection for sign errors, reciprocal slope, missing intercept, and incorrect form.

---

# 37. String and Essay

Use sparingly.

Good for:

* short vocabulary answers
* explanation checks
* reasoning prompts
* written interpretation

Use:

```php
scorestring(...)
```

when checking for required words.

Repository preference:

* Avoid long written responses unless needed.
* For auto-graded explanations, define expected keywords carefully.
* Do not over-rely on string scoring for nuanced mathematical reasoning.

---

# 38. Drawing

Use when students draw on a graph.

Good for:

* graph a line
* graph a system
* graph an inequality
* place a point
* draw a parabola or exponential curve

Useful data extraction macros:

```php
gettwopointlinedata
gettwopointdata
gettwopointformulas
getdotsdata
getopendotsdata
getineqdata
```

Repository preference:

* Use consistent graph windows.
* Use snap-to-grid when possible.
* Provide clear graphing instructions.
* In feedback, distinguish between wrong point, wrong slope, wrong boundary type, and wrong shading.
* Always visually test drawing problems before using.

---

# 39. N-Tuple and Calculated N-Tuple

Use for ordered pairs or coordinate answers.

Good for:

* intersection points
* vertex
* x/y coordinate pairs
* systems solutions

Use:

```php
getntupleparts(...)
comparentuples(...)
```

Repository preference:

* Use N-Tuple for ordered-pair answers.
* Use Calculated N-Tuple if entries may be expressions.
* Clarify expected format, such as `(x,y)`.

---

# 40. Interval and Calculated Interval

Use for interval notation.

Good for:

* domain
* range
* solution sets
* inequalities

Repository preference:

* For Algebra 1, also consider using inequalities if interval notation is not expected.
* Be clear about union notation and endpoints.

---

# 41. Multipart

Use for scaffolded problems with multiple parts.

Typical setup:

```php
$anstypes = array("choices","number","calculated")
$answeights = array(.3,.3,.4)
$answer[0] = ...
$answer[1] = ...
$answer[2] = ...
```

Question text uses answerboxes such as:

```html
$answerbox[0]
$answerbox[1]
$answerbox[2]
```

or placeholders such as:

```html
[AB0]
[AB1]
[AB2]
```

Repository preference:

* Use multipart for scaffolded reasoning.
* Keep most multipart problems to 2–4 parts.
* Use part weights intentionally.
* Use per-part feedback when possible.
* Use gating/conditional display when later parts depend on earlier parts.
* `$showanswer` should address each part.

Example showanswer style:

```php
$showanswer = "
<div style='font-size:14pt; line-height:1.2;'>
  <div><strong>Answer:</strong></div>
  <div>Part A: ...</div>
  <div>Part B: ...</div>
  <div style='margin-top:6px;'><strong>Rationale:</strong></div>
  <div>...</div>
</div>";
```

---

# 42. Conditional Questions

Conditional questions let the displayed or scored parts depend on previous answers or variables.

Repository preference:

* Use cautiously.
* Prefer simple multipart gating when possible.
* Always test every branch.
* Avoid hiding required answerboxes accidentally.
* Make sure the scoring logic matches the displayed branch.

---

# 43. `$showanswer` Best Practices

Repository standard:

* `$showanswer` belongs in Common Control when possible.
* It should show the answer first.
* Then it should explain the rationale.
* Use 14pt font.
* Use color only when it clarifies mathematical relationships.
* Avoid large colored backgrounds.

Pattern:

```php
$showanswer = "
<div style='font-size:14pt; line-height:1.2;'>
  <div><strong>Answer:</strong> [answer here]</div>
  <div style='margin-top:6px;'><strong>Rationale:</strong> [reasoning here]</div>
</div>";
```

For multipart:

```php
$showanswer = "
<div style='font-size:14pt; line-height:1.2;'>
  <div><strong>Answer:</strong></div>
  <div>Part A: [answer]</div>
  <div>Part B: [answer]</div>
  <div>Part C: [answer]</div>
  <div style='margin-top:6px;'><strong>Rationale:</strong></div>
  <div>[explanation]</div>
</div>";
```

---

# 44. Codex Rules for Creating MOM Problems

When Codex creates a new MOM problem, it should:

1. Read the style guide first.
2. Identify the TEKS standard.
3. Choose the correct MOM question type.
4. Put main code in Common Control.
5. Keep question text HTML-based and compact.
6. Use 14pt font.
7. Use clean randomized values.
8. Avoid impossible or messy random cases.
9. Use `diffrands` or uniqueness checks when answer choices must be unique.
10. Use `where` only when success probability is high.
11. Use fallback values when `where` might fail.
12. Define all answers clearly.
13. Use targeted feedback for predictable wrong answers.
14. Use `$showanswer` with answer first, then rationale.
15. Use accessible alt text for graphs and images.
16. Test every problem branch.
17. For multipart problems, verify part indexes carefully.
18. For calculated answers, use `$stuanswersval` in feedback.
19. For student-answer-based feedback, use `getstuans` and `stuansready`.
20. Do not invent MOM macros. Use only confirmed macros from this reference or working examples.

---

# 45. Common MOM Pitfalls

## Syntax Pitfalls

* Using `=` instead of `==` in a condition.
* Forgetting that arrays are zero-indexed.
* Treating string fractions like `"3/4"` as numbers.
* Forgetting curly braces around array variables in strings.
* Not using parentheses around negative values in display strings.
* Using display-formatted strings in calculations.

## Randomization Pitfalls

* `where` condition too restrictive.
* Duplicate answer choices.
* Random values create division by zero.
* Random values create undefined slope when not intended.
* Random values create non-integer or messy answers when clean answers were intended.
* Different problem types not equally likely when equal distribution was intended.

## Graphing Pitfalls

* Labels cut off because border is too small.
* Auto-generated alt text is inaccurate after graph modification.
* Graph window does not show key points.
* Open/closed dots are wrong.
* Dashed/solid boundary is wrong for inequalities.
* Drawing dimensions and snap-to-grid do not align.

## Feedback Pitfalls

* Feedback reveals the correct answer too early.
* Feedback checks raw `$stuanswers` before confirming it exists.
* Calculated feedback uses `$stuanswers` instead of `$stuanswersval`.
* Multipart feedback references the wrong part index.
* Feedback text array does not align with `$questions`.

## Question Text Pitfalls

* Long vertical layout that does not fit Chromebook screens.
* Answerboxes hidden by conditional display.
* Missing `$hintloc` when hints are defined.
* Raw `<` and `>` should often be replaced with `&lt;` and `&gt;` in HTML contexts.
* Rich text editor may alter raw HTML; raw HTML should be checked carefully.

---

# 46. Recommended Repo Organization for MOM Documentation

Use this folder structure:

```text
docs/myopenmath/
  mom-codex-reference.md
  known-issues.md
  macros/
    graphing.md
    feedback.md
    randomizers.md
    formatting.md
    student-answers.md
  answer-types/
    calculated.md
    multiple-choice.md
    multipart.md
    function.md
    drawing.md
```

This file is the master summary. More detailed files can be added later as specific patterns are tested.

---

# 47. Minimum Testing Checklist for Every MOM Problem

Before a problem is considered finished:

* [ ] Question type is appropriate.
* [ ] Common Control runs without syntax errors.
* [ ] Question Text displays correctly.
* [ ] Font is 14pt.
* [ ] Layout is compact and Chromebook-friendly.
* [ ] All random branches display correctly.
* [ ] All randomized values produce valid answers.
* [ ] Answer choices are unique.
* [ ] Correct answer is scored correctly.
* [ ] Common wrong answers receive useful feedback.
* [ ] Feedback does not give away the answer too soon.
* [ ] `$showanswer` starts with the answer.
* [ ] `$showanswer` includes rationale.
* [ ] Graphs/tables/images have accessibility notes or alt text.
* [ ] Multipart part indexes are correct.
* [ ] Student guide exists if requested.
* [ ] TEKS alignment is documented in `notes.md`.

---

# 48. Best Default Choices for Algebra 1 MOM Problems

Use these defaults unless the problem requires something else.

## Font

```text
14pt
```

## Layout

```text
compact, Chromebook-friendly, table-based when calculator or graph is present
```

## Randomization

```text
clean values, avoid unnecessary decimals, avoid fragile where conditions
```

## Feedback

```text
targeted feedback after submit, based on likely student misconceptions
```

## Showanswer

```text
answer first, then rationale
```

## Graphs

```text
use showplot, provide alt text, visually test
```

## Tables

```text
use showarrays or HTML tables; keep small and readable
```

## Calculators

```text
use calculator only when it supports the intended skill
```

---

# 49. Important Reminder for Codex

When uncertain about MOM syntax:

1. Prefer a working example from this repository.
2. Prefer a macro listed in this reference.
3. Avoid inventing syntax.
4. Flag uncertainty in `notes.md`.
5. Keep the generated problem simple and testable.
