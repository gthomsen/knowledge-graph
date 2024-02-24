Tags: #emacs #git #magit

The following Lisp code disables `whitespace-mode` in Magit's log, revision, and status modes:
```lisp
;; don't highlight whitespace when we're using Magit.  commit messages, long
;; lines in diffs, and commit metadata regularly have long lines and we don't
;; need to have them flagged (since we can't do anything about them).
(setq whitespace-global-modes '(not magit-diff-mode
                                    magit-log-mode
                                    magit-refs-mode
                                    magit-revision-mode
                                    magit-status-mode))
```

We need to directly configure `whitespace-mode` to ignore Magit-related buffers as it runs its hooks *after* Magit's mode hooks are evaluated.  If one is was to do the following, then `whitespace-mode` would be disabled for each Magit buffer and then immediately re-enabled:

```lisp
(eval-after-load "magit"
  '(progn
     (add-hook 'magit-status-mode-hook 'turn-off-whitespace-mode)
     (add-hook 'magit-revision-mode-hook 'turn-off-whitespace-mode)
     (add-hook 'magit-log-mode-hook 'turn-off-whitespace-mode)))
```

The Magit `magit-*-section-hook`'s are not the right answer as those are used for adding content into the Magit buffers, rather than when a buffer is created.

Unfortunately these easily found references are red herrings:
- [Reddit disabling `whitespace-mode` in Magit buffers](https://reddit.invak.id/r/emacs/comments/fmd2qo/disabling_globalwhitespacemode_in_magit_buffers/)
- [Magit manual - Section Hooks](https://reddit.invak.id/r/emacs/comments/fmd2qo/disabling_globalwhitespacemode_in_magit_buffers/)
