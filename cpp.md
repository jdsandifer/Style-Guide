# C++

Our main style in C++ is to follow every style rule in PHP. This document only describes styles specific to C++.
If you can't find something in here, it means you need to refer to our [PHP](https://github.com/Expensify/Style-Guide/blob/master/php.md) (or [SQL](https://github.com/Expensify/Style-Guide/blob/master/sql.md)) style.

The only notable difference with the PHP style is that concatenation operators *must* be surrounded by spaces.

## Documentation

TODO

## Namespace prefix

`std` and other namespaces *must* be prefixed everywhere. To keep things consistent, when calling a class method / using a class variable
 from inside the same class, the `ClassName` *should* be prefixed.

## Pointers and references

The `&` and `*` *must* stick to the type, like this: `const std::string& var`, `Command* cmd`.

When using these on variables, they must stick to the variable name.

## const

`const` *should* be used to achieve specific objectives, generally to avoid extraneous copies. A key scenario would be when passing an object by pointer or reference that shouldn't be modified, rather than by copy.  Example:

```cpp
string foo(const std::string& dontChangeThis)
{
    return dontChangeThis + "bar";
}
```

In this case, the const reference in the parameter to `foo()` assures the caller that this function won't modify the object being passed in.

However, `const` *should not* be used merely because the situation allows it (eg, you have a variable that you don't intend to modify again) -- just because you don't intend to modify it doesn't mean some future programmer might want to. Unless you have a very specific reason to *prevent* someone from modifying it, don't complicate their lives unnecessarily.  For example, do not use `const` in these scenarios:

 ```cpp
const int foo(const int a)
{
  const int b = a + 1;
  return b;
}
```

This would compile, but there's no reason to restrict the caller from modifying the return value. Furthermore, given that a copy of the `a` parameter has been made on the stack inside the function's scope, there's no reason to make it const either. And even though the `b` variable on the inside won't be modified after definition, there's no reason to actively prevent it from being modified should it make sense in the future.

Use `const` in a sparing, intentional manner, aiming for code clarity and simplicity.
