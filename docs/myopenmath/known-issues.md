# MyOpenMath Known Issues and Fixes

This file tracks common issues that happen when building MyOpenMath problems and how to avoid them.

## Formatting Issues

### Problem: Font size is inconsistent

Fix: Include CSS in the question text.

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
```

## Layout Issues

### Problem: Calculator takes too much space

Fix: Place the calculator in a narrow top-right table cell.

```html
<td style="width:1%; vertical-align:top; padding:0 0 0 6px; white-space:nowrap; text-align:right;">
  <!-- calculator iframe goes here -->
</td>
```

## Randomization Issues

### Problem: Answer choices repeat

Fix: Check that distractors are unique before displaying them.

### Problem: Random values create messy or invalid answers

Fix: Restrict random values so every version produces a clean, valid answer.

## Feedback Issues

### Problem: Feedback gives away the answer too early

Fix: Feedback should guide the student toward the error without revealing the correct answer unless the student is already correct.

## Showanswer Issues

### Problem: `$showanswer` starts with explanation instead of answer

Fix: Always show the answer first, then the rationale.

Preferred pattern:

```php
$showanswer = "
<div style='font-size:14pt; line-height:1.2;'>
  <div><strong>Answer:</strong> [answer here]</div>
  <div style='margin-top:6px;'><strong>Rationale:</strong> [explanation here]</div>
</div>";
```
