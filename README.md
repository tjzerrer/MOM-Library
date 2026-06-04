# MOM-Library

This repository stores MyOpenMath problem templates, student help guides, and reusable code patterns for building high-quality math practice problems.

## Goals

- Create randomized MyOpenMath problems with many variations.
- Keep formatting consistent across all problems.
- Build reusable templates for common problem types.
- Include targeted feedback for common student errors.
- Include clear `$showanswer` explanations.
- Maintain a library that can eventually be licensed or shared with schools.

## Main Sections

- `/style-guide/` — rules for formatting, layout, feedback, and student guides
- `/templates/` — reusable MOM templates
- `/problems/` — finished MOM problems organized by course and topic
- `/student-guides/` — standalone HTML student help guides
- `/tests/` — future testing/checking tools for generated problems

## Core Formatting Rules

- Use 14pt font unless otherwise specified.
- Keep layouts compact for Chromebooks.
- Use clear targeted feedback.
- `$showanswer` should give the answer first, then the rationale.
- Student guides should be textbook-style, not long vertical lists.
- Use inline CSS only for student guides.
