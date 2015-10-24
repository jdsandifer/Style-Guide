# C++

Our main style in C++ is to follow every style rule in PHP. This document only describes styles specific to C++.
If you can't find something in here, it means you need to refer to our PHP (or SQL) style.

## Namespace prefix

`std` and other namespaces *must* be prefixed everywhere. To keep things consistent, when calling a class method / using a class variable
 from inside the same class, the `ClassName` *should* be prefixed.

## Pointers / references / const

`const` *must* be used everywhere applicable.

The `&` and `*` *must* stick to the type, like this: `const std::string& var`, `Command* cmd`.

When using these on variables, they must stick to the variable name.
