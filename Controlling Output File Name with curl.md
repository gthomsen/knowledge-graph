Tags: #utilities 

`curl` writes the target URL's data to standard output by default unless specified via the `-o <output_name>` option.  Several options exist if `<output_name>` isn't known a priori.

Derived from [this Stack Overflow post](https://stackoverflow.com/questions/6881034/curl-to-grab-remote-filename-after-following-location).

# Naming Based on URL
`curl` can write file to a file that matches the last component in the URL specified via the `-O` option:
```sh
$ curl -O <URL>
```

# Naming Based on Content Disposition Header
`curl` 7.21.2, and newer, can respect the `Content-Disposition` header returned by the server and write data to that file, instead of the last component in the URL specified:

```sh
$ curl -O -J <url>
```
