# Texas Algebra 1 TEKS Summary for MOM Problem Development

Source reference: Texas Education Agency, 19 TAC Chapter 111, §111.39 Algebra I, Adopted 2012, One Credit.

This file summarizes the Algebra 1 TEKS in a way that is useful for creating MyOpenMath problems, tagging problems, and guiding Codex when generating new questions.

## Purpose

Use this file to help create, organize, and tag Algebra 1 MyOpenMath problems.

Each MOM problem should include:

* Course: Algebra 1
* TEKS standard code
* Topic
* Skill
* Representation type
* Problem format
* Difficulty level
* Common wrong answers
* Calculator need
* Student guide need

Recommended problem folder naming pattern:

```text
problems/algebra1/A1-3A-slope-from-table/
```

Recommended problem metadata pattern:

```md
Course: Algebra 1
TEKS: A.3A
Topic: Linear functions
Skill: Determine slope from a table, graph, two points, or equation
Representations: table, graph, points, equation
Problem Type: multipart / multiple choice / numerical / graphing
Calculator: optional
```

---

# Algebra 1 Overview

In Algebra 1, students build from middle school mathematics, especially linear relationships, proportionality, and number operations.

Major content areas include:

* linear functions, equations, inequalities, and systems
* quadratic functions and equations
* exponential functions and equations
* transformations of parent functions
* equations and solutions in mathematical and real-world contexts
* statistical relationships and data modeling
* polynomials of degree one and two
* radical expressions
* laws of exponents
* arithmetic and geometric sequences
* functions and relations
* literal equations and formulas

For MOM problem development, most Algebra 1 questions should emphasize:

* multiple representations
* student reasoning
* clean randomized values
* common student misconceptions
* real-world contexts when helpful
* graph/table/equation connections
* answer validation and targeted feedback

---

# A.1 Mathematical Process Standards

These process standards should be embedded across all Algebra 1 problems.

## A.1A Apply Mathematics

Students apply mathematics to problems arising in everyday life, society, and the workplace.

MOM problem implications:

* Use real-world contexts when appropriate.
* Ask students to interpret answers, not only calculate.
* Include units and reasonable domains when possible.

## A.1B Problem-Solving Model

Students analyze information, create a plan, determine a solution, justify the solution, and evaluate reasonableness.

MOM problem implications:

* Use multipart questions that guide students through reasoning.
* Include “reasonableness” checks.
* Use `$showanswer` to explain the reasoning process.

## A.1C Tools and Techniques

Students select tools, including manipulatives, paper and pencil, technology, mental math, estimation, and number sense.

MOM problem implications:

* Decide whether a calculator should be embedded.
* For regression or data-fitting tasks, technology may be expected.
* For skill fluency, avoid over-reliance on calculators.

## A.1D Multiple Representations

Students communicate mathematical ideas using symbols, diagrams, graphs, and language.

MOM problem implications:

* Connect equations, tables, graphs, and verbal descriptions.
* Include questions that ask students to interpret a representation.
* Use graph/table displays when the standard calls for them.

## A.1E Create and Use Representations

Students create and use representations to organize, record, and communicate mathematical ideas.

MOM problem implications:

* Ask students to complete tables, identify graph features, write equations, or create formulas.
* Use matching or multipart tasks when students must connect forms.

## A.1F Analyze Relationships

Students analyze mathematical relationships to connect and communicate ideas.

MOM problem implications:

* Ask students to compare patterns.
* Use questions that require identifying structure, such as slope, intercepts, zeros, factors, or growth factors.

## A.1G Justify Mathematical Ideas

Students explain and justify mathematical ideas using precise mathematical language.

MOM problem implications:

* Include explanation parts when appropriate.
* Use essay/string response carefully with keyword scoring if needed.
* In `$showanswer`, model precise vocabulary.

---

# A.2 Linear Functions, Equations, and Inequalities: Writing and Representing

Students write and represent linear equations, inequalities, and systems in multiple ways, with and without technology.

## A.2A Domain and Range of Linear Functions

Students determine domain and range of a linear function in mathematical problems, determine reasonable domain and range values for real-world situations, both continuous and discrete, and represent domain and range using inequalities.

Problem ideas:

