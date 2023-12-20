Tags: #software-engineering #shell-scripting #regexp #utilities 

The one-or-more occurrence operator (`+`)is not part of the basic regular expressions supported by `sed` and must be enabled via the extended/modern regular expressions flag in most implementations.  Without this, the `+` operator is matched literally which is not likely what is desired.

Unfortunately, there is no standard flag for extended/modern regular expressions so for GNU `sed` use `-r` and for MacOS's `sed` use `-E` like so:

```shell
$ echo "a     b c   d" | sed -e 's/ +/ /g'
a     b c   d
# GNU sed.
$ echo "a     b c   d" | sed -r -e 's/ +/ /g'
a b c d
# MacOS sed.
$ echo "a     b c   d" | sed -E -e 's/ +/ /g'
a b c d
```