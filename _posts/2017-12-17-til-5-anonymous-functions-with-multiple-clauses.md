---
layout: post
title:  "[#5] Anonymous functions with multiple clauses"
categories: elixir
---
In our Elixir programs, we can use the pattern matching to define multiple clauses in an anonymous function.

Example:

```elixir
anonymous_function = fn
  {:ok, x} -> "Success case: #{x}"
  {:error, x} -> "Fail case: #{x}"
end
```

Then we call our anonymous function

```elixir
iex(2)> anonymous_function.({:ok, :data})
"Success case: data"

iex(3)> anonymous_function.({:error, :error})
"Fail case: error"
```
