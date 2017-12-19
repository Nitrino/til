---
layout: post
title:  "[#6] Don't use keyword arguments in functions"
categories: elixir
---
Since Ruby 2.0 you can use keyword arguments in functions.
It looks something like this:

```ruby
def create_user(first_name:, last_name:)
  p first_name, last_name
end

irb > create_user(first_name: "Petr", last_name: "Stepchenko")
"Petr"
"Stepchenko"
```

In the Elixir for similar behavior often used a keyword list with pattern matching in function header.

Example:

```elixir
defmodule User do
  def create(first_name: first_name, last_name: last_name) do
    IO.inspect first_name
    IO.inspect last_name
  end
end

iex(1)> User.create(first_name: "Petr", last_name: "Stepchenko")
"Petr"
"Stepchenko"
```

But this will not be a function with two arguments, it is a function with one keyword list argument.

```elixir
iex(11)> User.create
create/1
```

So this code has a critical drawback associated with the rules of the pattern matching keyword lists. To match a keyword lists, you need two conditions:
1. Keys and values match
2. **The order of the keys must match**

The second condition causes a lot of inconvenience and it is necessary always to pay attention to it.

Example:

```elixir

iex(1)> User.create(first_name: "Petr", last_name: "Stepchenko")
"Petr"
"Stepchenko"

iex(2)> User.create(last_name: "Stepchenko", first_name: "Petr")
** (FunctionClauseError) no function clause matching in User.create/1

    The following arguments were given to User.create/1:

        # 1
        [last_name: "Stepchenko", first_name: "Petr"]

    iex:10: User.create/1
```

## Conclusion

Don't use keyword arguments for this behavior, especially if you are writing libraries.

For similar behavior, you can use maps with pattern matching.
```elixir
defmodule User do
  def create(%{first_name: first_name, last_name: last_name}) do
    IO.inspect first_name
    IO.inspect last_name
  end
end

iex(3)> User.create(%{first_name: "Petr", last_name: "Stepchenko"})
"Petr"
"Stepchenko"

iex(4)> User.create(%{last_name: "Stepchenko", first_name: "Petr"})
"Petr"
"Stepchenko"
```
