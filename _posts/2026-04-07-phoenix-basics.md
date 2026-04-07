---
layout: post
title:  "phoenix basics"
date:   2026-04-07 09:10:00 -0700
tags: [elixir]
---

- [reference](https://hexdocs.pm/phoenix/installation.html)

install the Phoenix application generator
```bash
mix archive.install hex phx_new
```


## phx_new (application that creates your phoenix)

documentation
```bash
mix help phx.new
```

create new project

```bash
mix phx.new hello_world
mix phx.new hello_world --database sqlite3

mix phx.new hello_world --database sqlite3 --no-ecto

mix phx.new hello_world --module HelloWorld

mix phx.new ~/Workspace/hello_world --no-html --no-assets
```

create phoenix html template basic

```bash
mix phx.gen.html Todos Todo todos title:string completed:boolean
mix phx.gen.html Todos Todo todos title:string description:text completed:boolean

mix ecto.migrate
```


output

```bash
* creating lib/hello_web/controllers/todo_controller.ex
* creating lib/hello_web/controllers/todo_html/edit.html.heex
* creating lib/hello_web/controllers/todo_html/index.html.heex
* creating lib/hello_web/controllers/todo_html/new.html.heex
* creating lib/hello_web/controllers/todo_html/show.html.heex
* creating lib/hello_web/controllers/todo_html/todo_form.html.heex
* creating lib/hello_web/controllers/todo_html.ex
* creating test/hello_web/controllers/todo_controller_test.exs
* creating lib/hello/todos/todo.ex
* creating priv/repo/migrations/20260403183538_create_todos.exs
* creating lib/hello/todos.ex
* injecting lib/hello/todos.ex
* creating test/hello/todos_test.exs
* injecting test/hello/todos_test.exs
* creating test/support/fixtures/todos_fixtures.ex
* injecting test/support/fixtures/todos_fixtures.ex
```


Add the resource to your browser scope in lib/hello_web/router.ex:

    resources "/todos", TodoController


Remember to update your repository by running migrations:

    $ mix ecto.migrate

## quicktour
[quicktour](https://hexdocs.pm/phoenix/up_and_running.html)

## post steps after running mix phx.new hello

We are almost there! The following steps are missing:

    $ cd hello

Then configure your database in config/dev.exs and run:

    $ mix ecto.create

Start your Phoenix app with:

    $ mix phx.server

You can also run your app inside IEx (Interactive Elixir) as:

    $ iex -S mix phx.server


## useful commands

kill process for existing port
```bash
lsof -i :4000

kill -9 PID
```
