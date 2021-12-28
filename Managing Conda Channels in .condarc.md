Tags: #python #conda #user-configuration 

Channels can be specified in `.condarc` so they aren't repeatedly specified on the command line.  Priotization can also be requested in the case where channels overlap in what they offer.

Specified like so:
```shell
channels:
    - a
    - b
    - c

# package resolution searches channel a, before b, before c.  without
# the following, then the resolution order is ???
channel_priority: true
```

# Channels for Machine Learning Development

Configuration for machine learning with Python:
```shell
channels:
    - pytorch
    - defaults
    - conda-forge

channel_priority: true
```