* Identify domain and range from a graph.
* Determine reasonable domain/range from a real-world situation.
* Distinguish continuous vs. discrete domains.
* Represent domain and range using inequalities.

Common errors:

* Mixing up domain and range.
* Using all real numbers in a restricted context.
* Ignoring discrete values.
* Reversing inequality symbols.

## A.2B Write Linear Equations from Slope and Points

Students write linear equations in two variables in forms including slope-intercept, standard form, and point-slope form, given one point and slope or two points.

Problem ideas:

* Write `y = mx + b` from a slope and a point.
* Write point-slope form from a point and slope.
* Write standard form from two points.
* Convert between forms.

Common errors:

* Using the x-value as the y-intercept.
* Sign errors when substituting into `y = mx + b`.
* Incorrect slope from two points.
* Incorrect standard form formatting.

## A.2C Write Linear Equations from Tables, Graphs, and Verbal Descriptions

Students write linear equations in two variables given a table of values, a graph, or a verbal description.

Problem ideas:

* Write an equation from a table.
* Write an equation from a graph.
* Write an equation from a word problem.
* Identify slope and intercept before writing the equation.

Common errors:

* Confusing slope with y-intercept.
* Using change in x over change in y.
* Ignoring initial value.
* Treating non-linear data as linear.

## A.2D Direct Variation

Students write and solve equations involving direct variation.

Problem ideas:

* Determine whether a relationship is direct variation.
* Write `y = kx`.
* Solve for the constant of variation.
* Interpret `k` in context.

Common errors:

* Including a nonzero y-intercept.
* Confusing direct variation with any linear relationship.
* Using `x/y` instead of `y/x`.

## A.2E Parallel Lines

Students write the equation of a line that contains a given point and is parallel to a given line.

Problem ideas:

* Find the slope of the given line.
* Use the same slope through a new point.
* Write the new line in slope-intercept or point-slope form.

Common errors:

* Using the opposite reciprocal slope.
* Copying the original line’s y-intercept.
* Sign errors when solving for `b`.

## A.2F Perpendicular Lines

Students write the equation of a line that contains a given point and is perpendicular to a given line.

Problem ideas:

* Find the negative reciprocal slope.
* Use a point and slope to write the new equation.
* Include horizontal/vertical special cases.

Common errors:

* Using the same slope instead of the negative reciprocal.
* Taking only the reciprocal but not changing the sign.
* Mishandling horizontal and vertical lines.

## A.2G Horizontal and Vertical Lines

Students write equations of lines parallel or perpendicular to the x-axis or y-axis and determine whether the slope is zero or undefined.

Problem ideas:

* Identify equations `x = a` and `y = b`.
* Determine zero vs. undefined slope.
* Match graphs to equations.

Common errors:

* Thinking vertical lines are functions.
* Saying vertical slope is zero.
* Confusing `x = a` with `y = a`.

## A.2H Linear Inequalities in Two Variables

Students write linear inequalities in two variables from a table, graph, or verbal description.

Problem ideas:

* Write an inequality from a boundary line and shaded region.
* Determine dashed vs. solid boundary.
* Interpret inequality constraints in context.

Common errors:

* Reversing the inequality sign.
* Using a solid line for strict inequalities.
* Shading the wrong side.

## A.2I Systems from Tables, Graphs, and Verbal Descriptions

Students write systems of two linear equations from a table, graph, or verbal description.

Problem ideas:

* Write a system from two scenarios.
* Write a system from two tables.
* Write a system from a graph.
* Interpret what the solution means.

Common errors:

* Writing only one equation.
* Mixing values from two relationships.
* Confusing the solution with an intercept.

---

# A.3 Linear Functions, Equations, and Inequalities: Graphs, Key Features, and Solving

Students use graphs of linear functions, key features, and transformations to represent and solve equations, inequalities, and systems.

## A.3A Determine Slope

Students determine slope from a table, graph, two points, or equation in various forms.

Problem ideas:

* Determine slope from a table.
* Determine slope from a graph.
* Determine slope from two points.
* Determine slope from `y = mx + b`.
* Determine slope from `Ax + By = C`.
* Determine slope from point-slope form.

Common errors:

