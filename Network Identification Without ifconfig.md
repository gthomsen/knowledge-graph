Tags: #linux 

Some systems do not install `net-tools` which means `ifconfig` is no where to be found.  The following parse the contents of `/proc/` and `/sys/` to extract information provided by `ifconfig`.

# Listing Adapter Addresses
To determine the address of each adapter:
```shell
$ awk '/32 host/ { print f } {f=$2}' <<< "$(</proc/net/fib_trie)" | sort -u
```

# Listing Adapter Routes
Magic:
```shell
ft_local=$(awk '$1=="Local:" {flag=1} flag' <<< "$(</proc/net/fib_trie)")

for IF in $(ls /sys/class/net/); do

    networks=$(awk '$1=="'$IF'" && $3=="00000000" && $8!="FFFFFFFF" {printf $2 $8 "\n"}' <<< "$(</proc/net/route)" )

    for net_hex in $networks; do

            net_dec=$(awk '{gsub(/../, "0x& "); printf "%d.%d.%d.%d\n", $4, $3, $2, $1}' <<< $net_hex)

            mask_dec=$(awk '{gsub(/../, "0x& "); printf "%d.%d.%d.%d\n", $8, $7, $6, $5}' <<< $net_hex)

            awk '/'$net_dec'/{flag=1} /32 host/{flag=0} flag {a=$2} END {print "'$IF':\t" a "\n\t'$mask_dec'\n"}' <<< "$ft_local"

    done

done
```