Tags: #macos 

# Listing Attributes
```shell
$ ls -la@ ~/Downloads/download.zip
-rw-r--r--@   1 user  staff   6148 Jan 31 20:44 download.zip
	com.apple.quarantine	   58
```

# Removing Attributes
Removing an `attribute` from a file or directory:
```shell
$ xattr -r attribute /path/to/file
```

Recursively removing an `attribute` from a directory:
```shell
$ xattr -r attribute /path/to/directory
```

## Removing MacOS's Quarantine Attribute
Files downloaded from the internet are quarantined by default to limit the effect of malware.  The `com.apple.quarantine` attribute is added to each file downloaded, and it is somehow propagated when derivative files are made (e.g. unpacking a `.zip` file).

```shell
$ xattr -r com.apple.quarantine ~/Downloads/downloaded.zip
```