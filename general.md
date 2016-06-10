Language agnostic Coding Standard
=====================

## Table of Contents
1. [Acronyms](#acronyms)
1. [Abbreviations](#abbreviations)
1. [Simplicity](#simplicity)

## Acronyms
- When using acronyms, only upper case the first letter, treating it as a regular word.

```PHP
   public function setUdfs($udfs)
   {
     ...
   }
```

## Abbreviations
- Don't use abbreviations if you can avoid it
- When referencing an ID, you can make "ID" all caps.

```php
   public function setReportID($id)
   {
      ...
   }
```

```js
   var policyID = 1234;
```

## Simplicity
As an engineer, you should strive to keep things simple and relevant.

> Don't engineer something in the hope it will be useful for someone someday. Engineer something so that it's useful for you today.

- Build things that you know will need to be refactored when/if more functionality is desired in the future
- Don't add functionality that is not in use RIGHT NOW
- Don't engineer things that you think will have value later
- Don't use a class when a function will do

```php
// Bad
class Foo
{
   public function __construct($data)
   {
      ...
   }
   
   public function doSomethingWithBar()
   {
      ...
   }
}
$Foo = new Foo('bar');
$Foo->doSomethingWithBar();


// Good
function doSomethingWithData($data)
{
   ...
}
doSomethingWithData('bar');
```

- Don't add getters and setters when referencing properties has no side effects

```php
// Bad
class Foo
{
   private $bar;
   
   public function __construct($bar)
   {
      $this->setBar($bar);
   }
   
   public function setBar($val)
   {
      ...
   }
   
   public function getBar()
   {
      ...
   }
}
$Foo = new Foo('bar');
echo $Foo->getBar();


// Good
class Foo
{
   public $bar;
   
   public function __construct($bar)
   {
      $this->bar = $bar;
   }
}
$Foo = new Foo('bar');
echo $Foo->bar;
```

**[⬆ back to top](#table-of-contents)**
