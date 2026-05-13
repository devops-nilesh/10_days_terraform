# Terraform Numeric Functions

Terraform includes built-in numeric functions that help you transform and evaluate numbers inside expressions.

## ceil
- Rounds a number up to the nearest integer.
- Syntax: `ceil(number)`

Example:
```hcl
ceil(4.2)
// Output: 5
```

## floor
- Rounds a number down to the nearest integer.
- Syntax: `floor(number)`

Example:
```hcl
floor(4.8)
// Output: 4
```

## log
- Returns the logarithm of a number with a specified base.
- Syntax: `log(number, base)`

Example:
```hcl
log(100, 10)
// Output: 2
```

## max
- Returns the largest value from its arguments.
- Syntax: `max(value1, value2, ...)`

Example:
```hcl
max(3, 7, 5)
// Output: 7
```

## min
- Returns the smallest value from its arguments.
- Syntax: `min(value1, value2, ...)`

Example:
```hcl
min(3, 7, 5)
// Output: 3
```

## parseint
- Converts a string representation of an integer into a number.
- Syntax: `parseint(string, base)`

Example:
```hcl
parseint("FF", 16)
// Output: 255
```

## pow
- Raises a number to a power.
- Syntax: `pow(base, exponent)`

Example:
```hcl
pow(2, 3)
// Output: 8
```

## abs
- Returns the absolute value of a number.
- Syntax: `abs(number)`

Example:
```hcl
abs(-5)
// Output: 5
```

## signum
- Returns the sign of a number.
- Output is `-1` for negative values, `0` for zero, and `1` for positive values.
- Syntax: `signum(number)`

Example:
```hcl
signum(-5)
// Output: -1
```

