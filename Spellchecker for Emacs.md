Tags: #emacs #macos 

Emacs on MacOS doesn't include a native spellchecker.

# aspell
[`aspell`](http://aspell.net/) is more robust for English than `ispell`, which focuses on internationalization.

Installation into `/usr/local/`:

```shell
$ wget https://ftp.gnu.org/gnu/aspell/aspell-0.60.8.tar.gz
$ tar zxf aspell-0.60.8.tar.gz
$ ./configure && make && sudo make install
```

Install `aspell`'s English dictionary ([master list](https://ftp.gnu.org/gnu/aspell/dict/0index.html))

```shell
$ wget https://ftp.gnu.org/gnu/aspell/dict/en/aspell6-en-2020.12.07-0.tar.bz2
$ tar zxf aspell6-en-2020.12.07-0.tar.bz2
$ ./configure && make && sudo make install
```
# Emacs Configuration
Add `(setq ispell-program-name "aspell")` into your Emacs configuration.

Specifically into the MacOS section of `~/.emacs.d/site.el`.