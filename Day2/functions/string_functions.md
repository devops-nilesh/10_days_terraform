# Terraform String Functions

## chomp
- Removes trailing newline characters from a string.
- Syntax: `chomp(string)`

Example:
```hcl
chomp("Hello\n")
// Output: "Hello"
```

## endswith
- Checks whether a string ends with a given suffix.
- Syntax: `endswith(string, suffix)`

Example:
```hcl
endswith("Hello, world!", "world!")
// Output: true
```

## format
- Formats a string using printf-style placeholders.
- The first argument is a template string.
- Each `%` placeholder is replaced by the next value in the argument list.

Syntax:
```hcl
format(template, values...)
```

Common placeholders:
- `%s` — insert a string.
- `%d` — insert a decimal integer.
- `%t` — insert a boolean (`true` or `false`).
- `%v` — default formatting for the value’s type.
- `%#v` — JSON serialization.
- `%f` — decimal fraction.
- `%e` — scientific notation.
- `%g` — compact float (chooses between `%f` and `%e`).
- `%o` — octal integer.
- `%x` — hexadecimal integer, lowercase.
- `%X` — hexadecimal integer, uppercase.
- `%c` — Unicode character from an integer.
- `%%` — literal percent sign.

Examples:
```hcl
format("Hello %s", "World")
// Output: "Hello World"

format("Count: %d", 42)
// Output: "Count: 42"

format("My name is %s and I am %d years old", "Alice", 30)
// Output: "My name is Alice and I am 30 years old"

format("Flag: %t", true)
// Output: "Flag: true"

format("Value: %v", [1, 2, 3])
// Output: "Value: [1 2 3]"

format("%#v", {a = 1, b = "x"})
// Output: {"a":1,"b":"x"}

format("Pi: %.2f", 3.14159)
// Output: "Pi: 3.14"

format("Sci: %e", 12345.6789)
// Output: "Sci: 1.234568e+04"

format("Compact: %g", 12345.6789)
// Output: "Compact: 12345.7"

format("Octal: %o", 9)
// Output: "Octal: 11"

format("Hex: %x", 255)
// Output: "Hex: ff"

format("Hex: %X", 255)
// Output: "Hex: FF"

format("Char: %c", 65)
// Output: "Char: A"

format("Progress: 100%%")
// Output: "Progress: 100%"
```

## formatlist
- Produces a list of strings by applying a format string to one or more lists of values.
- Syntax: `formatlist(spec, values...)`

Examples:
```hcl
formatlist("Hello %s", ["Alice", "Bob", "Charlie"])
// Output: ["Hello Alice", "Hello Bob", "Hello Charlie"]

formatlist("Hello, %s!", ["Valentina", "Ander", "Olivia", "Sam"])
// Output:
// ["Hello, Valentina!", "Hello, Ander!", "Hello, Olivia!", "Hello, Sam!"]

formatlist("%s, %s!", ["Salutations"], ["Valentina", "Ander", "Olivia", "Sam"])
// Output:
// ["Salutations, Valentina!", "Salutations, Ander!", "Salutations, Olivia!", "Salutations, Sam!"]
```

## indent
- Adds spaces to the beginning of every line except the first line.
- Useful for formatting multi-line strings such as YAML, JSON, or Kubernetes manifests.
- Syntax: `indent(num_spaces, string)`

Example:
```hcl
output "formatted_description" {
  value = indent(2, var.description)
}
```

## join
- Concatenates a list of strings into a single string, inserting a separator between each element.
- Syntax: `join(separator, list)`

Examples:
```hcl
join("-", ["foo", "bar", "baz"])
// Output: "foo-bar-baz"

join(", ", ["foo", "bar", "baz"])
// Output: "foo, bar, baz"

join(", ", ["foo"])
// Output: "foo"
```

Notes:
- Convert non-string values first using `tostring()` or `format()`.
- An empty list returns an empty string.
- The opposite function is `split()`.

## lower
- Converts all characters in a string to lowercase.
- Useful for normalizing tags, labels, or resource names.

Examples:
```hcl
lower("HELLO")
// Output: "hello"

lower("ΓΕΙΑ ΣΟΥ")
// Output: "γεια σου"
```

## regex
- Applies a regular expression pattern to a string.
- Returns the first match or captured groups.
- If the pattern does not match, Terraform raises an error.
- Syntax: `regex(pattern, string)`

Examples:
```hcl
regex("foo", "foobar")
// Output: "foo"

regex("f(o+)b", "foooob")
// Output: ["oooo"]
```

Explanation:
- `regex("foo", "foobar")` returns the full match because there are no capture groups.
- `regex("f(o+)b", "foooob")` returns the captured group `"oooo"`.

## regexall
- Finds all matches of a regular expression in a string.
- Returns a list of matches.
- Syntax: `regexall(pattern, string)`

Example:
```hcl
regexall("[0-9]+", "item1 item22 item333")
// Output: ["1", "22", "333"]
```

Behavior:
- Returns every match found in the input string.
- Use it when you need multiple results, not just the first one.
- Returns an empty list when there is no match (unlike `regex`, which errors).

### Capture group behavior
- No capture groups: each match is returned as a string.
- Unnamed capture groups: each match is returned as a list of captured substrings.
- Named capture groups: each match is returned as a map.

