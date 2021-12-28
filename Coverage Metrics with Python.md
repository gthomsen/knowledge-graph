Tags: #python #testing

Create coverage metrics and generate HTML in the current directory:

```shell
$ coverage -m pytest tests/test_foo.py
$ coverage html
```

Serve it with a local web server that lists on `localhost:8000`:
```shell
$ python -m http.server --bind localhost 8000
```