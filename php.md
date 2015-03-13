PHP Coding Standard
=====================

0. Introduction
---------------

Our PHP style guide is based on [[PSR-1]] and [[PSR-2]].
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [[RFC 2119]].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[PSR-2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md


1. Overview
-----------

- Code MUST use 4 spaces for indenting, not tabs.

> N.b.: Using only spaces, and not mixing spaces with tabs, helps to avoid
> problems with diffs, patches, history, and annotations. The use of spaces
> also makes it easy to insert fine-grained sub-indentation for inter-line 
> alignment.


- There MUST NOT be a hard limit on line length; the soft limit MUST be 120
  characters; lines SHOULD be 80 characters or less.
4. 

- Files MUST use only `<?php` and `<?=` tags.

- Files MUST use only UTF-8 without BOM for PHP code.

- Files SHOULD *either* declare symbols (classes, functions, constants, etc.)
  *or* cause side-effects (e.g. generate output, change .ini settings, etc.)
  but SHOULD NOT do both.
  
- PHP [keywords] MUST be in lower case.

[keywords]: http://php.net/manual/en/reserved.keywords.php


2. Files
--------

### 2.1. PHP Tags

- PHP code MUST use the long `<?php ?>` tags or the short-echo `<?= ?>` tags; it
MUST NOT use the other tag variations.

- The closing `?>` tag MUST be omitted from files containing only PHP.

### 2.2. Character Encoding

- PHP code MUST use only UTF-8 without BOM.
- All PHP files MUST use the Unix LF (linefeed) line ending.
- All PHP files MUST end with a single blank line.

### 2.3. Side Effects

A file SHOULD declare new symbols (classes, functions, constants,
etc.) and cause no other side effects, or it SHOULD execute logic with side
effects, but SHOULD NOT do both.

The phrase "side effects" means execution of logic not directly related to
declaring classes, functions, constants, etc., *merely from including the
file*.

"Side effects" include but are not limited to: generating output, explicit
use of `require` or `include`, connecting to external services, modifying ini
settings, emitting errors or exceptions, modifying global or static variables,
reading from or writing to a file, and so on.

The following is an example of a file with both declarations and side effects;
i.e, an example of what to avoid:

```php
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
```

The following example is of a file that contains declarations without side
effects; i.e., an example of what to emulate:

```php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
```


3. Namespaces
-------------

- Namespaces  MUST follow [PSR-4]].

- When present, there MUST be one blank line after the `namespace` declaration.

- When present, all `use` declarations MUST go after the `namespace`
declaration.

- There MUST be one `use` keyword per declaration.

- There MUST be one blank line after the `use` block.

For example:

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...

```


4. Class
--------
- The term "class" refers to all classes, interfaces, and traits.
- Classes without a namespace MUST follow [[PSR-0]] : the class name is mapping the directory, using underscores has directory seperator.
- Class names MUST be declared in `StudlyCaps`.
- Visibility MUST be declared on all properties and methods; `abstract` and
  `final` MUST be declared before the visibility; `static` MUST be declared
  after the visibility.
- Opening braces for classes MUST go on the next line, and closing braces MUST
  go on the next line after the body.
- Opening braces for methods MUST go on the next line, and closing braces MUST
  go on the next line after the body.


### 4.1. Constants

- Class constants MUST be declared in all upper case with underscore separators.
For example:

```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```


### 4.2. Properties

- Visibility MUST be declared on all properties.
- The `var` keyword MUST NOT be used to declare a property.
- There MUST NOT be more than one property declared per statement.
- Property names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.
- Property MUST be explicitely defined in the root of the class
- The default value of a property MUST be set explicitly.
- A property declaration looks like the following.
- PHPDoc with the type definition MUST be added on properties

```php
<?php

// Good
class ClassName
{
	/**
	 * @var null|string
	 */
    public $foo = null;
}

// Bad
class ClassName
{
    public function run()
    {
    	$this->foo = 5;
    }
}

```



### 4.3. Methods

- Visibility MUST be declared on all methods.
- Method names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.
- Method names MUST NOT be declared with a space after the method name. 
- The opening brace MUST go on its own line
- The closing brace MUST go on the next line following the body. 
- There MUST NOT be a space after the opening parenthesis
- There MUST NOT be a space before the closing parenthesis.

A method declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```   


- PHPDoc MUST be added on every method
- PHPDoc description MAY be omitted when the action of the method is obvious. Any push back on this during the review process MUST be followed by an addition of the description without any discussion
- PHPDoc MUST include parameter type then parameter name
- Mixed type SHOULD be avoid as much as possible
- Parameter description MAY be omitted
- PHPDoc MUST inclde return type if the return is none void 

```php
<?php
namespace Vendor\Package;

class ClassName
{
	/**
	 * @param string $arg1
	 * @param array  $arg2
	 */
    public function fooBarBaz($arg1, array $arg2 = [])
    {
        // method body
    }
    
    /**
     * This function tells you how awesome bob donuts ar
     *
     * @return int
     */
    public function bob()
    {
    	return 42;
    }
}
```   