* Computing run over rise.
* Sign errors.
* Treating y-intercept as slope.
* Mishandling standard form.

## A.3B Rate of Change in Context

Students calculate rate of change of a linear function represented in a table, graph, or equation in mathematical and real-world contexts.

Problem ideas:

* Interpret slope as a rate.
* Include units.
* Compare rates from different representations.
* Decide what the rate means in context.

Common errors:

* Leaving off units.
* Confusing initial value with rate.
* Using total amount instead of change.

## A.3C Graph Linear Functions and Identify Key Features

Students graph linear functions and identify x-intercept, y-intercept, zeros, and slope.

Problem ideas:

* Graph a line from slope and intercept.
* Identify slope and intercepts from a graph.
* Connect zero with x-intercept.
* Interpret key features in context.

Common errors:

* Plotting the y-intercept on the x-axis.
* Using slope incorrectly from the intercept.
* Confusing zero with y-intercept.

## A.3D Graph Linear Inequalities

Students graph solution sets of linear inequalities in two variables.

Problem ideas:

* Choose dashed or solid boundary.
* Shade the correct half-plane.
* Test a point.

Common errors:

* Wrong boundary style.
* Shading the wrong side.
* Graphing the line but forgetting the inequality region.

## A.3E Transformations of Linear Parent Function

Students determine effects on the graph of `f(x) = x` when replaced by `af(x)`, `f(x) + d`, `f(x - c)`, or `f(bx)`.

Problem ideas:

* Identify vertical stretch/compression.
* Identify vertical and horizontal shifts.
* Compare transformed line to parent function.

Common errors:

* Thinking `f(x - c)` shifts left instead of right.
* Confusing vertical and horizontal changes.
* Misinterpreting `a` and `b`.

## A.3F Graph Systems of Linear Equations

Students graph systems of two linear equations and determine solutions if they exist.

Problem ideas:

* Graph two lines and identify intersection.
* Classify one solution, no solution, or infinitely many solutions.
* Connect algebraic and graphical solutions.

Common errors:

* Reporting an intercept instead of the intersection.
* Failing to recognize parallel lines.
* Failing to recognize identical lines.

## A.3G Estimate Solutions to Systems in Context

Students estimate graphically the solutions to systems of two linear equations in real-world problems.

Problem ideas:

* Estimate intersection from a graph.
* Interpret break-even points.
* Decide which option is better before/after intersection.

Common errors:

* Exact answer expected when graph only supports estimate.
* Ignoring context units.
* Interpreting only one coordinate.

## A.3H Graph Systems of Linear Inequalities

Students graph solution sets of systems of linear inequalities.

Problem ideas:

* Graph two or more inequalities.
* Identify overlapping solution region.
* Test points in solution region.

Common errors:

* Shading union instead of intersection.
* Using wrong boundary style.
* Ignoring one inequality.

---

# A.4 Statistical Relationships

Students formulate statistical relationships and evaluate their reasonableness based on real-world data.

## A.4A Correlation Coefficient

Students calculate, using technology, the correlation coefficient between two quantitative variables and interpret it as a measure of strength of linear association.

Problem ideas:

* Interpret a given correlation coefficient.
* Match scatterplots to correlation strength.
* Use technology to calculate correlation when appropriate.

Common errors:

* Treating correlation as slope.
* Thinking negative correlation means weak correlation.
* Confusing association strength with direction.

## A.4B Association and Causation

Students compare and contrast association and causation in real-world problems.

Problem ideas:

* Identify whether a claim implies causation.
* Explain why association does not prove causation.
* Match scenarios to association/causation language.

Common errors:

* Assuming correlation proves causation.
* Ignoring lurking variables.

## A.4C Linear Models for Data

Students write, with and without technology, linear functions that reasonably fit data to estimate solutions and make predictions.

Problem ideas:

* Use a line of best fit.
* Make predictions from a linear model.
* Interpret slope and intercept of a model.
* Decide whether a prediction is interpolation or extrapolation.

Common errors:

* Using two arbitrary points without considering fit.
* Extrapolating too far.
* Misinterpreting slope or intercept.

---

# A.5 Solving Linear Equations, Inequalities, and Systems

Students solve linear equations and evaluate reasonableness.

