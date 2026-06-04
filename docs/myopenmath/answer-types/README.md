# MyOpenMath Answer Types Reference

This file summarizes the MyOpenMath answer types most useful for Algebra 1 problem creation.

Codex should use this file when deciding which question type to use, especially for multipart problems.

Use this together with:

* `docs/myopenmath/mom-codex-reference.md`
* `style-guide/MOM-style-guide.md`
* `standards/texas/algebra-1-teks-summary.md`
* tested examples in `examples/working-problems/`

---

# 1. Main Rule for Codex

Before creating a MOM problem, choose the answer type based on what the student should actually enter or select.

Do not choose a question type only because it is easy to code.

## Best Default Choices for Algebra 1

| Student Task                                     | Best MOM Answer Type            |
| ------------------------------------------------ | ------------------------------- |
| Choose one answer                                | Multiple Choice                 |
| Choose more than one answer                      | Multiple Answer                 |
| Enter a simple exact number                      | Number                          |
| Enter a numeric expression, fraction, or decimal | Calculated                      |
| Enter an algebraic expression or equation        | Function / Algebraic Expression |
| Enter an ordered pair                            | N-Tuple or Calculated N-Tuple   |
| Enter domain/range in interval notation          | Interval or Calculated Interval |
| Draw a line, point, inequality, or graph         | Drawing                         |
| Answer multiple scaffolded parts                 | Multipart                       |
| Give a short written explanation                 | String or Essay                 |

---

# 2. MOM Short Names for Multipart Problems

In multipart problems, define the answer types using `$anstypes`.

Example:

```php
$anstypes = array("number","calculated","choices")
```

Common short names:

| Question Type                   | MOM Short Name        |
| ------------------------------- | --------------------- |
| Number                          | `"number"`            |
| Calculated                      | `"calculated"`        |
| Multiple Choice                 | `"choices"`           |
| Multiple Answer                 | `"multans"`           |
| Matching                        | `"matching"`          |
| Function / Algebraic Expression | `"numfunc"`           |
| Drawing                         | `"draw"`              |
| N-Tuple                         | `"ntuple"`            |
| Calculated N-Tuple              | `"calcntuple"`        |
| Algebraic N-Tuple               | `"algntuple"`         |
| Complex N-Tuple                 | `"complexntuple"`     |
| Calculated Complex N-Tuple      | `"calccomplexntuple"` |
| Matrix                          | `"matrix"`            |
| Calculated Matrix               | `"calcmatrix"`        |
| Complex Matrix                  | `"complexmatrix"`     |
| Calculated Complex Matrix       | `"calccomplexmatrix"` |
| Algebraic Matrix                | `"algmatrix"`         |
| Complex                         | `"complex"`           |
| Calculated Complex              | `"calccomplex"`       |
| Interval                        | `"interval"`          |
| Calculated Interval             | `"calcinterval"`      |
| Essay                           | `"essay"`             |
| String                          | `"string"`            |
| File Upload                     | `"file"`              |
| Chemical Equation               | `"chemeqn"`           |
| Chemical Molecule Drawing       | `"molecule"`          |

For Algebra 1, the most important short names are:

```php
"number"
"calculated"
"choices"
"multans"
"matching"
"numfunc"
"draw"
"ntuple"
"calcntuple"
"interval"
"calcinterval"
"string"
"essay"
```

---

# 3. Multipart Indexing Rules

In multipart questions, most answer variables become arrays.

Example:

```php
$anstypes = array("choices","calculated","numfunc")
$answeights = array(.25,.35,.40)

$questions[0] = array("Yes","No")
$answer[0] = 0

$answer[1] = 12
$answerformat[1] = "integer"

$answer[2] = "2x+3"
$variables[2] = "x"
```

Question text can use:

```html
$answerbox[0]
$answerbox[1]
$answerbox[2]
```

or:

```html
[AB0]
[AB1]
[AB2]
```

Important:

* Multipart part indexes start at `0`.
* `$answer[0]` belongs to the first part.
* `$answer[1]` belongs to the second part.
* `$questions[0]` belongs to the first multiple-choice or dropdown part.
* `$variables[2]` belongs to the third part if that part is a function / algebraic expression answer.
* `$answeights` should usually add to 1, such as `array(.4,.6)`.

---

# 4. Number

Use `number` when the answer should be a simple fixed numeric value.

## Best For

* slope as an integer
* y-intercept as an integer
* a single coordinate value
* a simple count
* a simple solution like `x = 5`, when the student only enters `5`

## Example

```php
$answer = 5
```

Multipart example:

```php
$anstypes = array("number")
$answer[0] = 5
```

## Use Number When

* The answer is a number.
* Equivalent expressions like `10/2` are not the main goal.
* You do not need the student to enter a fraction or expression.

## Avoid Number When

