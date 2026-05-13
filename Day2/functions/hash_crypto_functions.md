# Terraform Hash and Crypto Functions

Terraform hash and crypto functions let you compute hashes, generate UUIDs, and perform RSA decryption in configuration language expressions.

## base64sha256
- Purpose: Computes the SHA256 hash of a given string and encodes the result with Base64.
- Arguments: `string`
- Returns: A Base64-encoded SHA256 hash string.
- Syntax: `base64sha256(string)`

Example:
```hcl
base64sha256("hello")
// Output: "LPJNul+..."
```

## base64sha512
- Purpose: Computes the SHA512 hash of a given string and encodes the result with Base64.
- Arguments: `string`
- Returns: A Base64-encoded SHA512 hash string.
- Syntax: `base64sha512(string)`

Example:
```hcl
base64sha512("hello")
// Output: "f7bc83..."
```

## bcrypt
- Purpose: Computes a hash of the given string using the Blowfish cipher.
- Arguments: `string`
- Returns: A hashed string in Modular Crypt Format.
- Syntax: `bcrypt(string)`

Example:
```hcl
bcrypt("password")
// Output: "$2a$..."
```

## filebase64sha256
- Purpose: Computes a Base64-encoded SHA256 hash of the contents of a given file.
- Arguments: `path`
- Returns: A Base64-encoded hash string for the file contents.
- Syntax: `filebase64sha256(path)`

Example:
```hcl
filebase64sha256("./secret.txt")
// Output: "uU2h..."
```

## filebase64sha512
- Purpose: Computes a Base64-encoded SHA512 hash of the contents of a given file.
- Arguments: `path`
- Returns: A Base64-encoded hash string for the file contents.
- Syntax: `filebase64sha512(path)`

Example:
```hcl
filebase64sha512("./secret.txt")
// Output: "xX0d..."
```

## filemd5
- Purpose: Computes an MD5 hash of the contents of a given file.
- Arguments: `path`
- Returns: A hexadecimal MD5 hash string for the file contents.
- Syntax: `filemd5(path)`

Example:
```hcl
filemd5("./secret.txt")
// Output: "5eb63bbbe01eeed093cb22bb8f5acdc3"
```

## filesha1
- Purpose: Computes a SHA1 hash of the contents of a given file.
- Arguments: `path`
- Returns: A hexadecimal SHA1 hash string for the file contents.
- Syntax: `filesha1(path)`

Example:
```hcl
filesha1("./secret.txt")
// Output: "2aae6c35c94fcfb415dbe95f408b9ce91ee846ed"
```

## filesha256
- Purpose: Computes a SHA256 hash of the contents of a given file.
- Arguments: `path`
- Returns: A hexadecimal SHA256 hash string for the file contents.
- Syntax: `filesha256(path)`

Example:
```hcl
filesha256("./secret.txt")
// Output: "b94d27b9934d3e08a52e52d7da7dabfade8ef..."
```

## filesha512
- Purpose: Computes a SHA512 hash of the contents of a given file.
- Arguments: `path`
- Returns: A hexadecimal SHA512 hash string for the file contents.
- Syntax: `filesha512(path)`

Example:
```hcl
filesha512("./secret.txt")
// Output: "9b71d224bd62f3785d96d46ad3ea3d73319bf..."
```

## md5
- Purpose: Computes the MD5 hash of a given string and encodes it with hexadecimal digits.
- Arguments: `string`
- Returns: A hexadecimal MD5 hash string.
- Syntax: `md5(string)`

Example:
```hcl
md5("hello")
// Output: "5d41402abc4b2a76b9719d911017c592"
```

## rsadecrypt
- Purpose: Decrypts an RSA-encrypted ciphertext and returns the corresponding cleartext.
- Arguments: `ciphertext, private_key_pem`
- Returns: The decrypted plaintext string.
- Syntax: `rsadecrypt(ciphertext, private_key_pem)`

Example:
```hcl
rsadecrypt(file("./encrypted.txt"), file("./private.pem"))
// Output: "secret message"
```

## sha1
- Purpose: Computes the SHA1 hash of a given string and encodes it with hexadecimal digits.
- Arguments: `string`
- Returns: A hexadecimal SHA1 hash string.
- Syntax: `sha1(string)`

Example:
```hcl
sha1("hello")
// Output: "aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d"
```

## sha256
- Purpose: Computes the SHA256 hash of a given string and encodes it with hexadecimal digits.
- Arguments: `string`
- Returns: A hexadecimal SHA256 hash string.
- Syntax: `sha256(string)`

Example:
```hcl
sha256("hello")
// Output: "2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824"
```

## sha512
- Purpose: Computes the SHA512 hash of a given string and encodes it with hexadecimal digits.
- Arguments: `string`
- Returns: A hexadecimal SHA512 hash string.
- Syntax: `sha512(string)`

Example:
```hcl
sha512("hello")
// Output: "9b71d224bd62f3785d96d46ad3ea3d73319bf..."
```

## uuid
- Purpose: Generates a UUID-format string using random bytes.
- Arguments: None
- Returns: A randomly generated UUID string.
- Syntax: `uuid()`

Example:
```hcl
uuid()
// Output: "f47ac10b-58cc-4372-a567-0e02b2c3d479"
```

## uuidv5
- Purpose: Generates a name-based UUID according to RFC 4122 section 4.3.
- Arguments: `namespace, name`
- Returns: A deterministic UUID based on the namespace and name.
- Syntax: `uuidv5(namespace, name)`

Example:
```hcl
uuidv5("6ba7b810-9dad-11d1-80b4-00c04fd430c8", "example")
// Output: "3bbcee75-cecc-5b56-8031-b6641c1ed1f1"
```
