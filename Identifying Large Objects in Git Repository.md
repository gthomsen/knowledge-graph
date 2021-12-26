Tags: #software-engineering #utilities #git

Large files results in repository bloat.  If said files were inadvertently checked in, then it has an impact on cloning the repository.

# Identification
Identifying large files in a repository that may have been inadvertently checked in.

```shell
$ git rev-list --all --objects | \
    sed -n $(git rev-list --objects --all | \
    cut -f1 -d' ' | \
    git cat-file --batch-check | \
    grep blob | \
    sort -n -k 3 | \
    tail -n40 | \
    while read hash type size; do 
         echo -n "-e s/$hash/$size/p ";
    done) | \
    sort -n -k1
```

From [StackOverflow](https://stackoverflow.com/questions/1029969/why-is-my-git-repository-so-big).

# Removing
[`git-filter-repo`]([https://github.com/newren/git-filter-repo](https://github.com/newren/git-filter-repo)) removes specific paths out of a repository and creates a new one.  The [examples]([https://github.com/newren/git-filter-repo/blob/docs/html/git-filter-repo.html#EXAMPLES](https://htmlpreview.github.io/?https://github.com/newren/git-filter-repo/blob/docs/html/git-filter-repo.html#EXAMPLES)) are useful.

Rough workflow is:
1. Clone the target repository.
2. Filter out the file(s) in question.
    `$ git filter-repo --path path/to/BIG_FILE --invert-paths`
    Specify `--path ...` as many times as necessary.
3. Review the contents and history to ensure everything is good.
4. Force push the repository.  Be sure to coordinate with others.
    `$ git push -f master`