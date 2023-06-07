---
weight: 30
Order: 3
Title: Regular Expressions Primer
description: An overview of how to use regular expressions to find patterns within your documents.
---
## Very Basic Overview of Regular Expressions

If you are unfamiliar with regular expressions, review this documentation:

[RE2 Regular Expression Syntax](https://cran.r-project.org/web/packages/re2/vignettes/re2_syntax.html)

We support the RE2 regular expression flavor. It is mostly standard syntax, but it excludes
some advanced functions available in some other implementations which cause performance
degradation with certain types of expressions.

To get you started with regex, here are a few basic patterns:

```
Pattern      Description
-------      -----------
.            Match any character
\.           Match a literal . character
^            Match the beginning of the line
$            Match the end of the line
\s           Match a whitespace character
\S           Match a non-whitespace character
*            Match the preceding expression zero or more times
+            Match the preceding expression one or more times

Examples     Description
--------     -----------
.*           Match any character zero or more times
\s*          Match a whitespace character zero or more times
\S+          Match a non-whitespace character one or more times
\.js$        Match a line or filename that ends in ".js"
```
