Tags: #git #software-engineering 

Custom formats can be applied to the output of `git log` via the `--pretty=<format>` option.  For example, the a format of `%h%x09%an%x09%ad%x09%s` produces:

```shell
$ git log --pretty=format:"%h%x09%an%x09%ad%x09%s"
3542c987        User Name    Wed Aug 2 16:35:08 2023 -0400   Topic: [WIP] Testing Python Module Benchmark Support Initial Addition
1e69060d        User Name    Wed Aug 2 12:01:50 2023 -0400   Topic: [WIP] Testing Python Module Renamed In Preparation for Benchmark Verification Support
6daad0cb        User Name    Tue Jul 25 16:24:36 2023 -0400  Topic: Merged 'regression_tests' Branch into 'main' Branch
...
```

Regularly used formats can be set as a Git configuration option:

```shell
$ git config pretty.format_name "%h%x09%an%x09%ad%x09%s"
```

Which then makes it available via `format_name` like so:
```shell
$ git log --format=format_name
...
```

