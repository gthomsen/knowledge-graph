Tags: #emacs #unfinished 

The `align` package provides a framework for aligning text about common points (e.g. about a `=` in an expression).  Should a mode not do the right thing, the most likely culprit is how the rules' `align-region-separate` is set.  This should almost always be set to `entire`, though `largest` is also suitable (though not implemented as of 2017/02/03).

# Custom Alignment Rules
Custom rules have the form of:
```lisp
'(rule-name
  (regexp . "...")
  (group N)
  (modes . mode-of-interest)
  ...
  )
```
Additional attributes can be specified for each rule, though at the heart one must specify the line structure so `align` can reformat its components, and which modes the rule should be applied.

Each rule's `regexp` is applied to lines that match, and is expected to have capture groups that partitions the line into components.  The `group` option specifies which components should be aligned (possibly justified according to [[#Alignment Options|additional options]]).

Consider the following line:
```
       11111111   222222     3333333
        11111111111 222222 33
     111111111111111      222      3333333333
```
and the following regular expression:
```lisp
  (regexp "\\([1]+\\)\s-*\\([2]+\\)\s-*\\([3]+\\)")
```

Specifying `(group 1)` produces:
```
                        11111111   222222          3333333
                     11111111111 222222                 33
                 111111111111111      222       3333333333
```
Analysis:
1. 

Specifying `(group 2)` produces:
```

```
Analysis:
1. All of the 


Specifying `(group 3)` produces:
```

```

Specifying `(group 1 2)` produces:
```
    
```

Specifying `(groups 1 3)` produces:
```
             11111111   222222         3333333
          11111111111   222222              33
      111111111111111   222         3333333333
```

## Alignment Options
Common options for alignment rules include:
- `separate` - String specifying how regions are separated, which controls the extent overwhich alignment is applied.  `entire` aligns everything in the region regardless of line breaks or comments.  `group` aligns one or more groups within the region, where a group is delimited by newlines or comments.  Additional options are available - see the source code.
- `justify` - Flag specifying whether alignment should be right-justified.  Defaults to `t` so the matched group is right-justified.  **NOTE:** I get _weird_ behavior when specifying as `nil`.
- `case-fold` - Flag specifying whether the regular expression should be case insensitive.  Defaults to `nil`.

# Custom Alignment Package
**NOTE:** Most use cases only require [[#Custom Alignment Rules|adding additional rules]], not a full package.

Building a custom package to align a particular language is straight forward.  At a high level it requires the following:
1. Defining region separators that constraints alignment within
2. Create a package loader that installs the rules and hooks
3. Define each of the alignment rules of interest

The [`align-f90` package](https://github.com/jannisteunissen/align-f90/blob/master/align-f90.el) is a simple example of this.

The bulk of the work will be spent crafting the [[#Custom Alignment Rules|rules]] which will require testing [[Regular Expressions in Emacs|Emacs regular expressions]] in [[Regular Expressions in Emacs#Regexp Builder|regexp-builder]].  Once the rules are created, creating an Emacs package is on the order of an hour-worth of work.

# Testing Custom Rules
```lisp
;; load the align package.
(require 'align)

;; add the test list ot the beginning of 'align-rules-list.
(add-to-list 'align-rules-list
             '(test-alignment
               (regexp . "\\([1]+\\)\\s-*\\([2]+\\)\\s-*\\([3]+\\)")
               (group 1)
               (justify . t)))

;; ... test alignment against target string(s).

;; remove the test rule so another can be tested.
(setq align-rules-list (cdr align-rules-list))
```