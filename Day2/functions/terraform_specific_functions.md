# Terraform-specific Functions

Terraform-specific functions include built-in provider-style functions that are specific to Terraform itself, plus the `type` function.

## provider::terraform::encode_tfvars
- Purpose: Converts an object value into a string containing a Terraform `.tfvars` representation.
- Arguments: `object`
- Returns: A string that describes the object in `.tfvars` format.
- Syntax: `provider::terraform::encode_tfvars(object)`

Example:
```hcl
provider::terraform::encode_tfvars({name = "app", env = "prod"})
// Output: "name = \"app\"\nenv = \"prod\"\n"
```

## provider::terraform::decode_tfvars
- Purpose: Parses a `.tfvars` string and returns an object describing the raw variable values it defines.
- Arguments: `string`
- Returns: An object representing the variable values defined in the input string.
- Syntax: `provider::terraform::decode_tfvars(string)`

Example:
```hcl
provider::terraform::decode_tfvars("name = \"app\"\nenv = \"prod\"\n")
// Output: {name = "app", env = "prod"}
```

## provider::terraform::encode_expr
- Purpose: Produces a Terraform expression string that approximates a given value.
- Arguments: `value`
- Returns: A string containing Terraform language expression syntax for the value.
- Syntax: `provider::terraform::encode_expr(value)`

Example:
```hcl
provider::terraform::encode_expr([1, 2, 3])
// Output: "[1, 2, 3]"
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
