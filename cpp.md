# C++

Our main style in C++ is to follow every style rule in PHP. This document only describes styles specific to C++.
If you can't find something in here, it means you need to refer to our [PHP](https://github.com/Expensify/Style-Guide/blob/master/php.md) (or [SQL](https://github.com/Expensify/Style-Guide/blob/master/sql.md)) style.

The only notable difference with the PHP style is that concatenation operators *must* be surrounded by spaces.

## Documentation


- Docs for params and return values *should* be avoided, unless they add useful additional information (eg, `@param reportID` in the code below is useless because because both the type and the name of the param are in the signature).
- Docs for methods *must* be in the header files.
- Each parameter *must* be documented using the following format: `* @param paramName description`. The description is required, otherwise it's just redundant information.
- Return values *must* be documented using the following format: `* @return description`. Similarly, the description is required, otherwise the docs are pointless.
- All exceptions thrown by a method *must* be documented using the following format: `* @throws InvalidJSONException [description]`. The description is required if it is not obvious why this exception can be thrown.

Thus, a doc block for a method *must* look like this:

```cpp
// Good
/**
 * Gets a reportNameValuePair's value
 *
 * @param name The name of the reportNameValuePair
 * @return the rNVP's value
 */
static string getValue(SQLite& db, uint64_t reportID, const string& name);

// Bad
/**
 * Gets a reportNameValuePair's value
 *
 * @param db
 * @param reportID
 * @param name     The name of the reportNameValuePair
 * @return the rNVP's value
 */
static string getValue(SQLite& db, uint64_t reportID, const string& name);
```

## Namespace

The `using namespace` statement is *only* allowed on the `std` namespace. That means `std::` does *not have to* be prefixed everywhere.

## Pointers and references

The `&` and `*` *must* stick to the type, like this: `const string& var`, `Command* cmd`.

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

Use `const` in a sparing, intentional manner, aiming for code clarity and simplicity.  For example, do not use `const` merely because you don't *intend* to change something, use it when it is so important not to change it that you want the compiler to forbid it.
