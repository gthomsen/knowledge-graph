Tags: #utilities #macos #linux #cheatsheet 

Mindmaps with lists encoded as children nodes are pasted with one child per line.  The following `sed` commands prepend the Markdown list formatting (`- `) and copies it to the clipboard for easy pasting into a separate tool.

Derived from [[Copying and Pasting in the Terminal with the Clipboard]].

# MacOS
```shell
$ sed -e 's/^/- /g' | pbcopy
```

# Linux
```shell
$ sed -e 's/^/- /g' | xclip -in -sel clipboard
```