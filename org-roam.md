Tags: #trade-study 
# Details
[![Roam Unicorn](https://camo.githubusercontent.com/91c10a024f9becaae8033e741c8f688ef7189c332b1a45dc4ca5846a82098300/68747470733a2f2f7777772e6f7267726f616d2e636f6d2f696d672f6c6f676f2e737667)]

[Github](https://github.com/org-roam/org-roam)

Knowledge management inside of Emacs using `org-mode` as the foundation.

[Blog post](https://blog.jethro.dev/posts/how_to_take_smart_notes_org/) describing note taking with `org-roam`.
# Observations
# Pros
1. Emacs-based.
2. Infinitely configurable via Lisp.
3. Local installation.
# Cons
1. Requires customization to setup the workflow.  Requires knowing what the workflow is _a priori_.
2. Infinitely configurable.
3. Functionality is split across a number of packages (`org-publish` or `ox-hugo` for publishing, `org-transclusion` for Org Mode transclusion, [[md-roam]] for Markdown support in Org Roam, etc)
# Deep Dive!
## Node Templates
`org-md` template to create a YAML heading with a topic-based file name.

```lisp
```emacs-lisp
(setq org-roam-capture-templates '(("m" "Markdown" plain ""
                                      :if-new
                                      (file+head "${slug}.md"
                                                 "---\ntitle: ${title}\nid: %<%Y-%m-%dT%H%M%S>\ncategory: \n---\n")
                                      :immediate-finish t))
        time-stamp-start "#\\+lastmod: [\t]*")```

Results in:
```
---
title:
id:
category:
roam_refs:
roam_aliases:
---
```
## Exporting Subset
[Exporting nodes](https://github.com/alexkehayias/emacs.d/blob/master/init.el#L1172) that aren't private can be done via a SQL `SELECT` statement.
# Questions
1. How do you install and configure `org-roam`?  How hard is it to do in an offline mode?
2. Unclear how hard the visualization integration is.  [`org-roam-ui`](https://github.com/org-roam/org-roam-ui)
3. What are the publishing options?  
    - `org-publish` pushes to static HTML
    - Export to external tool (e.g. Jekyll)
4. Real-time rendering?  LaTeX? 
5. Importing Markdown from an external source (e.g. [[Obsidian]])
    1. Coexisting with external edits?  Do you need to reindex anything if content is the only change?  This is necessary if a knowledge base is shared across multiple systems and periodically synchronized (e.g. laptop and server).
6. Is transclusion supported?  [`org-transclusion`](https://github.com/nobiot/org-transclusion) says yes.
