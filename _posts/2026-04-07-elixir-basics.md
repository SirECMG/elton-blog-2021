---
layout: post
title:  "elixir basics"
date:   2026-04-09 07:29:00 -0700
tags: [elixir]
---

open file in elixir
```elixir
file_name = "input.txt"
case File.read(file_name) do
  {:ok, content} ->
    IO.puts(content)
  {:error, reason} ->
    IO.puts("open failed: #{reason}")
end
```

## tuples

[tuple docs](https://hexdocs.pm/elixir/1.12.3/Tuple.html)

- tuples are intended as fixed-size containers for multiple elements
- tuple usage
   - do
		- typically used either when a function has multiple return values for error handling
	- do not
		- to manipulate a collection of elements, use a list instead
	- notes
		- Enum functions don't work on tuples
		- may contain different types
		- stored contiguously(in a row) in memory
		- access any element takes constant time
		- modifying produces a shallow copy, takes O(n)
		- good for reading data (list better for traveral)
		- functions that add and remove elements from tuples are rarely used in practice, as they imply tuples are
		- to append to a tuple, it is preferable to extract the elements from the old tuple with pattern matching and being used as collections.
	
create a new tuple 
```elixir
{} # basic tuple

{1, :two, "three"}

tuple = {:ok, :example}

# avoid
result = Tuple.insert_at(tuple, 2, %{})
# prefer
{:ok, atom} = tuple # uses deconstruct syntax to create a new tuple
result = {:ok, atom, %{}}
```

## lists

[list docs](https://hexdocs.pm/elixir/1.12.3/List.html)
	- linked lists hold zero, one, or moe elements in the chosen order

```elixir
[1, "two", 3, :four]

[1, 2, 3] ++ [4, 5, 6]

[new | list]

[head | tail] = [1, 2, 3]

[1 | [2 | [3 | []]]]

```


- con cells
	- [head | tail]
	- prepending is always faster
	- appending is slower
	- most functions work in linear time
	- Enum module works on List
 
## charlists
- list made of non-negative integer, where each integer represents a Unicode code point, the list can be also calle a charlist.
	- 0..0x10FFFF
	- be out of range 0xD800..0xDFFF
	- elixir uses single quotes to define charlists

## maps

- are the "go to" key-value data structure in elixir
	- ```%{}```
	- key-value pair ```key => value```
	- kv pairs in a map do not follow any order
	- maps do not impose any restriction on the key type: anything ca be a key in a map
	- as a key-value structure, maps don't allow duplicate keys
	- when the key in a kv pair is an atom the key: value short hard syntax can be used ```%{a: 1, b: 2}```

```elixir
%{}

%{"one" => :two, 3 => "four"}

%{one: 1, two: 2}

%{:one => 1, :two => 2}
```


### map access Module
```elixir
map = %{a: 1, b: 2}
Map.fetch(map, :a)
map[:b]

map.foo
map.non_existing_key
```

- do not add parens when accessing fields, such as in data.key(). If parenthesis are used, Elixir will expect data to be an atom representing a module and attempt to call the function key/0 in it.
- the two syntaxes for accessing keys reveal the dual nature of maps.
	- map[key] is used for dynamically created maps that may have any key of any type.
	- map.key is used with maps that hold a predetermined set of atom keys, which are expected to always be present.
	- Structs, defined via defstruct, are one example of such "static maps" where keys can also be checked during compile time
	- maps can be pattern matched on.
 
```elixir
%{} = %{foo: "bar"}
%{a: a} = %{:a => 1, "b" => 2, [:c, :e, :e] => 3}
a
1

# Match Error
%{:c => 3} = %{:a => 1, 2 => :b}

```

- Variables can be used as map keys both when writing map literals as well as when matching:

- Maps also support a specific update syntax to update the value stored under existing atom keys:

```elixir
map = %{one: 1, two: 2}
%{map | one: "one"}
%{one: "one", two: 2}
```

When a key that does not exist in the map is updated a KeyError exception will be raised:
```elixir
%{map | three: 3}
```

- The functions in this module that need to find a specific key work in logarithmic time.
- This means that the time it takes to find keys grows as the map grows, but it's not directly proportional to the map size.
- In comparison to finding an element in a list, it performs better because lists have a linear time complexity.
- Some functions, such as keys/1 and values/1, run in linear time because they need to get to every element in the map.
- Maps also implement the Enumerable protocol, so many functions to work with maps are found in the Enum module. Additionally, the following functions for maps are found in Kernel:

## records

Module to work with, define, and import records.

Records are simply tuples where the first element is an atom:

```elixir
Record.is_record({User, "john", 27})
true
```

This module provides conveniences for working with records at compilation time, where compile-time field names are used to manipulate the tuples, providing fast operations on top of the tuples' compact structure.

In Elixir, records are used mostly in two situations:

    to work with short, internal data
    to interface with Erlang records

The macros defrecord/3 and defrecordp/3 can be used to create records while extract/2 and extract_all/1 can be used to extract records from Erlang files.


### Types

Types can be defined for tuples with the record/2 macro (only available in typespecs). This macro will expand to a tuple as seen in the example below:

```elixir
defmodule MyModule do
  require Record
  Record.defrecord(:user, name: "john", age: 25)

  @type user :: record(:user, name: String.t(), age: integer)
  # expands to: "@type user :: {:user, String.t(), integer}"
end
```

## struct

[struct doc](https://hexdocs.pm/elixir/1.12.3/Kernel.html#defstruct/1)
[struct doc#2](https://hexdocs.pm/elixir/1.12.3/Kernel.SpecialForms.html#%25/2)
Defines a struct.

A struct is a tagged map that allows developers to provide default values for keys, tags to be used in polymorphic dispatches and compile time assertions.

To define a struct, a developer must define both __struct__/0 and __struct__/1 functions. defstruct/1 is a convenience macro which defines such functions with some conveniences.

For more information about structs, please check Kernel.SpecialForms.%/2.
```elixir
defmodule User do
	defstruct [:name, :age]
end

or

defmodule User do
	defstruct :name, :age
end

defmodule User do
	defstruct name: nil, age: nil
end
```
