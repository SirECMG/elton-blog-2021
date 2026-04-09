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

