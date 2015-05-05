# Java Coding Standards

## Table of contents

1. [Introduction](#introduction)
2. [Class](#class)
3. [Formatting](#formatting)
4. [Name](#naming)
5. [Javadoc](#javadoc)
 
## Introduction

Our Java style guide is tightly based on the [Google Java Style](https://google-styleguide.googlecode.com/svn/trunk/javaguide.html), with a few notable differences. This document focuses on style guides and coding standards that differ from, or extend it. If a rule is not defined in this document, assume the Google style should be used.

**[⬆ back to top](#table-of-contents)**

## Class

### Class member ordering

From [Google's style guide](https://google-styleguide.googlecode.com/svn/trunk/javaguide.html#s3.4.2-class-member-ordering):
> The ordering of the members of a class can have a great effect on learnability, but there is no single correct recipe for how to do it. Different classes may order their members differently.

> What is important is that each class order its members in ___some___ _logical order_, which its maintainer could explain if asked. For example, new methods are not just habitually added to the end of the class, as that would yield "chronological by date added" ordering, which is not a logical ordering.

In addition to that, the following order of definitions is preferred:

1. abstract methods, if any,
2. public and static attributes,
3. protected and private attributes,
4.  protected and private methods

**[⬆ back to top](#table-of-contents)**

## Formatting

### Braces

Braces are mandatory where optional. One line statements shall not be used.

```java
if (foo) {
    bar();
}
```

### Indentation

- Indentation uses __4__ spaces. Tabs shall not be used.
- Chained method invocations should all be placed on a new line after the first one, indented with __8__ spaces. The dot `.` should be placed on the new line.

```java
ExpensifyAPIResponse apiResponse = api.prepareCommand("Command")
        .addParameter("key", "value")
        .execute();
```

### Enums

Enumerations shall be formatted as follows:

* One value per line,
* Every value ends with a comma (`,`),
* A semicolon (`;`) is added after all the definitions, on a separate line.

```java
/**
 * Some explanation
 */
public enum FooBarEnum {
    FOO,
    BAR,
    FOOBAR,
    ;
}
```

### Line wrapping

The default column limit is __100__ characters. However, when it makes sense, line-wrapping is not mandatory (_eg._ if a line is 102 characters long).

### Horizontal alignment
- Not recommended

**[⬆ back to top](#table-of-contents)**

## Naming

### Attributes

- Public static final fields are `UPPERCASE_WITH_UNDERSCORES`.
- All other fields should use `lowerCamelCase`.

### Type Variables

Each type variable shall be named in the same way as a class (`UpperCamelCase`), followed by the capital letter  `T`. This has the advantage of being more readable than one-letter types (_eg._ `List<T>`), and easily distinguishable from a regular class name at the same time.

Examples:

* `ConfigurationT`
* `DataT`

### Enums

Enums' names shall end with `Enum`.

Examples:

* `FooBarEnum` instead of `FooBar`

**[⬆ back to top](#table-of-contents)**

## Javadoc

Javadoc is mandatory for:

- class definitions
- method definitions

It is strongly recommended for attributes definitions, unless for obvious ones.

#### Exception: overrides
Javadoc is optional on a method that overrides a parent method.

### At-clauses

- `@param` must be specified for every parameter of a method. A description must be specified, unless the name of the parameter is enough to determine what it corresponds to, without any possible ambiguity.
- `@return` must be specified when the method is not `void`. A description of the returned object is recommended when not clearly specified in the method's description.
- `@override` must specify why, or in favor of which other method the method is deprecated.
- `@throws` must list every different exception thrown by the method on a separate line.

**[⬆ back to top](#table-of-contents)**

## Netbeans formatter

Todo

**[⬆ back to top](#table-of-contents)**