* The student might enter `3/4`, `sqrt(2)`, or another expression.
* You want the system to evaluate equivalent numeric expressions.
* You need answer format control.

Use `calculated` instead.

---

# 5. Calculated

Use `calculated` when the student should enter a numeric expression that MOM can evaluate.

## Best For

* fractions
* decimals
* square roots
* expressions like `3/4`
* answers that can be equivalent in multiple forms
* numeric answers requiring tolerance

## Example

```php
$answer = "3/4"
```

Multipart example:

```php
$anstypes = array("calculated")
$answer[0] = "3/4"
```

## Helpful Options

```php
$answerformat = "fraction"
$requiretimes = "3,4"
```

Multipart version:

```php
$answerformat[0] = "fraction"
$requiretimes[0] = "3,4"
```

## Feedback Pattern

For calculated answers, use `$stuanswersval` when checking the numerical value.

```php
$stu = getstuans($stuanswers,$thisq,0)
$stuval = getstuans($stuanswersval,$thisq,0)
```

## Use Calculated When

* Equivalent numeric forms should be accepted.
* The answer could be a fraction.
* The answer may require tolerance.
* You want to detect format issues, such as decimal instead of fraction.

## Avoid Calculated When

* The answer is an algebraic expression with variables.
* The student should enter an equation.
* The task is mostly about form, not numeric value.

Use `numfunc` instead.

---

# 6. Multiple Choice

Use `choices` when the student chooses one option.

## Best For

* identify the correct equation
* choose a graph description
* choose whether a relation is a function
* choose the correct interpretation
* select the best model

## Example

```php
$questions = array("Yes","No")
$answer = 0
```

Multipart example:

```php
$anstypes = array("choices")
$questions[0] = array("Yes","No")
$answer[0] = 0
```

## Important

The correct answer is usually the index of the correct choice.

```text
0 = first choice
1 = second choice
2 = third choice
3 = fourth choice
```

## Best Practices

* Keep choices unique.
* Distractors should reflect real student mistakes.
* Do not make choices too wordy unless the skill is interpretation.
* Use targeted feedback for each wrong choice when possible.
* Randomize or shuffle choices only if the answer index is updated correctly.

---

# 7. Multiple Answer

Use `multans` when more than one answer may be correct.

## Best For

* select all functions
* select all equivalent expressions
* select all true statements
* select all points that lie on a line
* select all equations with the same solution

## Example

```php
$questions = array("A","B","C","D")
$answer = "0,2"
```

Multipart example:

```php
$anstypes = array("multans")
$questions[0] = array("A","B","C","D")
$answer[0] = "0,2"
```

## Best Practices

* Clearly say “Select all that apply.”
* Make sure there is at least one correct answer.
* Avoid having too many correct answers.
* Make distractors plausible but not ambiguous.
* Use this type only when multiple selections are instructionally meaningful.

---

# 8. Matching

Use `matching` when students pair items.

## Best For

* match equations to graphs
* match terms to definitions
* match tables to equations
* match verbal descriptions to function types
* match graph features to meanings

## Best Practices

* Keep the matching set short.
* Avoid nearly identical wording.
* Make every pair unambiguous.
* Use matching when it is more efficient than several multiple-choice questions.

---

# 9. Function / Algebraic Expression

Use `numfunc` when students enter an algebraic expression, equation, or function.

## Best For

* writing linear equations
* writing explicit formulas
* writing recursive rules
* writing equivalent expressions
* solving literal equations
* entering expressions with variables

## Example

```php
$answer = "2x+3"
$variables = "x"
```

Multipart example:

```php
$anstypes = array("numfunc")
$answer[0] = "2x+3"
$variables[0] = "x"
```

## For Equations

```php
$answer = "y=2x+3"
$variables = "x,y"
```

## Helpful Options

```php
$requiretimes = "x"
```

Multipart version:

```php
$requiretimes[0] = "x"
```

## Use `numfunc` When

* The answer includes variables.
* Equivalent algebraic expressions should be accepted.
* The student writes an equation.
* The student writes a formula.

## Avoid `numfunc` When

* The answer is just a number or fraction.
* The student is choosing from options.
* The answer is an ordered pair.

Use `calculated`, `choices`, or `ntuple` instead.

## Important Codex Rule

Be explicit in the question text:

* “Enter only the expression.”
* “Enter the full equation.”
* “Use `x` as the variable.”
* “Do not include spaces or units.”

Only include those instructions when they are useful and not cluttering the page.

---

# 10. String

Use `string` for short text answers.

## Best For

* vocabulary words
* one-word classification
* short labels
* short explanations with predictable wording

## Example

```php
$answer = "linear"
```

## Best Practices

* Use sparingly.
* Avoid when many equivalent phrasings are possible.
* Consider multiple choice if the exact wording is not important.
* Consider essay if you want a longer response.