## A.5A Solve Linear Equations

Students solve linear equations in one variable, including equations requiring the distributive property and equations with variables on both sides.

Problem ideas:

* One-step and two-step equations.
* Equations with distribution.
* Variables on both sides.
* Equations with fractions or decimals.

Common errors:

* Not distributing to every term.
* Combining unlike terms.
* Sign errors.
* Not applying inverse operations to both sides.

## A.5B Solve Linear Inequalities

Students solve linear inequalities in one variable, including distribution and variables on both sides.

Problem ideas:

* Solve and graph inequalities.
* Include cases requiring flipping the inequality sign.
* Interpret solution sets in context.

Common errors:

* Forgetting to reverse the inequality when multiplying or dividing by a negative.
* Graphing with the wrong open/closed circle.
* Reversing arrow direction.

## A.5C Solve Systems Algebraically

Students solve systems of two linear equations with two variables in mathematical and real-world problems.

Problem ideas:

* Solve by substitution.
* Solve by elimination.
* Interpret the solution in context.
* Classify no solution or infinitely many solutions.

Common errors:

* Arithmetic errors in elimination.
* Substituting into the wrong equation incorrectly.
* Reporting only one coordinate.
* Not interpreting the ordered pair.

---

# A.6 Quadratic Functions and Equations: Writing and Representing

Students write and represent quadratic equations in multiple ways.

## A.6A Domain and Range of Quadratics

Students determine domain and range of quadratic functions and represent them using inequalities.

Problem ideas:

* Determine domain and range from a graph.
* Determine range from a vertex and opening direction.
* Use inequality notation.

Common errors:

* Giving range as all real numbers.
* Reversing domain and range.
* Using the x-coordinate of the vertex for range.

## A.6B Write Quadratics from Vertex and Point

Students write equations of quadratic functions given the vertex and another point, write the equation in vertex form, and rewrite it from vertex form to standard form.

Problem ideas:

* Use `f(x) = a(x - h)^2 + k`.
* Substitute a point to solve for `a`.
* Convert vertex form to standard form.

Common errors:

* Incorrect sign in `(x - h)`.
* Forgetting to square.
* Not solving correctly for `a`.

## A.6C Write Quadratics from Real Solutions and Graphs

Students write quadratic functions given real solutions and graphs of related equations.

Problem ideas:

* Use zeros to write factored form.
* Determine `a` from another point or graph.
* Connect x-intercepts and factors.

Common errors:

* Using zeros as factors without changing signs.
* Forgetting the leading coefficient.
* Confusing solutions with y-intercept.

---

# A.7 Quadratic Functions and Equations: Graphs and Transformations

Students use graphs and transformations to determine solutions.

## A.7A Graph Quadratics and Identify Key Attributes

Students graph quadratic functions and identify x-intercept, y-intercept, zeros, maximum value, minimum value, vertex, and axis of symmetry.

Problem ideas:

* Identify key features from a graph.
* Graph from vertex form.
* Graph from standard form.
* Interpret maximum/minimum in context.

Common errors:

* Confusing x-intercepts and zeros.
* Giving axis of symmetry as a point instead of a line.
* Mixing up maximum and minimum.
* Using the wrong coordinate of the vertex.

## A.7B Linear Factors and Zeros

Students describe the relationship between linear factors of quadratic expressions and zeros of associated quadratic functions.

Problem ideas:

* Match factored form to zeros.
* Use zeros to write factors.
* Explain why a factor gives a zero.

Common errors:

* Not changing signs between factors and zeros.
* Confusing factors with solutions.
* Treating repeated roots as two different zeros.

## A.7C Transformations of Quadratic Parent Function

Students determine effects on the graph of `f(x) = x^2` when replaced by `af(x)`, `f(x) + d`, `f(x - c)`, or `f(bx)`.

Problem ideas:

* Identify shifts, stretches, compressions, and reflections.
* Match equations to transformed graphs.
* Describe transformations in words.

Common errors:

* Misreading horizontal shifts.
* Confusing `a` and `b`.
* Forgetting reflection when coefficient is negative.

---

# A.8 Solving Quadratics and Quadratic Models

Students solve quadratic equations and use quadratic models.

