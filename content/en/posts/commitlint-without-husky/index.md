---
title: "Run Commitlint Locally Without Husky"
languageCode: en-US
date: 2020-09-15T11:30:03+00:00
# weight: 1
# aliases: ["/first"]
tags: ["devops", "commitlint"]
author: "mmoyle"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Run Commitlint Locally Without Husky"
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowCodeCopyButtons: true
ShowRssButtonInSectionTermList: true
ShowShareButtons: true
UseHugoToc: true
# cover:
#     image: "images/00162-1331686939.png" # image path/url
#     alt: "<alt text>" # alt text
#     caption: "<text>" # display caption under cover
#     relative: true # when using page bundles set this to true
#     hidden: false # only hide on current single page
#     linkFullImages: true
editPost:
    URL: "https://github.com/mmoyle/mmoyle.github.io/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

## Overview
Some projects use [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/). You may want to run the linter locally in a non node.js project. All of the documentation I found assumes the presence of a package.json file and the use of Husky. What if you are not working in a node.js project and don't have a package.json file? Then husky will not initialize. This guide sets up commitlint locally without husky.

## Setup (Mac OS Homebrew)

### Install packages

```bash
brew install npm
npm install --save-dev @commitlint/{cli,config-conventional}

```
### cd to your cloned git repo.

```
echo "npx --no -- commitlint --edit \$1" > .git/hooks/commit-msg
chmod 755 .git/hooks/commit-msg

# create commitlint.config.js
$ echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```

## Test It
Create a temp file and try to commit it.

```bash
$ touch foo
$ git add foo
$ git commit -m 'foo: this message will fail'

```

The output should look like this:

```
⧗   input: foo: fail
✖   type must be one of [build, chore, ci, docs, feat, fix, perf, refactor, revert, style, test] [type-enum]

✖   found 1 problems, 0 warnings
ⓘ   Get help: https://github.com/conventional-changelog/commitlint/#what-is-commitlint

❯ git commit -m 'foo: this message will fail'
⧗   input: foo: this message will fail
✖   type must be one of [build, chore, ci, docs, feat, fix, perf, refactor, revert, style, test] [type-enum]

✖   found 1 problems, 0 warnings
ⓘ   Get help: https://github.com/conventional-changelog/commitlint/#what-is-commitlint
```

## References
- [Commitlint Shareable Config](https://commitlint.js.org/concepts/shareable-config.html)
- [Commitlint Getting Started Guide](https://commitlint.js.org/guides/getting-started.html)
