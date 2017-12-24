---
layout: post
title:  "[#7] Configuring line length to Elixir 1.6 formatter"
categories: elixir
---
With Elixir 1.6 we have a built-in code formatter. When I started to use the formatter on my project I encountered that it split the code into several lines if its length is more than 90-100 characters.

In search of the string length setting parameter, I found the documentation for `Code.format_string!/2` function and `line_length` parameter, that can be used in global formatter configs.

Example `.formatter.exs` config:

```elixir
[
  inputs: ["mix.exs","{config,lib,test,web}/**/*.{ex,exs}"],
  line_length: 120
]
```

Default line length is `98` characters.

More information can be found by calling `h Code.format_string!/2` in `iex`