## A.8A Solve Quadratic Equations

Students solve quadratic equations with real solutions by factoring, square roots, completing the square, and quadratic formula.

Problem ideas:

* Choose a solving method.
* Solve by factoring.
* Solve by square roots.
* Solve using the quadratic formula.
* Compare solution methods.

Common errors:

* Forgetting `±`.
* Factoring errors.
* Sign errors in quadratic formula.
* Incorrect square root simplification.

## A.8B Quadratic Regression and Modeling

Students write quadratic functions using technology to fit data, estimate solutions, and make predictions.

Problem ideas:

* Interpret a quadratic model.
* Use regression output.
* Predict from a quadratic model.
* Decide whether a prediction is reasonable.

Common errors:

* Treating quadratic data as linear.
* Extrapolating too far.
* Misinterpreting vertex or intercepts in context.

---

# A.9 Exponential Functions and Equations

Students write, graph, represent, and interpret exponential functions and models.

## A.9A Domain and Range of Exponential Functions

Students determine domain and range of exponential functions of the form `f(x) = ab^x` and represent domain and range using inequalities.

Problem ideas:

* Identify domain and range from an exponential graph.
* Connect horizontal asymptote to range.
* Use inequality notation.

Common errors:

* Giving range as all real numbers.
* Ignoring the asymptote.
* Confusing growth/decay with domain.

## A.9B Interpret `a` and `b` in Exponential Functions

Students interpret the meaning of `a` and `b` in `f(x) = ab^x` in real-world problems.

Problem ideas:

* Identify initial value.
* Identify growth or decay factor.
* Interpret percent increase/decrease.

Common errors:

* Treating `b` as percent instead of multiplier.
* Confusing initial value and growth factor.
* Thinking decay factor must be negative.

## A.9C Write Exponential Functions

Students write exponential functions in the form `f(x) = ab^x`, where `b` is rational, to describe mathematical and real-world growth and decay situations.

Problem ideas:

* Write a function from an initial value and growth/decay factor.
* Write a function from a table.
* Write a function from a percent change.

Common errors:

* Using additive change instead of multiplicative change.
* Writing `1 - r` incorrectly for decay.
* Using the wrong initial value.

## A.9D Graph Exponential Functions

Students graph exponential functions that model growth and decay and identify y-intercept and asymptote.

Problem ideas:

* Graph growth and decay.
* Identify y-intercept.
* Identify horizontal asymptote.
* Match graph to equation.

Common errors:

* Drawing a linear graph.
* Crossing the asymptote.
* Misidentifying the y-intercept.

## A.9E Exponential Regression and Modeling

Students write exponential functions using technology to fit data and make predictions.

Problem ideas:

* Use regression output.
* Choose exponential model from data.
* Make and interpret predictions.

Common errors:

* Using linear regression for exponential data.
* Misinterpreting growth factor.
* Extrapolating beyond reasonable context.

---

# A.10 Number and Algebraic Methods: Polynomials

Students rewrite equivalent forms and perform operations on polynomial expressions.

## A.10A Add and Subtract Polynomials

Students add and subtract polynomials of degree one and degree two.

Problem ideas:

* Combine like terms.
* Subtract polynomials with parentheses.
* Identify equivalent expressions.

Common errors:

* Combining unlike terms.
* Not distributing the negative.
* Dropping terms.

## A.10B Multiply Polynomials

Students multiply polynomials of degree one and degree two.

Problem ideas:

* Distribute monomials.
* Multiply binomials.
* Multiply polynomial expressions.

Common errors:

* Missing middle terms.
* Sign errors.
* Squaring binomials incorrectly.

## A.10C Divide Polynomials

Students determine quotients of polynomials of degree one and degree two divided by polynomials of degree one and degree two when the divisor degree does not exceed the dividend degree.

Problem ideas:

* Divide polynomial by monomial or binomial.
* Use factoring to simplify rational polynomial expressions.
* Use polynomial division where appropriate.

Common errors:

* Dividing only the first term.
* Cancelling terms incorrectly.
* Ignoring degree restrictions.

## A.10D Rewrite Using the Distributive Property

Students rewrite polynomial expressions of degree one and degree two in equivalent forms using the distributive property.

