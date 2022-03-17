Tags: #emacs #cheatsheet #regexp

Search with regular expressions using `C-M-s`.

# Regular Expression Syntax
Emacs has its [own syntax](https://www.emacswiki.org/emacs/RegularExpression#regexp) which is neither PCRE nor POSIX.  Below are commonly used tokens though the [[#Regexp Builder]] is highly recommended to interactively test out patterns.

Repetition:
- `*` - previous character/group, zero or more times (greedy)
- `+` - previous character/group, one or more times (greedy)
- `?` - previous character/group, zero or one time (greedy)
- `*?` - previous character/group, zero or more times (non-greedy)
- `+?` - previous character/group, one or more times (non-greedy)
- `??` - previous character/group, zero or one time (non-greedy)
- `\{N\}` - previous character/group, N times
- `\{N,\}` - previous character/group, N or more times
- `\{N,M\}` - previous character/group, N to M times

Anchors:
- `^` - beginning of line
- `$` - end of line
- `\w` - word constituent
- `\b` - word boundary

Grouping:
- `\(` and `\)` - start and end of group
- `\|` - group separator
- `\N` - reference to the Nth group matched (1-based)

Characters:
- `.` - any non-newline character
- `\` - escape the next character
- `[...]` - any character in between the brackets
- `[^...]` - any character not between the brackets
- `[a-z]` - range of characters

Syntax classes:
- `\s-` - Whitespace characters
- `\sw` - Word constituent
- `\s_` - Symbol constituent

Character classes:
- `[:digit:]` - any digit
- `[:alpha:]` - any letter
- `[:upper:]` - any upper-case letter (negate to get lower-case letters)
- `[:alnum:]` - any alphanumeric
- `[:space:]` - whitespace, as defined by the current syntax table

# Regexp Builder
Enter with `M-x regexp-builder` to create a sub-buffer that highlights matches in the original buffer.

Useful keybindings:
- `C-u C-x =` - Describe what is at the current point.  Useful for identifying which match was highlighted.
- `C-c C-w` - Copy the regexp into elisp format
- `C-c C-s` - Go to the next match
- `C-c C-r` - Go to the previous match
- `C-c C-b` - Switch the target buffer the Builder searches
- `C-c C-q` - Quit Regexp Builder

By default the Builder accepts elisp syntax though this isn't the most intuitive.  The following switches it to human-readable (according to the syntax listed [[#Regular Expression Syntax|above]]) for interactive use:

```lisp
# NOTE: 'read is the default.  set it back when editing existing regular
#       expressions.
(setq reb-re-syntax 'string)
```

Copy the elisp version via `C-c C-w` once the expression has been created.


