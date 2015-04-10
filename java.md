# Java Coding Standards

## Table of contents

1. [Introduction](#introduction)
 
## Introduction

Our Java style guide is tightly based on the [Google Java Style](https://google-styleguide.googlecode.com/svn/trunk/javaguide.html), with a few notable differences. This document focuses on style guides and coding standards that differ from, or extend it. If a rule is not defined in this document, assume the Google style should be used.

**[⬆ back to top](#table-of-contents)**

## Class

### Class member ordering ([ref](https://google-styleguide.googlecode.com/svn/trunk/javaguide.html#s3.4.2-class-member-ordering))

> The ordering of the members of a class can have a great effect on learnability, but there is no single correct recipe for how to do it. Different classes may order their members differently.

> What is important is that each class order its members in ___some___ _logical order_, which its maintainer could explain if asked. For example, new methods are not just habitually added to the end of the class, as that would yield "chronological by date added" ordering, which is not a logical ordering.

In addition to that, the following order of definitions is preferred:

1. abstract methods, if any,
2. public and static attributes,
3. protected and private attributes,
4.  protected and private methods
	

## Formatting


### Braces

Braces are mandatory where optional. One line statements shall not be used.

```java
if (foo) {
    bar();}
```

### Indentation

- Indentation uses __4__ spaces. Tabs shall not be used.
- Chained method invocations should all be placed on a new line after the first one, indented with __8__ spaces. The dot `.` should be placed on the new line.

```java
ExpensifyAPIResponse apiResponse = api.prepareCommand("Command")
        .addParameter("key", "value")
        .execute();
```

### Line wrapping

Default line wrapping  100 characters, allowed more when it makes sense

### Horizontal alingment
- allowed, not recommended


## Naming

### Rules common to all identifiers

- For private attributes, no prefixing with like `_attribute` or `mAttribute`

### Attributes

- static attributes in uppercase
- private lowerCamelCase

**[⬆ back to top](#table-of-contents)**

## Netbeans formatter

**[⬆ back to top](#table-of-contents)**