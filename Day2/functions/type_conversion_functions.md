# Terraform Type Conversion Functions

Terraform type conversion functions let you convert values between types, inspect expression results, and work with sensitive or ephemeral data.

## can
- Purpose: Checks whether an expression evaluates successfully without errors.
- Arguments: `expression`
- Returns: `true` if the expression produces a result, otherwise `false`.
- Syntax: `can(expression)`

Example:
```hcl
can(1 / 0)
// Output: false
```

## ephemeralasnull
- Purpose: Converts an ephemeral value to null.
- Arguments: `value`
- Returns: `null` for ephemeral values.
- Syntax: `ephemeralasnull(value)`

Example:
```hcl
ephemeralasnull(terraform.workspace)
// Output: null
```

## issensitive
- Purpose: Tests whether Terraform treats a value as sensitive.
- Arguments: `value`
- Returns: `true` if the value is marked sensitive; otherwise `false`.
- Syntax: `issensitive(value)`

Example:
```hcl
issensitive(sensitive("secret"))
// Output: true
```

## nonsensitive
- Purpose: Removes the sensitive marking from a value.
- Arguments: `value`
- Returns: A copy of the value without sensitive masking.
- Syntax: `nonsensitive(value)`

Example:
```hcl
nonsensitive(sensitive("secret"))
// Output: "secret"
```

## sensitive
- Purpose: Marks a value as sensitive so Terraform treats it as secret.
- Arguments: `value`
- Returns: The same value with the sensitive flag applied.
- Syntax: `sensitive(value)`

Example:
```hcl
sensitive("secret")
// Output: sensitive("secret")
```

## tobool
- Purpose: Converts a value to a boolean.
- Arguments: `value`
- Returns: The boolean representation of the input.
- Syntax: `tobool(value)`

Example:
```hcl
tobool("true")
// Output: true
```

## tolist
- Purpose: Converts a value to a list.
- Arguments: `value`
- Returns: A list representation of the input.
- Syntax: `tolist(value)`

Example:
```hcl
tolist("a")
// Output: ["a"]
```

## tomap
- Purpose: Converts a value to a map.
- Arguments: `value`
- Returns: A map representation of the input.
- Syntax: `tomap(value)`

Example:
```hcl
tomap(["a", "b"])
// Output: {"a" = "b"}
```

## tonumber
- Purpose: Converts a value to a number.
- Arguments: `value`
- Returns: The numeric representation of the input.
- Syntax: `tonumber(value)`

Example:
```hcl
tonumber("42")
// Output: 42
```

## toset
- Purpose: Converts a value to a set.
- Arguments: `value`
- Returns: A set representation of the input.
- Syntax: `toset(value)`

Example:
```hcl
toset(["a", "b", "a"])
// Output: ["a", "b"]
```

## tostring
- Purpose: Converts a value to a string.
- Arguments: `value`
- Returns: The string representation of the input.
- Syntax: `tostring(value)`

Example:
```hcl
tostring(42)
// Output: "42"
```

## try
- Purpose: Evaluates expressions in order and returns the first one that does not error.
- Arguments: `expr1, expr2, ...`
- Returns: The result of the first successful expression.
- Syntax: `try(expr1, expr2, ... )`

Example:
```hcl
try(1 / 0, 2)
// Output: 2
```

## type
- Purpose: Returns the type of a given value.
- Arguments: `value`
- Returns: A type object describing the value.
- Syntax: `type(value)`

Example:
```hcl
type("hello")
// Output: string
```
