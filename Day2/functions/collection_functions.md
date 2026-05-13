# Terraform Collection Functions

Terraform collection functions help you manipulate lists, maps, tuples, and sets inside expressions. Use them to combine values, inspect structure, or transform collection data before passing it to resources and outputs.

## alltrue
- Purpose: Checks whether every element in the given collection is true.
- Arguments: `collection`
- Returns: `true` if all elements are `true` or the string `"true"`; otherwise `false`. Returns `true` for an empty collection.
- Syntax: `alltrue(collection)`

Example:
```hcl
alltrue([true, "true", true])
// Output: true
```

## anytrue
- Purpose: Checks whether any element in the given collection is true.
- Arguments: `collection`
- Returns: `true` if any element is `true` or the string `"true"`; otherwise `false`. Returns `true` for an empty collection.
- Syntax: `anytrue(collection)`

Example:
```hcl
anytrue([false, "true", false])
// Output: true
```

## chunklist
- Purpose: Breaks a list into smaller fixed-size sublists.
- Arguments: `list, size`
- Returns: A list of lists, where the last chunk may be smaller if the input list length is not evenly divisible.
- Syntax: `chunklist(list, size)`

Example:
```hcl
chunklist([1, 2, 3, 4, 5], 2)
// Output: [[1, 2], [3, 4], [5]]
```

## coalesce
- Purpose: Returns the first argument that is neither `null` nor an empty string.
- Arguments: `arg1, arg2, ...`
- Returns: The first non-null, non-empty string argument.
- Syntax: `coalesce(arg1, arg2, ...)`

Example:
```hcl
coalesce(null, "", "value")
// Output: "value"
```

## coalescelist
- Purpose: Returns the first non-empty list from a sequence of lists.
- Arguments: `list1, list2, ...`
- Returns: The first list containing at least one element.
- Syntax: `coalescelist(list1, list2, ...)`

Example:
```hcl
coalescelist([], [1, 2], [3])
// Output: [1, 2]
```

## compact
- Purpose: Removes null and empty string elements from a list of strings.
- Arguments: `list`
- Returns: A new list with only non-empty, non-null string values.
- Syntax: `compact(list)`

Example:
```hcl
compact(["a", "", null, "b"])
// Output: ["a", "b"]
```

## concat
- Purpose: Joins multiple lists into one.
- Arguments: `list1, list2, ...`
- Returns: A new list containing the elements of all input lists in order.
- Syntax: `concat(list1, list2, ...)`

Example:
```hcl
concat(["a", "b"], ["c"], ["d", "e"])
// Output: ["a", "b", "c", "d", "e"]
```

## contains
- Purpose: Tests whether a collection contains a specific value.
- Arguments: `collection, value`
- Returns: `true` if the value exists in the list, tuple, or set; otherwise `false`.
- Syntax: `contains(collection, value)`

Example:
```hcl
contains(["red", "green", "blue"], "green")
// Output: true
```

## distinct
- Purpose: Removes duplicate elements from a list.
- Arguments: `list`
- Returns: A new list preserving the first occurrence of each element.
- Syntax: `distinct(list)`

Example:
```hcl
distinct(["a", "b", "a", "c", "b"])
// Output: ["a", "b", "c"]
```

## element
- Purpose: Retrieves an element from a list by index.
- Arguments: `list, index`
- Returns: The element at the specified index. Supports negative indexing by wrapping around.
- Syntax: `element(list, index)`

Example:
```hcl
element(["a", "b", "c"], 1)
// Output: "b"
```

## flatten
- Purpose: Flattens a nested list by one level.
- Arguments: `list`
- Returns: A list where any nested lists are replaced by their contents.
- Syntax: `flatten(list)`

Example:
```hcl
flatten([[1, 2], [3], [4, 5]])
// Output: [1, 2, 3, 4, 5]
```

## index
- Purpose: Finds the index of the first matching value in a list.
- Arguments: `list, value`
- Returns: The index position of the matching element.
- Syntax: `index(list, value)`

Example:
```hcl
index(["red", "green", "blue"], "green")
// Output: 1
```

## keys
- Purpose: Extracts the keys from a map.
- Arguments: `map`
- Returns: A list of keys in unspecified order.
- Syntax: `keys(map)`

Example:
```hcl
keys({name = "app", env = "prod"})
// Output: ["env", "name"]
```

## length
- Purpose: Returns the number of elements in a collection or the number of characters in a string.
- Arguments: `collection`
- Returns: An integer count for lists, maps, sets, tuples, or strings.
- Syntax: `length(collection)`

Example:
```hcl
length([1, 2, 3])
// Output: 3
```

## list
- Purpose: Deprecated list constructor.
- Arguments: `value1, value2, ...`
- Returns: A list composed of the provided values. Use `tolist` in modern configurations.
- Syntax: `list(value1, value2, ...)`

Example:
```hcl
# Deprecated usage
list(1, 2, 3)
```

## lookup
- Purpose: Gets a value from a map by key.
- Arguments: `map, key, default`
- Returns: The value for `key`, or `default` if the key does not exist.
- Syntax: `lookup(map, key, default)`

Example:
```hcl
lookup({env = "prod"}, "env", "dev")
// Output: "prod"
```