---

# 11. Essay

Use `essay` when the student writes a longer explanation.

## Best For

* explain reasoning
* justify a choice
* interpret a slope or intercept in context
* describe why a graph is or is not a function

## Best Practices

* Use when teacher review is expected or when auto-scoring is limited.
* If auto-scoring, use keyword-based checks carefully.
* Do not use essay when a precise auto-graded answer type is available.

---

# 12. Drawing

Use `draw` when students must create or edit a graph.

## Best For

* plot a point
* graph a line
* graph a system
* graph an inequality
* draw a parabola or exponential curve
* place open or closed dots

## Useful Related Macros

```php
gettwopointlinedata
gettwopointdata
gettwopointformulas
getdotsdata
getopendotsdata
getineqdata
getsnapwidthheight
```

## Best Practices

* Use consistent graph windows.
* Use snap-to-grid when possible.
* Make the instructions very clear.
* Visually test the problem before using it.
* Use feedback to distinguish different graphing mistakes:

  * wrong slope
  * wrong intercept
  * wrong point
  * wrong open/closed dot
  * wrong dashed/solid boundary
  * wrong shading

---

# 13. N-Tuple

Use `ntuple` for ordered pairs or coordinate-style answers.

## Best For

* ordered pairs
* solution to a system
* vertex of a parabola
* coordinate points
* center of a circle, if applicable

## Example

```php
$answer = "(2,3)"
```

Multipart example:

```php
$anstypes = array("ntuple")
$answer[0] = "(2,3)"
```

## Best Practices

* Tell students the expected format, such as `(x,y)`.
* Use when order matters.
* Do not use for a list of unrelated numbers.

---

# 14. Calculated N-Tuple

Use `calcntuple` when tuple entries may be numeric expressions.

## Best For

* ordered pairs with fractions
* intersection points with non-integer values
* vertices involving fractional coordinates

## Example

```php
$answer = "(1/2,3/4)"
```

## Best Practices

* Use when equivalent numeric forms should be accepted.
* Use `getntupleparts` when extracting student entries.
* Use `comparentuples` when comparing tuple values.

---

# 15. Interval

Use `interval` when the answer is interval notation.

## Best For

* domain in interval notation
* range in interval notation
* solution sets
* inequality solution intervals

## Example

```php
$answer = "[2,infty)"
```

## Best Practices

* Use only if students are expected to know interval notation.
* Be clear about parentheses and brackets.
* For Algebra 1 TEKS, inequality notation may sometimes be better than interval notation.

---

# 16. Calculated Interval

Use `calcinterval` when interval endpoints may be expressions or calculated values.

## Best For

* interval endpoints involving fractions
* calculated domain/range endpoints
* solution intervals with non-integer endpoints

## Best Practices

* Use when equivalent numeric endpoints should be accepted.
* Avoid if simple inequality notation is more appropriate for the standard.

---

# 17. Conditional

Use conditional logic when displayed content or required answers depend on a prior answer or random branch.

## Best For

* unlock-style multipart problems
* different follow-up questions based on a previous response
* separate graph/table/equation branches

## Best Practices

* Test every branch.
* Do not hide answerboxes accidentally.
* Make sure the scoring logic matches the displayed branch.
* Keep conditions simple.
* Prefer normal multipart unless conditional behavior is really needed.

---

# 18. Choosing Between Similar Types

## Number vs. Calculated

Use `number` when:

```text
answer is a simple fixed number
```

Use `calculated` when:

```text
student may enter a fraction, decimal, or equivalent numeric expression
```

Example:

* Slope is `3`: use `number` or `calculated`.
* Slope is `3/4`: use `calculated`.

## Calculated vs. Numfunc

Use `calculated` when:

```text
answer has no variables
```

Use `numfunc` when:

```text
answer includes variables or is an equation
```

Example:

* `3/4`: calculated
* `3x+4`: numfunc
* `y=3x+4`: numfunc

## Multiple Choice vs. Multiple Answer

Use `choices` when:

```text
exactly one answer is correct
```

Use `multans` when:

```text
more than one answer may be correct
```

## N-Tuple vs. Two Number Parts

Use `ntuple` when:

```text
the ordered pair is the answer
```

Use two number/calculated parts when:

```text
you want to scaffold x-coordinate and y-coordinate separately
```

## Drawing vs. Multiple Choice Graph Selection

Use `draw` when:

```text
students need to construct the graph
```

Use `choices` when:

```text
students only need to recognize or interpret the graph
```

---

# 19. Recommended Algebra 1 Defaults

## Slopes

| Situation                            | Recommended Type     |
| ------------------------------------ | -------------------- |
| integer slope                        | number or calculated |
| fractional slope                     | calculated           |
| slope from graph with answer choices | choices              |
| construct line from slope            | draw                 |