Problem ideas:

* Factor out a common factor.
* Expand expressions.
* Match equivalent expressions.

Common errors:

* Not distributing to every term.
* Incorrect greatest common factor.
* Sign errors.

## A.10E Factor Trinomials

Students factor, if possible, trinomials with real factors in the form `ax^2 + bx + c`, including perfect square trinomials.

Problem ideas:

* Factor simple trinomials.
* Factor trinomials where `a > 1`.
* Identify perfect square trinomials.
* Determine if a trinomial is not factorable over real/integer factors depending on task design.

Common errors:

* Choosing factors of `c` that do not add to `b`.
* Ignoring `a`.
* Incorrect signs.
* Misidentifying perfect square trinomials.

## A.10F Difference of Squares

Students decide if a binomial can be written as the difference of two squares and, if possible, use the structure to rewrite it.

Problem ideas:

* Identify difference of squares.
* Factor `a^2 - b^2`.
* Decide whether an expression is not a difference of squares.

Common errors:

* Factoring a sum of squares.
* Missing square roots of terms.
* Sign errors in factors.

---

# A.11 Number and Algebraic Methods: Radicals and Exponents

Students rewrite algebraic expressions into equivalent forms.

## A.11A Simplify Numerical Radical Expressions

Students simplify numerical radical expressions involving square roots.

Problem ideas:

* Simplify square roots.
* Identify perfect square factors.
* Compare simplified radicals.

Common errors:

* Taking square root of each term in a sum.
* Not fully simplifying.
* Incorrect perfect square factor.

## A.11B Laws of Exponents

Students simplify numeric and algebraic expressions using laws of exponents, including integral and rational exponents.

Problem ideas:

* Product of powers.
* Quotient of powers.
* Power of a power.
* Zero and negative exponents.
* Rational exponents.

Common errors:

* Adding exponents when multiplying bases that are different.
* Multiplying exponents in the wrong situation.
* Treating negative exponents as negative values.
* Misinterpreting rational exponents.

---

# A.12 Number and Algebraic Methods: Functions, Sequences, and Literal Equations

Students write, solve, analyze, and evaluate equations, relations, and functions.

## A.12A Determine Whether a Relation is a Function

Students decide whether relations represented verbally, in tables, graphs, and symbols define a function.

Problem ideas:

* Vertical line test.
* Mapping diagrams.
* Tables with repeated x-values.
* Ordered pairs.
* Verbal descriptions.

Common errors:

* Repeated y-values incorrectly considered not a function.
* Ignoring repeated x-values with different y-values.
* Misapplying the vertical line test.

## A.12B Evaluate Functions

Students evaluate functions in function notation given one or more domain elements.

Problem ideas:

* Evaluate `f(x)` for a number.
* Evaluate using a table or graph.
* Evaluate expressions like `f(a + 1)`.
* Evaluate multiple function values.

Common errors:

* Treating `f(x)` as multiplication.
* Substituting into only part of the expression.
* Order of operations errors.

## A.12C Recursive Sequences

Students identify terms of arithmetic and geometric sequences when sequences are given in function form using recursive processes.

Problem ideas:

* Generate terms from recursive notation.
* Identify next terms.
* Compare arithmetic and geometric recursive patterns.

Common errors:

* Using explicit formula thinking when recursion is required.
* Adding when the sequence is geometric.
* Forgetting the starting term.

## A.12D Formulas for Arithmetic and Geometric Sequences

Students write a formula for the nth term of arithmetic and geometric sequences given several terms.

Problem ideas:

* Write explicit arithmetic formula.
* Write explicit geometric formula.
* Determine common difference or common ratio.
* Connect sequence formula to function notation.

Common errors:

* Confusing common difference and common ratio.
* Off-by-one error in the exponent.
* Using term number incorrectly.

## A.12E Literal Equations and Formulas

Students solve mathematical and scientific formulas and other literal equations for a specified variable.

Problem ideas:

* Rearrange formulas.
* Solve for one variable in terms of others.
* Use geometry, science, or finance formulas.

Common errors:

* Not applying inverse operations to all terms.
* Dividing only one term.
* Sign errors.
* Losing parentheses.

---

