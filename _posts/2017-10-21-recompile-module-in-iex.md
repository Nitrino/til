---
layout: post
title:  "[#1] Recompile module in iex session"
categories: elixir
---
While working in iex session, the modified modules are not updated. We can recompile the file containing specified module with the `r` command.

{% highlight elixir %}
# code.exs
defmodule Bar do
 # code
end

defmodule Foo do
  # code
end
{% endhighlight %}

{% highlight elixir %}
iex(1)> r Foo
{:reloaded, Foo, [Bar, Foo]
{% endhighlight %}

You can get more information called `h()` function in iex session.
