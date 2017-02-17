# Elixir

## Why?

This is a Markdown file to use like reminder of elixir details, because I learn things very fast and forget also.
Then this will help me to remember elixir caracteristics.

### Sigils

  Used to work with literals.
  Example:

  ~W Generate a list of words
```elixir
    ~W/Daniel is very hot/
```
Result will be: ["Daniel","is","Very","Hot"]

### Functions
#### The &
Used to create anon functions

  Example:

  ```elixir

   sum = &(&1 + &2)

  ```

  Result: sum.(2, 3)
  5

#### Creating a pattern matching function
Example:
```elixir
  handle_result = fn
    {:ok, result} -> IO.puts "Yes, the result is correct"
    {:error} -> IO.puts "Oh no, error!"
  end
```

#### Creating anon functions
Divided argument of body with ->

Example:
```elixir
sum = fn (a,b) -> a + b end
sum.(1,2) ```

Result: 3

#### Creating function in an line
Use "do:"
Example:
  ```elixir
  def hello(name) do: "Hello, " <> name
  ```

#### Creating recursive function
```elixir
defmodule Length do
  def of([]), do: 0
  def of([_|t]), do: 1 + of[t]
end
```

This is a recursive function that will get the first element of the list, add more one to list in each "of function" called.

#### Default value to Arguments
Used \\ to pass default value to an argument

```elixir
defmodule Greeter do
  def hello(name, country \\ "en") do
    phrase(country) <> name
  end
  def phrase("en"), do: "Hellou, "
  def phrase("br"), do: "Uuuuuuuuuuuh, seu demonho!!! "
end
```
**PS**: Do not use default arguments with Guards, to do this, create a method with default value and other with Guards.

#### Guards

Used to create the same method with different behaviors according to the type of arguments

Example:
```elixir
  defmodule Greeter do
    def hello(names) when is_list(names) do
      names
      |> Enum.join(", ")
      |> hello
    end
    def hello(name) when is_binary(name) do
      phrase <> name
    end
    def phrase, do: "Hello, "
  end
```

### Data Structures
#### Maps
  %{} - Maps representation. Remember: Maps are different to lists of keywords because maps accept keys of any types.

#### Atoms
  :name - Atoms are constants with the name equal to value.

#### structs
  structs are like maps but is special type.

#### The ?
  Elixir use UTF-8 string. And to discover the code of a char in string you can use the operator ?.

  Example:
  ```elixir
  ?C
  ```
  Result: 67

  Could you use the function codepoints of String module to split the characters of string

  Example:
  ```elixir
  String.codepoints("daniel")
  ```
  Result: ["d", "a", "n", "i", "e", "l"]

#### Especial Conventions

  **!** - Use for functions which raise exceptions on failure
  **?** - Use for functions which return a boolean value
  **_** - Use to ignore arguments of a function or part of pattern matching expression
  **.** - Used for calling anonymous function
  
