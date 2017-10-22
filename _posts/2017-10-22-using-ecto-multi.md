---
layout: post
title:  "[#2] Using Ecto Multi"
categories: elixir
---
`Ecto.Multi` — a set of utilities for grouping multiple Repo operations and perform in a single database transaction.
Each operation is given a name that is unique and will identify its result in case of success or failure.

{% highlight elixir %}
defmodule PasswordManager do
  alias Ecto.Multi

  def reset(account, params) do
    Multi.new
    |> Multi.update(:account, Account.password_reset_changeset(account, params))
    |> Multi.insert(:log, Log.password_reset_changeset(account, params))
    |> Multi.delete_all(:sessions, Ecto.assoc(account, :sessions))
  end
end
{% endhighlight %}

`Multi.run` - allows you to run arbitrary functions as part of your transaction.
This is very useful when you need to use data from a previous operation.

{% highlight elixir %}
defmodule PostsManager do
  alias Ecto.Multi

  # We insert the list of posts in the database and return only published posts
  def import(posts) do
    Multi.new()
    |> Multi.insert_all(:posts, Post, posts)
    |> Multi.run(:pablished_users, fn %{posts: posts} ->
      result = Enum.filter(posts, &(&1.is_published))
      {:ok, result}
    end)
  end
end
{% endhighlight %}

More information you can get from the [official documentation](https://hexdocs.pm/ecto/Ecto.Multi.html){:target="_blank"}
