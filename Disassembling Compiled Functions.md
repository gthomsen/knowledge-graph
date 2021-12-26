Tags: #utilities #software-engineering

# Identify Available Functions
```shell
$ objdump -d executable | grep '>:'
```

# List Instructions Used by Function
Find the function name of interest using [[#Identify Available Functions]].
```shell
$ objdump -d file.o | sed -n '/function_name>:/,/^ *$/p' | cut -f3 | cut -d ' ' -f1 | sort -u
```

# Show Disassembly of Function
```shell
$ objdump -d file.o | sed -n '/function_name>:/,/^ *$/p' | less
```