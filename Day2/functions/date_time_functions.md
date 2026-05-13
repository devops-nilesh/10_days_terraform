# Terraform Date and Time Functions

Terraform date and time functions let you format, compare, and manipulate timestamps inside expressions.

## formatdate
- Purpose: Converts a timestamp into a different time format.
- Arguments: `layout, timestamp`
- Returns: A formatted date/time string based on the provided layout.
- Syntax: `formatdate(layout, timestamp)`

Example:
```hcl
formatdate("%Y-%m-%dT%H:%M:%SZ", timestamp())
// Output: "2026-05-14T12:34:56Z"
```

## plantimestamp
- Purpose: Returns a UTC timestamp string in RFC 3339 format representing when Terraform creates a plan.
- Arguments: None
- Returns: A timestamp string for the current plan creation time.
- Syntax: `plantimestamp()`

Example:
```hcl
plantimestamp()
// Output: "2026-05-14T12:34:56Z"
```

## timeadd
- Purpose: Adds a duration to a timestamp and returns a new timestamp.
- Arguments: `timestamp, duration`
- Returns: A timestamp string representing the result of the addition.
- Syntax: `timeadd(timestamp, duration)`

Example:
```hcl
timeadd(timestamp(), "24h")
// Output: "2026-05-15T12:34:56Z"
```

## timecmp
- Purpose: Compares two timestamps.
- Arguments: `timestamp1, timestamp2`
- Returns: A number indicating ordering: negative if the first is earlier, zero if equal, positive if later.
- Syntax: `timecmp(timestamp1, timestamp2)`

Example:
```hcl
timecmp("2026-05-14T12:00:00Z", "2026-05-14T13:00:00Z")
// Output: -1
```

## timestamp
- Purpose: Returns the current time as a UTC timestamp string in RFC 3339 format.
- Arguments: None
- Returns: The current timestamp string.
- Syntax: `timestamp()`

Example:
```hcl
timestamp()
// Output: "2026-05-14T12:34:56Z"
```
