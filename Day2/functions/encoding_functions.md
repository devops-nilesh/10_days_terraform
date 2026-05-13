# Terraform Encoding Functions

Terraform encoding functions let you convert data between text formats, encode or decode binary-safe strings, and parse or emit structured payloads.

## base64decode
- Purpose: Decodes a Base64-encoded string back into the original string.
- Arguments: `string`
- Returns: The decoded string.
- Syntax: `base64decode(string)`

Example:
```hcl
base64decode("SGVsbG8gV29ybGQ=")
// Output: "Hello World"
```

## base64encode
- Purpose: Encodes a string as Base64.
- Arguments: `string`
- Returns: A Base64-encoded representation of the input string.
- Syntax: `base64encode(string)`

Example:
```hcl
base64encode("Hello World")
// Output: "SGVsbG8gV29ybGQ="
```

## base64gzip
- Purpose: Compresses a string using gzip and then encodes the compressed bytes as Base64.
- Arguments: `string`
- Returns: A Base64-encoded gzip representation of the input string.
- Syntax: `base64gzip(string)`

Example:
```hcl
base64gzip("Hello World")
// Output: "H4sIAAAAAAAA/..."
```

## csvdecode
- Purpose: Parses a CSV-formatted string and converts it into a list of maps.
- Arguments: `string`
- Returns: A list of maps where each row becomes a map and the first CSV row is treated as headers.
- Syntax: `csvdecode(string)`

Example:
```hcl
csvdecode("name,env\napp,prod\n")
// Output: [{name = "app", env = "prod"}]
```

## jsondecode
- Purpose: Decodes a JSON string into a Terraform value.
- Arguments: `string`
- Returns: The decoded object, list, string, number, boolean, or null value.
- Syntax: `jsondecode(string)`

Example:
```hcl
jsondecode("{\"name\": \"app\", \"port\": 8080}")
// Output: {name = "app", port = 8080}
```

## jsonencode
- Purpose: Encodes a Terraform value as a JSON string.
- Arguments: `value`
- Returns: A JSON-formatted string representation of the input value.
- Syntax: `jsonencode(value)`

Example:
```hcl
jsonencode({name = "app", port = 8080})
// Output: "{\"name\":\"app\",\"port\":8080}"
```

## textdecodebase64
- Purpose: Decodes a Base64 string and interprets the result as text.
- Arguments: `string`
- Returns: The decoded string in the specified character encoding.
- Syntax: `textdecodebase64(string)`

Example:
```hcl
textdecodebase64("SGVsbG8gV29ybGQ=")
// Output: "Hello World"
```

## textencodebase64
- Purpose: Encodes a string into Base64 after converting it to the specified character encoding.
- Arguments: `string`
- Returns: A Base64-encoded text string.
- Syntax: `textencodebase64(string)`

Example:
```hcl
textencodebase64("Hello World")
// Output: "SGVsbG8gV29ybGQ="
```

## urlencode
- Purpose: Encodes a string using URL encoding.
- Arguments: `string`
- Returns: A string where reserved URI characters are percent-encoded.
- Syntax: `urlencode(string)`

Example:
```hcl
urlencode("hello world?foo=bar")
// Output: "hello%20world%3Ffoo%3Dbar"
```

## yamldecode
- Purpose: Parses a YAML string into a Terraform value.
- Arguments: `string`
- Returns: A decoded representation of the YAML input.
- Syntax: `yamldecode(string)`

Example:
```hcl
yamldecode("name: app\nenv: prod\n")
// Output: {name = "app", env = "prod"}
```

## yamlencode
- Purpose: Encodes a Terraform value as a YAML string.
- Arguments: `value`
- Returns: A YAML-formatted string representation of the input value.
- Syntax: `yamlencode(value)`

Example:
```hcl
yamlencode({name = "app", env = "prod"})
// Output: "name: app\nenv: prod\n"
```