## map
- Purpose: Deprecated map constructor.
- Arguments: `key1, value1, key2, value2, ...`
- Returns: A map constructed from the provided key/value pairs. Use `tomap` in modern configurations.
- Syntax: `map(key1, value1, key2, value2, ...)`

Example:
```hcl
# Deprecated usage
map("name", "app", "env", "prod")
```

## matchkeys
- Purpose: Builds a list of elements from one list selected by a second list of booleans.
- Arguments: `list, keys`
- Returns: A new list containing elements from `list` where the corresponding `keys` entry is true.
- Syntax: `matchkeys(list, keys)`

Example:
```hcl
matchkeys(["a", "b", "c"], [false, true, true])
// Output: ["b", "c"]
```

## merge
- Purpose: Combines multiple maps or objects into one.
- Arguments: `map1, map2, ...`
- Returns: A merged map or object. Later arguments override earlier keys.
- Syntax: `merge(map1, map2, ...)`

Example:
```hcl
merge({a = 1}, {b = 2}, {c = 3})
// Output: {a = 1, b = 2, c = 3}
```

## one
- Purpose: Extracts the single element from a collection.
- Arguments: `collection`
- Returns: The only element if the collection contains exactly one item, `null` if empty, or raises an error if there are multiple items.
- Syntax: `one(collection)`

Example:
```hcl
one([42])
// Output: 42
```

## range
- Purpose: Creates a sequence of numbers.
- Arguments: `start, stop, step`
- Returns: A list of numbers from `start` up to but not including `stop`, incremented by `step`.
- Syntax: `range(start, stop, step)`

Example:
```hcl
range(1, 5, 2)
// Output: [1, 3]
```

## reverse
- Purpose: Reverses the order of elements in a sequence.
- Arguments: `sequence`
- Returns: A new sequence with elements in reverse order.
- Syntax: `reverse(sequence)`

Example:
```hcl
reverse(["a", "b", "c"])
// Output: ["c", "b", "a"]
```

## setintersection
- Purpose: Computes the common elements across multiple sets.
- Arguments: `set1, set2, ...`
- Returns: A set containing elements present in every input set.
- Syntax: `setintersection(set1, set2, ...)`

Example:
```hcl
setintersection([1, 2, 3], [2, 3, 4])
// Output: [2, 3]
```

## setproduct
- Purpose: Computes the Cartesian product of multiple sets.
- Arguments: `set1, set2, ...`
- Returns: A set of tuples where each combination includes one element from each input set.
- Syntax: `setproduct(set1, set2, ...)`

Example:
```hcl
setproduct(["a", "b"], [1, 2])
// Output: [["a", 1], ["a", 2], ["b", 1], ["b", 2]]
```

## setsubtract
- Purpose: Removes elements found in the second set from the first.
- Arguments: `set1, set2`
- Returns: A set containing elements that exist in `set1` but not in `set2`.
- Syntax: `setsubtract(set1, set2)`

Example:
```hcl
setsubtract([1, 2, 3], [2])
// Output: [1, 3]
```

## setunion
- Purpose: Combines elements from multiple sets.
- Arguments: `set1, set2, ...`
- Returns: A set containing all unique elements from the input sets.
- Syntax: `setunion(set1, set2, ...)`

Example:
```hcl
setunion([1, 2], [2, 3])
// Output: [1, 2, 3]
```

## slice
- Purpose: Extracts consecutive elements from a list.
- Arguments: `list, start, end`
- Returns: A sublist from `start` up to but not including `end`.
- Syntax: `slice(list, start, end)`

Example:
```hcl
slice(["a", "b", "c", "d"], 1, 3)
// Output: ["b", "c"]
```

## sort
- Purpose: Sorts a list of strings in lexicographic order.
- Arguments: `list`
- Returns: A new list containing the sorted string values.
- Syntax: `sort(list)`

Example:
```hcl
sort(["z", "a", "m"])
// Output: ["a", "m", "z"]
```

## sum
- Purpose: Adds all numeric values in a list or set.
- Arguments: `collection`
- Returns: The numeric total of all values in the collection.
- Syntax: `sum(collection)`

Example:
```hcl
sum([1, 2, 3])
// Output: 6
```

## transpose
- Purpose: Swaps rows and columns in a map of lists of strings.
- Arguments: `map`
- Returns: A new map where list elements become keys and original keys become list values.
- Syntax: `transpose(map)`

Example:
```hcl
transpose({
  a = ["1", "2"],
  b = ["3", "4"]
})
// Output: {"1" = ["a"], "2" = ["a"], "3" = ["b"], "4" = ["b"]}
```

## values
- Purpose: Extracts the values from a map.
- Arguments: `map`
- Returns: A list of values in unspecified order.
- Syntax: `values(map)`

Example:
```hcl
values({name = "app", env = "prod"})
// Output: ["prod", "app"]
```

## zipmap
- Purpose: Constructs a map by pairing keys and values from two lists.
- Arguments: `keys, values`
- Returns: A map whose keys come from the first list and values from the second list.
- Syntax: `zipmap(keys, values)`

Example:
```hcl
zipmap(["name", "env"], ["app", "prod"])
// Output: {name = "app", env = "prod"}
```
