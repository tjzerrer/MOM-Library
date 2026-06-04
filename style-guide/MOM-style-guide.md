# MyOpenMath Style Guide

## General Layout

* Use 14pt font for problem text, answer inputs, dropdowns, radio buttons, and feedback.
* Keep vertical spacing tight.
* Avoid overly long vertical explanations.
* Design for Chromebook screens.
* Use tables when helpful to keep problem text and calculator side by side.

## Calculator

When requested, embed the Desmos Texas Scientific Calculator using the MOM data-toggler iframe pattern:

```html
<iframe
  src="https://www.desmos.com/testing/texas/scientific"
  width="350"
  height="380"
  frameborder="0"
  data-toggler="Calculator"
  data-toggler-hide="Hide Calculator">
</iframe>
```

Preferred placement: put the calculator in the top-right cell of a table so the problem text stays on the left and the calculator toggle stays on the right.

```html
<td style="width:1%; vertical-align:top; padding:0 0 0 6px; white-space:nowrap; text-align:right;">
  <!-- calculator iframe goes here -->
</td>
```

## Student Guide Rules

* Use standalone HTML.
* Use inline CSS only.
* No external CSS.
* No JavaScript.
* No SVG.
* Use 14pt body text.
* Max-width should be about 1100px.
* Use a two-column textbook-style layout when possible.
* Left column: main method and worked examples.
* Right column: what to look for, shortcut, shortcut example, and common mistakes.
* Use bordered example cards and callout boxes.
* Use stacked fractions with inline HTML/CSS instead of slash fractions when fractions appear in final answers.
* Use color sparingly:

  * blue for x-related ideas
  * orange/brown for y-coefficient, divisor, or comparison value
  * green for the final answer, rate of change, slope, or key conclusion

## Showanswer Rules

* `$showanswer` should appear in the common control when possible.
* `$showanswer` should give the answer first.
* Then it should explain the rationale.
* Use color only when it helps show relationships between values.
* Do not use large colored backgrounds unless specifically requested.

## Randomization Rules

* Randomized values must produce clean, valid answers.
* Distractors should reflect real student mistakes.
* Answer choices should be unique.
* If different problem types are included, each type should have an equal chance of appearing.
* Prefer at least 40 variations.
* For larger problems, aim for 90+ variations.

## Feedback Rules

Feedback should detect common wrong answers when possible, such as:

* wrong sign
* reciprocal slope
* using the wrong coordinate
* confusing x-value and y-value
* using the y-value as the y-intercept
* solving only part of the problem
* arithmetic error
* choosing the correct method but applying it incorrectly

Feedback should guide the student without simply giving away the answer unless the answer is already correct.
