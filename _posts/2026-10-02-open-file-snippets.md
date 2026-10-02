---
layout: post
title:  "Open file snippets"
date:   2026-10-02 03:24:00 -0700
tags: [ productivity ]
---

# Open file snippets

## C character by character

```c

#include "stdio.h"
#include "stdlib.h"

#define FILENAME "input.txt"

int main() {
  FILE *fp = fopen(FILENAME, "r");

  if(fp == NULL) {
    printf("something went wrong with reading the file\n");
    return EXIT_FAILURE;
  }

  char ch;
  while((ch = fgetc(fp) != EOF)) {
    
  }
  return EXIT_SUCCESS;
}
```

## Erlang

```erlang
-module(example).
-export([main/0]).

process_char(Cur) ->
  io:format("do something with ~c", [Cur]).

main() ->
  case file:read_file("input.txt") of
    {ok, BinaryData} -> 
        Ch = binary_to_list(BinaryData),
        process_char(Ch);
    {error, _} ->
        io:format("something went wrong with the file")
  end.
```

```text
erlc example.erl                                     
erl -noshell -s example main -s init stop < input.txt
```

## improvements to reading files. we will need to leverage <  (reading from stdin)

```

```text
./main < input.txt
```


```erlang
-module(example).

-export([main/0]).

main() ->
    case io:get_chars("", 1) of
        eof -> 
            ok;
        Char -> 
            io:format("~p~n", [Char]),
            main()
    end.
```

```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int ch;

    while ((ch = getchar()) != EOF) {
        printf("%c\n", ch);
    }

    return EXIT_SUCCESS;
}
```
