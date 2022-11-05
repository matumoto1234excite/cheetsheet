# VSCode の設定

```json
{
    /* code-runner begin here */
    // {{{
    "code-runner.clearPreviousOutput": true,
    "code-runner.runInTerminal": true,
    "code-runner.executorMap": {
        "vue": "cd $dir && clear && npm run dev",
        "elm": "cd $dir && clear && elm reactor",
        "javascript": "node",
        "java": "cd $dir && clear && javac $fileName && java $fileNameWithoutExt",
        "c": "cd $dir && clear && gcc $fileName -lm -o a.out && ./a.out",
        "cpp": "cd $dir && g++-11 $fileName -O2 -Wall -Wextra -fsplit-stack -fstack-protector-all -ftrapv -fsanitize=undefined -D_GLIBCXX_DEBUG -Wfloat-equal -std=c++20 -I/home/matumoto/code_box/library/ -I/home/matumoto/src/iutest-master/include/ -o a.out && ./a.out",
        "objective-c": "cd $dir && gcc -framework Cocoa $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
        "php": "php",
        "python": "cd $dir && python3 -u $fileName",
        "perl": "perl",
        "perl6": "perl6",
        "ruby": "ruby",
        "go": "go run",
        "lua": "lua",
        "groovy": "groovy",
        "powershell": "powershell -ExecutionPolicy ByPass -File",
        "bat": "cmd /c",
        "shellscript": "bash",
        "fsharp": "fsi",
        "csharp": "cd $dir && dotnet run",
        "vbscript": "cscript //Nologo",
        "typescript": "cd $dir; tsc $fileName; node $fileNameWithoutExt.js",
        "coffeescript": "coffee",
        "scala": "scala",
        "swift": "swift",
        "julia": "julia",
        "crystal": "crystal",
        "ocaml": "ocaml",
        "r": "Rscript",
        "applescript": "osascript",
        "clojure": "lein exec",
        "haxe": "haxe --cwd $dirWithoutTrailingSlash --run $fileNameWithoutExt",
        "html": "cd $dir && open $fileName",
        "rust": "cd $dir && rustc $fileName && $dir$fileNameWithoutExt",
        "racket": "racket",
        "scheme": "csi -script",
        "ahk": "autohotkey",
        "autoit": "autoit3",
        "dart": "dart",
        "pascal": "cd $dir && fpc $fileName && $dir$fileNameWithoutExt",
        "d": "cd $dir && dmd $fileName && $dir$fileNameWithoutExt",
        "haskell": "runhaskell",
        "nim": "nim compile --verbosity:0 --hints:off --run",
        "lisp": "sbcl --script",
        "kit": "kitc --run",
        "v": "v run",
        "sass": "sass --style expanded",
        "scss": "scss --style expanded"
    },
    // }}}
    /* code-runner end here */
    //
    //
    /* editor begin here */
    // {{{
    "editor.formatOnSave": true,
    "editor.formatOnPaste": true,
    "editor.tabSize": 2,
    "editor.guides.bracketPairs": true,
    // 行の折り返し
    "editor.wordWrap": "off",
    // カーソル系
    "editor.lineNumbers": "on",
    "editor.cursorStyle": "line",
    "editor.cursorBlinking": "solid",
    "editor.cursorSurroundingLines": 2,
    "editor.cursorSmoothCaretAnimation": true,
    "editor.cursorSurroundingLinesStyle": "default",
    // 検索系
    "editor.wordSeparators": "/\\()\"':,.;<>~!@#$%^&*|+=[]{}`?-",
    "editor.suggestSelection": "first",
    "editor.suggest.showWords": false,
    "editor.suggest.showKeywords": false,
    "editor.acceptSuggestionOnEnter": "off",
    "editor.acceptSuggestionOnCommitCharacter": false,
    // インデント系
    "editor.detectIndentation": true,
    "editor.insertSpaces": true,
    // フォント系
    "editor.fontFamily": "JetBrains Mono",
    "editor.fontLigatures": true,
    // 入力に応じて系
    "editor.formatOnType": false,
    // }}}
    /* editor end here */
    //
    //
    /* vim begin here */
    // searchMatchColor
    "vim.searchMatchColor": "#c6c6b0",
    "vim.timeout": 1000,
    "vim.useCtrlKeys": true,
    "vim.vimrc.enable": false,
    // "vim.vimrc.path": "\\\\wsl$\\Ubuntu\\home\\matumoto",
    "vim.leader": "<space>",
    "vim.insertModeKeyBindings": [
        {
            "before": [
                "j",
                "j"
            ],
            "after": [
                "<Esc>"
            ]
        },
        {
            "before": [
                "J",
                "J"
            ],
            "after": [
                "<Esc>"
            ]
        }
    ],
    "vim.normalModeKeyBindings": [
        {
            "before": [
                "Y"
            ],
            "after": [
                "v",
                "$",
                "h",
                "y"
            ]
        },
        {
            "before": [
                "leader",
                "x"
            ],
            "after": [],
            "commands": [
                {
                    "command": ":tabclose",
                    "args": []
                }
            ]
        },
        {
            "before": [
                "leader",
                "j"
            ],
            "after": [],
            "commands": [
                {
                    "command": ":tabprevious",
                    "args": []
                }
            ]
        },
        {
            "before": [
                "leader",
                "k"
            ],
            "after": [],
            "commands": [
                {
                    "command": ":tabnext",
                    "args": []
                }
            ]
        },
        {
            "before": [
                "f"
            ],
            "after": [
                "leader",
                "leader"
            ],
            "commands": []
        }
    ],
    "vim.hlsearch": true,
    "vim.useSystemClipboard": true,
    "vim.foldfix": true, // おりたたみしている所に vim 通過しても展開されなくする
    "vim.easymotion": true,
    /* vim end here */
    //
    //
    "[python]": {
        "editor.semanticHighlighting.enabled": true
    },
    "[yaml]": {
        "editor.insertSpaces": true,
        "editor.tabSize": 2,
        "editor.autoIndent": "advanced"
    },
    "files.autoSave": "afterDelay",
    "files.autoSaveDelay": 1000,
    "go.toolsManagement.autoUpdate": true,
    "git.autofetch": true,
    "files.exclude": {
        "**/.classpath": true,
        "**/.project": true,
        "**/.settings": true,
        "**/.factorypath": true
    },
    // "C_Cpp.updateChannel": "Insiders",
    "remote.SSH.remotePlatform": {
        "u-aizu-mac": "macOS",
        "u-aizu-std4dc27": "linux",
        "cadsv": "linux"
    },
    "[javascript]": {
        "editor.codeActionsOnSave": {
            "source.fixAll.eslint": true
        },
    },
    "workbench.startupEditor": "newUntitledFile",
    "workbench.editor.untitled.hint": "hidden",
    "terminal.integrated.scrollback": 20000,
    "terminal.integrated.cursorBlinking": true,
    "workbench.editorAssociations": {
        "*.enc": "default"
    },
    "C_Cpp.clang_format_style": "file",
    // おりたたみ
    "explicitFolding.rules": {
        "*": {
            "begin": "{{{",
            "end": "}}}"
        }
    },
    "json.maxItemsComputed": 10000,
    "bracketPairColorizer.depreciation-notice": false,
    "search.useIgnoreFiles": true,
    "terminal.integrated.enableMultiLinePasteWarning": false,
    "terminal.integrated.defaultProfile.windows": "PowerShell",
}
```

