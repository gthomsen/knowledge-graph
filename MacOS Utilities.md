Tags: #macos

# List User Identifiers
```shell
$ dscl . -list /Users UniqueID
_accessoryupdater        278
_amavisd                 83
_analyticsd              263
_appinstalld             273
_appleevents             55
_applepay                260
_appowner                87
_appserver               79
_appstore                33
_ard                     67
...
```

# List Groups
```shell
$ dscl . -list /Groups
_accessoryupdater
_amavisd
_analyticsd
_analyticsusers
_appinstalld
_appleevents
_applepay
_appowner
_appserveradm
_appserverusr
```
# Enumerate Group Membership
Lists all of the usernames (`Bob` below) belonging to a particular group (`staff` below):
```shell
$ dscacheutil -q group -a name staff
name: staff
password: *
gid: 20
users: root Bob _nsurlstoraged
```

# Query the Display Resolution

```shell
$ system_profiler SPDisplaysDataType | grep Resolution
          Resolution: 2560 x 1600 Retina
```

# Export Certificate Authority Chain from Keyring

```shell
$ security find-certificate -a -p /System/Library/Keychains/SystemRootCertificates.keychain > test.crt
$ security find-certificate -a -p /Library/Keychains/System.keychain >> test.crt
```

Originally from [here](https://stackoverflow.com/questions/41851601/how-do-i-export-all-ca-certificates-from-apple-keychain-into-a-single-pem-bundle).