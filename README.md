# obb

[![project chat](https://img.shields.io/badge/slack-join_chat-brightgreen.svg)](https://app.slack.com/client/T03RZGPFR/C02S1220XRV)
![Stability: Experimental](https://img.shields.io/badge/stability-experimental-orange.svg)

Ad-hoc [ClojureScript](https://clojurescript.org/) scripting of Mac applications via Apple's [Open Scripting Architecture](https://developer.apple.com/library/archive/documentation/LanguagesUtilities/Conceptual/MacAutomationScriptingGuide/).

## Status

Experimental.

## Installation

### Homebrew

``` shell
$ brew install babashka/brew/obb
```

### Manual

Download from [Github releases](https://github.com/babashka/obb/releases).

## Usage

Evaluate an expression:

``` shell
$ obb -e '(-> (js/Application "Safari") (.-documents) (aget 0) (.url))'
https://clojure.org/
```

``` shell
$ obb -e '(-> (js/Application "Google Chrome") (.-windows) (aget 0) (.activeTab) (.title))'
Slack | obb | clojurians
```

Or evaluate a file:

``` shell
$ obb examples/choice.cljs
```

Or make an executable script by using `obb` in a [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)):

``` shell
$ cat quit.cljs
#!/usr/bin/env obb
(-> (js/Application "Safari")
    (.quit))
$ chmod u+x quit.cljs
$ ./quit.cljs
true
```

## How does this tool work?

ClojureScript code is evaluated through [SCI](https://github.com/borkdude/sci), the same interpreter that powers [babashka](https://babashka.org/). SCI is compiled to JavaScript which is then by executed by `osascript`.

## References

- [Mac Automation Scripting Guide](https://developer.apple.com/library/archive/documentation/LanguagesUtilities/Conceptual/MacAutomationScriptingGuide/GettoKnowScriptEditor.html#//apple_ref/doc/uid/TP40016239-CH5-SW1)
- [JXA Cookbook](https://github.com/JXA-Cookbook/JXA-Cookbook/wiki)

## Build

[Install Babashka](https://github.com/babashka/babashka/#installation). Then build with:

``` shell
$ bb build
```

Then place `out/obb` anywhere on your path.