### 4.4. Method Arguments

- In the argument list, there MUST NOT be a space before each comma, and there
MUST be one space after each comma.

- Method arguments with default values MUST go at the end of the argument
list.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

- Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

When the argument list is split across multiple lines, the closing parenthesis
and opening brace MUST be placed together on their own line with one space
between them.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

- Type hinting SHOULD be used as often as possible.


### 4.5. Extends, Implements and Traits

- The `extends` and `implements` keywords MUST be declared on the same line as
the class name.
- The opening brace for the class MUST go on its own line
- The closing brace for the class MUST go on the next line after the body.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```

Lists of `implements` MAY be split across multiple lines, where each
subsequent line is indented once. When doing so, the first item in the list
MUST be on the next line, and there MUST be only one interface per line.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```

- Traits MUST be define immediately after the class name

```PHP
class Yop extends Lait
{
	use MyAwesomeTrait;
	
	public function __construct()
	{
	
	}
}
```


### 4.6. `abstract`, `final`, and `static`

- When present, the `abstract` and `final` declarations MUST precede the
visibility declaration.

- When present, the `static` declaration MUST come after the visibility
declaration.

```php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
```

### 4.7. Method and Function Calls

When making a method or function call, there MUST NOT be a space between the
method or function name and the opening parenthesis, there MUST NOT be a space
after the opening parenthesis, and there MUST NOT be a space before the
closing parenthesis. In the argument list, there MUST NOT be a space before
each comma, and there MUST be one space after each comma.

```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

```php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```


5. Control Structures
---------------------

The general style rules for control structures are as follows:

- There MUST be one space after the control structure keyword
- There MUST NOT be a space after the opening parenthesis
- There MUST NOT be a space before the closing parenthesis
- There MUST be one space between the closing parenthesis and the opening
  brace
- The structure body MUST be indented once
- The closing brace MUST be on the next line after the body

The body of each structure MUST be enclosed by braces. This standardizes how
the structures look, and reduces the likelihood of introducing errors as new
lines get added to the body.


### 5.1. `if`, `elseif`, `else`

An `if` structure looks like the following. Note the placement of parentheses,
spaces, and braces; and that `else` and `elseif` are on the same line as the
closing brace from the earlier body.

```php
<?php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```

The keyword `elseif` SHOULD be used instead of `else if` so that all control
keywords look like single words.

- Strict equality testing (`===`) SHOULD be used as often as you can


### 5.2. `switch`, `case`

A `switch` structure looks like the following. Note the placement of
parentheses, spaces, and braces. 
- The `case` statement MUST be indented once from `switch`, and the `break` keyword (or other terminating keyword) MUST be indented at the same level as the `case` body. 
- There MUST be a comment such as `// no break` when fall-through is intentional in a non-empty `case` body.

```php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```


### 5.3. `while`, `do while`

A `while` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
while ($expr) {
    // structure body
}
```

Similarly, a `do while` statement looks like the following. Note the placement
of parentheses, spaces, and braces.

```php
<?php
do {
    // structure body;
} while ($expr);
```

### 5.4. `for`

A `for` statement looks like the following. Note the placement of parentheses,
spaces, and braces.

```php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```

### 5.5. `foreach`
    
A `foreach` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```

### 5.6. `try`, `catch`

A `try catch` block looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```

6. Closures
-----------

Closures MUST be declared with a space after the `function` keyword, and a
space before and after the `use` keyword.

The opening brace MUST go on the same line, and the closing brace MUST go on
the next line following the body.

There MUST NOT be a space after the opening parenthesis of the argument list
or variable list, and there MUST NOT be a space before the closing parenthesis
of the argument list or variable list.

In the argument list and variable list, there MUST NOT be a space before each
comma, and there MUST be one space after each comma.

Closure arguments with default values MUST go at the end of the argument
list.

A closure declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

```php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```

Argument lists and variable lists MAY be split across multiple lines, where
each subsequent line is indented once. When doing so, the first item in the
list MUST be on the next line, and there MUST be only one argument or variable
per line.

When the ending list (whether or arguments or variables) is split across
multiple lines, the closing parenthesis and opening brace MUST be placed
together on their own line with one space between them.

The following are examples of closures with and without argument lists and
variable lists split across multiple lines.

```php
<?php
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
```

Note that the formatting rules also apply when the closure is used directly
in a function or method call as an argument.

```php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```


7. Variables
------------

7.1. Null
---------

- MUST be lower case
- Use mosty to indicate that something is not instanciated or wrong


7.2. Bool
---------

- Must be lower case


7.3. String
------------

- to be filled


7.4. Number
-----------

- PHPDoc int or integer
- 

7.5. Array
----------

- Array are not a scalar type, and MUST be type hinted
- Use short notation to create arrays

```php
// Good
$n = [];

// Bad
$b = array();
```

- When building a list that is going to grow in the future, align the items and keep a trailing comma

```PHP
$myList = [
	'a',
	'b',
	'c',
];
```











- When function is deprecated in favor of an other one, use the `@deprecated` tag and indicate