## Linear Equations

| Situation                      | Recommended Type |
| ------------------------------ | ---------------- |
| choose equation                | choices          |
| write equation                 | numfunc          |
| identify slope/intercept first | multipart        |
| graph equation                 | draw             |

## Functions

| Situation                        | Recommended Type |
| -------------------------------- | ---------------- |
| decide if relation is a function | choices          |
| select all functions             | multans          |
| evaluate function value          | calculated       |
| write function rule              | numfunc          |
| explain why not a function       | essay or string  |

## Systems

| Situation                    | Recommended Type     |
| ---------------------------- | -------------------- |
| solution as ordered pair     | ntuple or calcntuple |
| solve x and y separately     | multipart calculated |
| graph the system             | draw                 |
| classify number of solutions | choices              |

## Quadratics

| Situation                 | Recommended Type                     |
| ------------------------- | ------------------------------------ |
| identify vertex           | ntuple or calcntuple                 |
| identify axis of symmetry | numfunc or string                    |
| identify zeros            | calculated, calcntuple, or multipart |
| write quadratic equation  | numfunc                              |
| choose graph features     | choices                              |
| graph quadratic           | draw                                 |

## Exponentials

| Situation                  | Recommended Type |
| -------------------------- | ---------------- |
| identify initial value     | calculated       |
| identify growth factor     | calculated       |
| write exponential function | numfunc          |
| choose growth/decay        | choices          |
| graph exponential          | draw             |

## Domain and Range

| Situation                     | Recommended Type                                |
| ----------------------------- | ----------------------------------------------- |
| choose domain/range statement | choices                                         |
| enter inequality notation     | numfunc or string, depending on expected format |
| enter interval notation       | interval or calcinterval                        |
| scaffold lower/upper bounds   | multipart calculated/choices                    |

---

# 20. Feedback by Answer Type

## Multiple Choice

Use choice-specific feedback.

```php
$feedbacktxt[0] = "Check whether the graph passes the vertical line test."
$feedbacktxt[1] = "Correct."
```

## Number

Use partial-credit wrong-answer checks for common mistakes.

Examples:

* wrong sign
* reciprocal
* used x-value instead of y-value
* used y-intercept instead of slope

## Calculated

Use `$stuanswersval` for numeric comparisons.

Examples:

* correct value but wrong format
* decimal instead of required fraction
* reciprocal
* negative of correct answer

## Numfunc

Use common wrong-expression checks.

Examples:

* missing `x`
* wrong slope
* wrong intercept
* reversed sign
* equation instead of expression
* expression instead of equation

## Drawing

Use graph-data extraction macros when possible.

Examples:

* wrong point
* wrong line
* wrong slope
* wrong shading
* wrong boundary type

## Multipart

Use per-part feedback.

Example:

```php
$feedback[0] = ...
$feedback[1] = ...
$feedback[2] = ...
```

Always verify that feedback references the correct part index.

---

# 21. Codex Checklist for Answer Type Selection

Before writing the problem, Codex should answer:

* What should the student do?
* Is the student selecting, entering, drawing, matching, or explaining?
* Is the answer numeric, algebraic, graphical, verbal, or a tuple?
* Should equivalent forms be accepted?
* Does the answer need a variable?
* Does the answer need a specific format?
* Is this a one-part or multipart problem?
* Does the problem need targeted feedback?
* Does the problem need a student guide?

---

# 22. Common Mistakes Codex Must Avoid

* Using `number` when the answer is a fraction expression.
* Using `calculated` when the answer has variables.
* Using `numfunc` without defining `$variables`.
* Using `choices` but setting `$answer` to the answer text instead of the index.
* Forgetting that choices are zero-indexed.
* Forgetting that multipart parts are zero-indexed.
* Referencing `$answerbox[1]` when only one part exists.
* Using `$stuanswers` in feedback before checking that an answer exists.
* Using `$stuanswers` instead of `$stuanswersval` for calculated feedback.
* Forgetting to set `$answeights` for uneven multipart scoring.
* Hiding answerboxes with conditional text.
* Giving feedback that reveals the answer before the student is done.

---

# 23. Minimum Testing Checklist

Before using any generated MOM problem:

* [ ] The chosen answer type matches the student task.
* [ ] The correct MOM short name is used.
* [ ] `$answer` or `$answer[part]` is defined.
* [ ] `$questions` is defined for choice-based parts.
* [ ] `$variables` is defined for `numfunc` parts.
* [ ] `$answerformat` is defined when format matters.
* [ ] `$requiretimes` is defined when structure matters.
* [ ] `$answerbox` indexes match `$anstypes`.
* [ ] `$answeights` match the number of parts.
* [ ] Feedback references the correct part.
* [ ] `$showanswer` gives the answer first.
* [ ] All branches and random versions are tested.
