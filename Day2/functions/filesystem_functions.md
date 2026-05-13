# Terraform Filesystem Functions

Terraform filesystem functions are used to inspect and manipulate paths, read file contents, and generate file lists from the local filesystem.

## abspath
- Purpose: Converts a filesystem path into an absolute path.
- Arguments: `path`
- Returns: The absolute path corresponding to the input path.
- Syntax: `abspath(path)`

Example:
```hcl
abspath("./config.tf")
// Output: "/absolute/path/to/config.tf"
```

## basename
- Purpose: Extracts the final component of a filesystem path.
- Arguments: `path`
- Returns: The last path segment from the input path.
- Syntax: `basename(path)`

Example:
```hcl
basename("/tmp/project/main.tf")
// Output: "main.tf"
```

## dirname
- Purpose: Removes the final component from a filesystem path.
- Arguments: `path`
- Returns: The directory path containing the input file.
- Syntax: `dirname(path)`

Example:
```hcl
dirname("/tmp/project/main.tf")
// Output: "/tmp/project"
```

## pathexpand
- Purpose: Expands a path that begins with `~` to the current user's home directory.
- Arguments: `path`
- Returns: The expanded path.
- Syntax: `pathexpand(path)`

Example:
```hcl
pathexpand("~/project/vars.tf")
// Output: "/home/user/project/vars.tf"
```

## file
- Purpose: Reads the contents of a file and returns them as a string.
- Arguments: `path`
- Returns: The file contents.
- Syntax: `file(path)`

Example:
```hcl
file("./config.tf")
// Output: "resource \"aws_instance\" \"example\" { ... }"
```

## fileexists
- Purpose: Tests whether a file exists at the given path.
- Arguments: `path`
- Returns: `true` if the file exists; otherwise `false`.
- Syntax: `fileexists(path)`

Example:
```hcl
fileexists("./config.tf")
// Output: true
```

## fileset
- Purpose: Lists regular files that match a glob pattern in a specified directory.
- Arguments: `path, pattern`
- Returns: A set of matching file names.
- Syntax: `fileset(path, pattern)`

Example:
```hcl
fileset("./modules", "*.tf")
// Output: ["main.tf", "variables.tf", "outputs.tf"]
```

## filebase64
- Purpose: Reads the contents of a file and returns them encoded as Base64.
- Arguments: `path`
- Returns: A Base64-encoded string of the file contents.
- Syntax: `filebase64(path)`

Example:
```hcl
filebase64("./secret.txt")
// Output: "U2VjcmV0IFZhbHVlCg=="
```

## templatefile
- Purpose: Reads a file and renders it as a template using provided variables.
- Arguments: `path, vars`
- Returns: The rendered template string.
- Syntax: `templatefile(path, vars)`

Example:
```hcl
templatefile("./template.tpl", {name = "app", env = "prod"})
// Output: "resource \"aws_instance\" \"app\" { ... }"
```
