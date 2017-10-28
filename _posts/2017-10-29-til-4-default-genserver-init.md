---
layout: post
title:  "[#4] Default GenServer init"
categories: elixir
---
When we using `use GenServer` we get the predefined function `init/1`
{% highlight elixir %}
def init(args) do
  {:ok, args}
end
{% endhighlight %}

This implies:
1. When you see `GenServer` that doesn’t have `init/1` defined in the code - it will look like described above.
2. If your `init/1` does the same as predefined `init/1` - don’t override it manually in the code.
