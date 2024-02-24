Tags: #utilities #sed

# Print Lines Between Markers
Print everything between `START PATTERN` and `STOP PATTERN`:
```shell
$ sed -n -e '/START PATTERN/,/STOP PATTERN/p' file.txt
```

A variant of the above omits `STOP PATTERN` and simply prints until the end of the file:
```shell
$ sed -n -e '/START PATTERN/,$p' file.txt
```

A variant of the above specifies the first line and prints from the first line of the file to the pattern:
```shell
$ sed -n -e '0,/END PATTERN/p' file.txt
```