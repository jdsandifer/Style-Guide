CSS Coding Standards
====================

## Table of Contents

1. [Spacing](#spacing)
2. [Formatting](#formatting)
3. [Misc](#misc)
4. [Examples](#examples)

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

* Sort declarations alphabetically, except for vendor prefixes, variables and mixins. Variables and mixins (like `@include` or `@extend`) always belong to the top followed by an empty line.
* Use full 6 digits, lower cased hex color codes `#00aa00`. When using SCSS, the `rgba()` method will support hex colors as a param, e.g., `rgba(#00ff00, 0.5)`. In raw CSS it is permitted to break this rule when using `rgba()` only.
* Use `//` for comment blocks (instead of `/* */`).
* Use single line quotes `'` for strings, e.g. `url('http://...')`.
* Avoid specifying units for zero values, e.g. `margin: 0` instead of `margin: 0px`.
* Add leading zeros as in `0.5`.
* Always use double colons with pseudo elements (e.g. `.foo::after`) and single colons with pseudo classes (e.g. `.foo:hover`)
* Strive to limit use of shorthand declarations to instances where you must explicitly set all the available values.
 * When using shorthands make sure that values are as concise as possible, e.g. `margin: 0 5px` instead of `margin: 0 5px 0 5px`.
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

* When concatenating strings and variables use `#{}` style interpolation, e.g. `url('#{ $baseURL }/image.jpg')`


## Misc

As a rule of thumb, avoid unnecessary nesting in SCSS. At most, aim for three levels. If you cannot help it, step back and rethink your overall strategy (either the specificity needed, or the layout of the nesting).

## Examples

Here are some good examples that more or less apply the above guidelines:

```scss
// Example of good basic formatting practices
.styleguide-format {
    background-color: rgba(#000000, 0.5);
    border: 1px solid #00ff00;
    color: #ffffff;
    display: block;
    z-index: 1;
}

// Example of individual selectors getting their own lines (for error reporting)
.multiple,
.classes,
.get-new-lines {
    display: block;
}

// Avoid unnecessary shorthand declarations
// e.g. if you only want to modify the bottom margin:
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
 content :"abc" }

.much-better {
    content: '4 soft spaces indentation, space after colon, single quotes, semicolon';
}
```
