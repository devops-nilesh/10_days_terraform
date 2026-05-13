# Terraform IP Network Functions

Terraform IP network functions let you work with CIDR blocks and calculate IP addresses and subnets.

## cidrhost
- Purpose: Calculates a full host IP address for a given host number within a CIDR range.
- Arguments: `network, hostnum`
- Returns: The IP address for the specified host number.
- Syntax: `cidrhost(network, hostnum)`

Example:
```hcl
cidrhost("10.0.0.0/24", 5)
// Output: "10.0.0.5"
```

## cidrnetmask
- Purpose: Converts an IPv4 address prefix in CIDR notation into a subnet mask.
- Arguments: `prefix`
- Returns: The subnet mask corresponding to the CIDR prefix.
- Syntax: `cidrnetmask(prefix)`

Example:
```hcl
cidrnetmask("10.0.0.0/24")
// Output: "255.255.255.0"
```

## cidrsubnet
- Purpose: Calculates a subnet address within a given IP network prefix.
- Arguments: `network, newbits, netnum`
- Returns: The CIDR subnet address for the requested block.
- Syntax: `cidrsubnet(network, newbits, netnum)`

Example:
```hcl
cidrsubnet("10.0.0.0/16", 8, 1)
// Output: "10.1.0.0/24"
```

## cidrsubnets
- Purpose: Calculates a sequence of consecutive IP address ranges within a CIDR prefix.
- Arguments: `network, newbits, count`
- Returns: A list of CIDR subnets.
- Syntax: `cidrsubnets(network, newbits, count)`

Example:
```hcl
cidrsubnets("10.0.0.0/16", 8, 3)
// Output: ["10.0.0.0/24", "10.1.0.0/24", "10.2.0.0/24"]
```
