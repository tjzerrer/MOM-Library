# Multipart MOM Problem Template

Use this template when creating a MyOpenMath problem with multiple parts, targeted feedback, and a `$showanswer`.

## Problem Overview

* Course:
* Standard:
* Skill:
* Number of variations:
* Problem type:
* Calculator:
* Graph/table/diagram needed:
* Student guide needed:

## Common Control

```php
// Random variables go here.

// Answer variables go here.

// Distractors and common wrong answers go here.

// Feedback logic goes here.

$showanswer = "
<div style='font-size:14pt; line-height:1.2;'>
  <div><strong>Answer:</strong> [answer here]</div>
  <div style='margin-top:6px;'><strong>Rationale:</strong> [explanation here]</div>
</div>";
```

## Question Text

```html
<style>
  .anstext,
  .answer,
  input[type="text"],
  input[type="number"],
  textarea,
  label {
    font-size:14pt !important;
    line-height:1.12 !important;
  }
</style>

<div style="font-size:14pt; line-height:1.12; max-width:1100px; margin:0;">
  <!-- Problem text goes here -->
</div>
```

## Required Checks Before Using

* 14pt font is used throughout.
* The layout is compact for Chromebooks.
* All randomized values produce valid answers.
* Answer choices are unique.
* Different problem types appear with equal probability when required.
* Common wrong answers are detected when possible.
* Feedback guides the student without giving away the answer.
* `$showanswer` gives the answer first, then the rationale.
