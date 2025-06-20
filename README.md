# participle lexer/parser for playwright Actions DSL

> NOTE: This is just an experiment for an idea I got while working on a PR for [ovh/venom](https://github.com/ovh/venom/pull/843), YMMV

Playwright Actions (PACT) is a small DSL (domain specific language) for interacting with [playwright](https://playwright.dev).

It allows users to perform actions via Playwright without having to use 
actual programmatic SDKs or syntax - opening Playwright up to less technical
users and faster authoring of end to end UI tests.

This repository implements a basic Lexer and Parser for PACT using [participle](https://github.com/alecthomas/participle)

It looks like this, each action is specified on its own line:

```
Fill "x" "something something here" 
Fill "#x" "something something here"
Fill ".x" "something something here"
Fill "[name=email]" "something something here"
Fill "some element with whitespace" "something something here"
Fill ".input[type=\"text\"]" "something something here"
Click "existent" "something"
Click "GetByRole( \"existent\" )"
```

To play with this repo you can:

```sh 
$ git clone https://github.com/zikani03/pact

$ cd pact

$ cat actions.pact | go run ./cmd/main.go
```