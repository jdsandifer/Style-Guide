# C++

Our main style in C++ is to follow every style rule in PHP. This document only describes styles specific to C++.
If you can't find something in here, it means you need to refer to our [PHP](https://github.com/Expensify/Style-Guide/blob/master/php.md) (or [SQL](https://github.com/Expensify/Style-Guide/blob/master/sql.md)) style.

The only notable difference with the PHP style is that concatenation operators *must* be surrounded by spaces.

## Documentation

TODO

## Namespace

The `using namespace` statement is *only* allowed on the `std` namespace. That means `std::` does *not have to* be prefixed everywhere.

## Pointers and references

The `&` and `*` *must* stick to the type, like this: `const std::string& var`, `Command* cmd`.

When using these on variables, they must stick to the variable name.

## const

`const` *should* be used to achieve specific objectives, generally to avoid extraneous copies. A key scenario would be when passing an object by pointer or reference that shouldn't be modified, rather than by copy. Example:

```cpp
string foo(const string& dontChangeThis)
{
    return dontChangeThis + "bar";
}
```

In this case, the const reference in the parameter to `foo()` assures the caller that this function won't modify the object being passed in.

Use `const` in a sparing, intentional manner, aiming for code clarity and simplicity.
