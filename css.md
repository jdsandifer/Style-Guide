CSS Coding Standards
====================

## Table of Contents

1. [Introduction](#introduction)
2. [Spacing](#spacing)
3. [Formatting](#formatting)
4. [Misc](#misc)
5. [Examples](#examples)

## Introduction



## Spacing

* Use soft tabs set to 4 spaces. Spaces are the only way to guarantee code renders the same in any person's environment.
* Put spaces after `:` in property declarations, but never before.
* Put spaces before `{` in rule declarations.
* Put spaces before and after combinators, e.g. `li > a` instead of `li>a`.
* Put line breaks between rulesets.
* When grouping selectors, keep individual selectors to a single line.
* Place closing braces of declaration blocks on a new line.
* Each declaration should appear on its own line for more accurate error reporting and end with a `;` semicolon.

## Formatting

* Use hex color codes `#000000` (full 6 digits) unless using `rgba()` in raw CSS (SCSS' `rgba()` function is overloaded to accept hex colors as a param, e.g., `rgba(#000000, .5)`).
* Use `//` for comment blocks (instead of `/* */`).
* Use single line quotes `'` for strings, e.g. `url('http://...')`.
* Avoid specifying units for zero values, e.g., `margin: 0;` instead of `margin: 0px;`.
* Strive to limit use of shorthand declarations to instances where you must explicitly set all the available values.
* When using vendor prefixes align with soft spaces:

  ```scss
  -webkit-border-radius: 3px;
     -moz-border-radius: 3px;
          border-radius: 3px;
  ```

* All files must end with a single newline character:

  ```scss
  .last-rule {
      z-index: 2;
  }↵
  
  ```


## Misc

As a rule of thumb, avoid unnecessary nesting in SCSS. At most, aim for three levels. If you cannot help it, step back and rethink your overall strategy (either the specificity needed, or the layout of the nesting).

## Examples

Here are some good examples that more or less apply the above guidelines:

```scss
// Example of good basic formatting practices
.styleguide-format {
    background-color: rgba(0, 0, 0, .5);
    border: 1px solid #00fff00;
    color: #000000;
    z-index: 1;
}

// Example of individual selectors getting their own lines (for error reporting)
.multiple,
.classes,
.get-new-lines {
    display: block;
}

// Avoid unnecessary shorthand declarations
.not-so-good {
    margin: 0 0 20px;
}
.good {
    margin-bottom: 20px;
}

// Avoid spacing mistakes
.not-so-good {
    color :blue;
}
.even-worse{
 display :block }

.much-better {
    content: '4 soft spaces indentation, space after colon, single line quotation, semicolon';
}
```
