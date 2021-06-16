---
title: ':emojisense:, Emoji snippet VSCODE'
categories: text-editor emoji, emoji snippet, emojisence 
permalink: emojisence.html
tags: [notes]
---

VScode এ emoji type করতে চাইলে,

প্রথমে extention panel থেকে <font color="blue"> :emojisence: </font> install করে নিতে হবে।

এর পর settings.json এ emojisense.languages portion এ , যে সব language এ emoji ব্যবহার করার প্রয়োজন সে সব language এর নাম দিয়ে দিতে হবে ।

আমি একটি demo দিয়ে দিতেছি, চাইলে এই DEMO use করতে পারেন ।

```
    "emojisense.languages": {
        "plaintext": {
            "markupCompletionsEnabled": true,
            "emojiDecoratorsEnabled": true
        },
        "javascript.validate.enable": false,
        "abap": true,
        "bat": true,
        "bibtex": true,
        "clojure": true,
        "coffeescript": true,
        "c": true,
        "cpp": true,
        "csharp": true,
        "css": true,
        "diff": true,
        "dockerfile": true,
        "fsharp": true,
        "git-commit": true,
        "git-rebase": true,
        "go": true,
        "groovy": true,
        "handlebars": true,
        "html": true,
        "ini": true,
        "java": true,
        "javascript": true,
        "javascriptreact": true,
        "json": true,
        "jsonc": true,
        "latex": true,
        "less": true,
        "lua": true,
        "makefile": true,
        "markdown": true,
        "objective-c": true,
        "objective-cpp": true,
        "perl6": true,
        "php": true,
        "powershell": true,
        "jade": true,
        "python": true,
        "r": true,
        "razor": true,
        "ruby": true,
        "rust": true,
        "scss": true,
        "sass": true,
        "shaderlab": true,
        "shellscript": true,
        "sql": true,
        "swift": true,
        "typescript": true,
        "typescriptreact": true,
        "tex": true,
        "vb": true,
        "xml": true,
        "xsl": true,
        "yaml": true
    }

```