# Recommended Algebra 1 MOM Problem Categories

Use these categories to organize the repository.

## Linear Functions

Relevant TEKS:

* A.2A
* A.2B
* A.2C
* A.2D
* A.2E
* A.2F
* A.2G
* A.3A
* A.3B
* A.3C
* A.3E

Problem types:

* slope from table
* slope from graph
* equation from table
* equation from graph
* equation from point and slope
* parallel and perpendicular lines
* horizontal and vertical lines
* direct variation
* transformations of `f(x) = x`

## Linear Inequalities and Systems

Relevant TEKS:

* A.2H
* A.2I
* A.3D
* A.3F
* A.3G
* A.3H
* A.5C

Problem types:

* graph linear inequalities
* write inequalities from graphs
* systems from word problems
* solve systems by graphing
* solve systems algebraically
* systems of inequalities

## Data and Modeling

Relevant TEKS:

* A.4A
* A.4B
* A.4C
* A.8B
* A.9E

Problem types:

* correlation coefficient interpretation
* association vs. causation
* line of best fit
* quadratic regression
* exponential regression
* prediction and reasonableness

## Equations and Inequalities

Relevant TEKS:

* A.5A
* A.5B
* A.12E

Problem types:

* solve linear equations
* solve linear inequalities
* literal equations
* formulas in context

## Quadratics

Relevant TEKS:

* A.6A
* A.6B
* A.6C
* A.7A
* A.7B
* A.7C
* A.8A
* A.8B

Problem types:

* domain and range of quadratics
* write quadratics from vertex and point
* write quadratics from zeros
* graph quadratics
* identify vertex, axis, zeros, intercepts
* factor/zero relationships
* transformations of `f(x) = x^2`
* solve quadratics by factoring, square roots, completing the square, and quadratic formula

## Exponentials

Relevant TEKS:

* A.9A
* A.9B
* A.9C
* A.9D
* A.9E

Problem types:

* domain and range of exponentials
* interpret `a` and `b`
* write exponential growth and decay functions
* graph exponential functions
* identify y-intercept and asymptote
* exponential regression and prediction

## Polynomials

Relevant TEKS:

* A.10A
* A.10B
* A.10C
* A.10D
* A.10E
* A.10F

Problem types:

* add and subtract polynomials
* multiply polynomials
* divide polynomials
* factor using GCF/distributive property
* factor trinomials
* perfect square trinomials
* difference of squares

## Radicals and Exponents

Relevant TEKS:

* A.11A
* A.11B

Problem types:

* simplify square roots
* laws of exponents
* rational exponents
* negative and zero exponents

## Functions and Sequences

Relevant TEKS:

* A.12A
* A.12B
* A.12C
* A.12D

Problem types:

* determine if a relation is a function
* evaluate function notation
* recursive sequences
* explicit arithmetic sequences
* explicit geometric sequences

---

# Codex Instructions for TEKS-Aligned Problem Creation

When creating a new Algebra 1 MOM problem, Codex should:

1. Identify the TEKS standard first.
2. Determine the specific skill within that standard.
3. Use the repository style guide for formatting.
4. Use the MOM documentation summaries and macro notes for valid syntax.
5. Create clean randomized values.
6. Ensure all answer choices are unique.
7. Include targeted feedback for common student mistakes.
8. Include `$showanswer` with the answer first, then the rationale.
9. Add student guide HTML when requested.
10. Include a short note explaining how the problem supports the TEKS.

Recommended output files for each problem:

```text
common-control.txt
question-text.html
student-guide.html
notes.md
```

Recommended `notes.md` format:

```md
# Problem Notes

Course: Algebra 1  
TEKS:  
Topic:  
Skill:  
Problem Type:  
Minimum Variations:  
Calculator:  
Student Guide:  

## TEKS Alignment

This problem supports the standard by asking students to...

## Randomization Notes

- 

## Common Wrong Answers Detected

- 

## Testing Checklist

- [ ] All randomized values produce valid answers.
- [ ] Answer choices are unique.
- [ ] Correct answer is displayed first in `$showanswer`.
- [ ] Feedback does not give away the answer too early.
- [ ] Font is 14pt.
- [ ] Layout is Chromebook-friendly.
```
