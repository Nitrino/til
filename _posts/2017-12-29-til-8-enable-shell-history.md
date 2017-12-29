---
layout: post
title:  "[#8] Enable shell history in iex"
categories: elixir
---
Starting with OTP 20 appeared support for shell history. By default this option is disabled, to enable it, you need to add an environment variable in your shell.

```sh
export ERL_AFLAGS="-kernel shell_history enabled"
```
Now you can navigate the history of previous iex sessions using the up/down keys.
