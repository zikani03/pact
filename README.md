# pact

`pact` allow users and developers to author and run Playwright actions using a simple
configuration file with less code. 

`pact` supports writing playwright actions as either `.yaml` or `.pact` files. The goal
is for the .pact file DSL to be simple enough to hand over to non-technical users.

> NOTE: `pact` is still in very early development. There are no guarantees about API or feature stability.

## Building 

```sh
$ git clone https://github.com/zikani03/pact

$ cd pact

$ go build -o pact ./cmd/main.go

$ ./pact --help

# Test with the example file in the repo

$ ./pact run --file example-hn.pact --url "https://news.ycombinator.com"
```

## Example usage

> NOTE: the `pact` depends on Playwright and as a result, will
> attempt to install playwright if it is not already installed.
> you will notice this the first time you run the test/files

Create a file named `basic.yaml`

```yaml
name: Try to login to HackerNews
description: Test login to hacker news
url: htts://news.ycombinator.com
headless: true
actions:
  - { action: Goto,       content: "/login" }
  - { action: Fill,       selector: "input[name=acct]", content: "throwaway-user" }
  - { action: Fill,       selector: "input[name=pw]", content:  "fakepassword" }
  - { action: Click,      selector: "input[value=login]" }
  - { action: Screenshot, selector: "body", content: "./test-screenshot.png" }
```

The equivalent `basic.pact` file can be authored like this

```
Goto "/login"
Fill "input[name=acct]" "throwaway-username" 
Fill "input[name=pw]" "fakepassword"
Click "input[value=login]"
Screenshot "body" "./test-screenshot.png"
```

You can now run the file using pact, like so:

```sh 
$ ./pact run --file basic.yaml
```

Or 

```sh 
$ ./pact run --file basic.pact --url "https://news.ycombinator.com"
```

## Available actions

|Action|Arguments|Example|
|------|---------|-------|
|Click                 |**querySelector**| Click "#element" |
|DoubleClick           |**querySelector**| DoubleClick "#element" |
|Tap                   |**querySelector**| Tap "#element" |
|Focus                 |**querySelector**| Focus "#element" |
|Blur                  |**querySelector**| Blur "#element" |
|Fill                  |**querySelector** TEXT| Fill "#element" "my input text" |
|Clear                 |**querySelector**| Clear "#element" |
|Check                 |**querySelector**| Check "#element" |
|Uncheck               |**querySelector**| Uncheck "#element" |
|FillCheckbox          |**querySelector**| FillCheckbox "#element" |
|Press                 |**querySelector** TEXT| Press "#element" "some text"|
|PressSequentially     |**querySelector** TEXT | PressSequentially "#element" "some input"|
|Type                  |**querySelector** TEXT | Type "#element" |
|Screenshot            |**querySelector** TEXT | Screenshot "#selector" "filename.png"|
|Select                |**querySelector** TEXT | Select "#someSelect" "Value or Label"|
|SelectOption          |**querySelector** TEXT | Select "#someSelect" "Value or Label"|
|SelectMultipleOptions |**querySelector** TEXT | SelectMultipleOptions "#someSelect" "Value or Label 1,Value or Label 2,..., Value or Label N"|
|WaitFor               |**querySelector**| WaitFor "#element" |
|WaitForSelector       |**querySelector**| WaitForSelector "#element" |
|Goto                  |**REGEX**| Goto "^some-page" |
|WaitForURL            |**REGEX**| WaitForURL "^some-page" |
|GoBack                |N/A| GoBack |
|GoForward             |N/A| GoForward |
|Refresh               |N/A| Refresh |

## LICENSE

Apache 2.0 LICENSE