Tags: #linux #macos #utilities #X11 #user-configuration 


# pbcopy + pbpaste
`pbcopy` and `pbpaste` are MacOS utilities that copy and pastes text from standard input/output to/from the clipboard.

```shell
# copy some of the current directory's listing onto the clipboard.
$ ls | head | pbcopy

# print the contents of the clipboard.
$ pbpaste
Apply Expressions to netCDF Data.md
Benchmarking FFTW.md
Benchmarking libxsmm Performance.md
Changing netCDF Chunk Sizes.md
Conda Quirks.md
Container Networking Explained.md
Copying and Pasting in the Terminal with the Clipboard.md
Creating Self-Signed Certificate.md
Creating a Certificate Authority.md
Debian.md
```

# xclip
`xclip` is a Linux utility that copy and paste text from standard input/output to/from X11 selections, including the clipboard.

```shell
# copy the current directory's listing onto the clipboard selection.
$ ls -la | xclip -in -sel clipboard

# print the contents of the clipboard.
$ xclip -out -sel clipboard
total 28
drwxrwxr-x  4 gthomsen gthomsen 4096 Jul 27 12:46 .
drwxrwxr-x 68 gthomsen gthomsen 4096 Dec 18 13:20 ..
drwxrwxr-x  2 gthomsen gthomsen 4096 Jul 27 13:02 docker-squid
drwxrwxr-x  8 gthomsen gthomsen 4096 Dec 26 11:33 .git
-rw-rw-r--  1 gthomsen gthomsen 1070 Jul 27 12:46 LICENSE
-rw-rw-r--  1 gthomsen gthomsen 7259 Jul 27 12:46 README.md
```

The following aliases make working with `xclip` a little easier:

```shell
alias xpaste='xclip -out -sel clipboard'
alias xcopy='xclip -in -sel clipboard'
```