### Examples
#### 1. Multiple matches (no capture groups)
```hcl
regexall("foo", "foo bar foo baz")
// Output: ["foo", "foo"]
```

#### 2. Unnamed capture groups
```hcl
regexall("f(o+)b", "foob fooob foooob")
// Output: [["o"], ["oo"], ["ooo"]]
```

#### 3. Named capture groups
```hcl
regexall("(?P<word>[a-z]+)", "one two three")
// Output:
// [
//   { word = "one" },
//   { word = "two" },
//   { word = "three" }
// ]
```

#### 4. Safe validation
```hcl
regexall("^[^@]+@[^@]+\\.[^@]+$", "not-an-email")
// Output: []
```

#### 5. Additional examples
```hcl
regexall("[a-z]+", "1234abcd5678efgh9")
// Output: ["abcd", "efgh"]

length(regexall("[a-z]+", "1234abcd5678efgh9"))
// Output: 2

length(regexall("[a-z]+", "123456789")) > 0
// Output: false
```

## replace
- Replaces text in a string.
- Syntax: `replace(string, substring, replacement)`
- If `substring` is wrapped in `/.../`, it is treated as a regular expression.
- When using regex, you can use `$1`, `$2`, etc. to insert captured groups.

Examples:
```hcl
replace("1 + 2 + 3", "+", "-")
// Output: "1 - 2 - 3"

replace("hello world", "/w.*d/", "everybody")
// Output: "hello everybody"
```

## split
- Splits a string into a list using a separator.
- Syntax: `split(separator, string)`

Examples:
```hcl
split(",", "foo,bar,baz")
// Output: ["foo", "bar", "baz"]

split(",", "foo")
// Output: ["foo"]

split(",", "")
// Output: [""]
```

## startswith
- Checks whether a string begins with a given prefix.
- Syntax: `startswith(string, prefix)`

Examples:
```hcl
startswith("hello world", "hello")
// Output: true

startswith("hello world", "world")
// Output: false
```

## strcontains
- Checks if one string contains another substring.
- Syntax: `strcontains(string, substr)`

Examples:
```hcl
strcontains("hello world", "wor")
// Output: true

strcontains("hello world", "wod")
// Output: false
```

## strrev
- Reverses the characters in a string.
- Uses Unicode grapheme clusters.
- Syntax: `strrev(string)`

Examples:
```hcl
strrev("hello")
// Output: "olleh"

strrev("a ☃")
// Output: "☃ a"
```

## substr
- Extracts a substring from a string.
- Syntax: `substr(string, offset, length)`

Example:
```hcl
substr("hello world", 1, 4)
// Output: "ello"
```

## templatestring
- Replaces placeholders in a string with values from a map.
- Placeholders use the `$${name}` syntax.
- Syntax: `templatestring(string, values_map)`

Example:
```hcl
templatestring("Hello $${who}", { who = "World" })
// Output: "Hello World"
```

Example with locals:
```hcl
locals {
  my_string = templatestring("Hello $${name}", {
    name = "World"
  })
}

output "example" {
  value = local.my_string
}
```

Dynamic templates:
- Define a template with placeholders.
- Pass a map of values for substitution.
- Terraform produces a final string using the map.

Example:
```hcl
variable "rg_pattern" {
  default = "rg-$${service}-$${env}-$${location}"
}

locals {
  rg_name = templatestring(var.rg_pattern, {
    service  = "demo"
    env      = "prod"
    location = "uksouth"
  })
}

output "rg_name" {
  value = local.rg_name
}
```

## title
- Converts the first letter of each word in a string to uppercase.
- Leaves other letters unchanged.
- Syntax: `title(string)`

Examples:
```hcl
title("hello world")
// Output: "Hello World"

title("HELLO WORLD")
// Output: "HELLO WORLD"
```

## trim
- Removes the specified set of characters from the start and end of a string.
- Syntax: `trim(string, character_set)`

Examples:
```hcl
trim("?!hello?!", "!?" )
// Output: "hello"

trim("foobar", "far")
// Output: "oob"

trim("   hello! world.!  ", "! " )
// Output: "hello! world."
```

## trimprefix
- Removes the specified prefix from the beginning of a string, only once.
- If the prefix is not present, the original string stays unchanged.
- Syntax: `trimprefix(string, prefix)`

Examples:
```hcl
trimprefix("helloworld", "hello")
// Output: "world"

trimprefix("helloworld", "cat")
// Output: "helloworld"

trimprefix("--hello", "-")
// Output: "-hello"
```

## trimsuffix
- Removes the specified suffix from the end of a string, only once.
- If the suffix is not present at the end, the original string stays unchanged.
- Syntax: `trimsuffix(string, suffix)`

Examples:
```hcl
trimsuffix("helloworld", "world")
// Output: "hello"

trimsuffix("helloworld", "cat")
// Output: "helloworld"

trimsuffix("hello--", "-")
// Output: "hello-"
```

## trimspace
- Removes Unicode whitespace from the start and end of a string.
- Includes spaces, tabs, newlines, and other Unicode space characters.
- Syntax: `trimspace(string)`

Example:
```hcl
trimspace("  hello\n\n")
// Output: "hello"
```


