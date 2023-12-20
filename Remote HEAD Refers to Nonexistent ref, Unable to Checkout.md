Tags: #git 

The following warning when cloning a repository indicates that something on the upstream side is wrong and requires an update:

```shell
$ git clone <uri_to_repo>
`warning: remote HEAD refers to nonexistent ref, unable to checkout.`
```

This may occur because the upstream is a newly created bare repository that doesn't have the default branch set.

On the client side, you can simply checkout the branch of interest:

```shell
$ git branch -a
$ git checkout branch-of-interest
```

Fixing the server requires modifying either `.git/HEAD` (for working copies) or `HEAD` (for bare repositories) so that the `ref:` line points to the default branch of interest.  The following will specify `main` as the default branch:

```
ref: refs/heads/main
```

Derived from this [Stackoverflow post](https://stackoverflow.com/questions/11893678/warning-remote-head-refers-to-nonexistent-ref-unable-to-checkout/15631690#15631690).