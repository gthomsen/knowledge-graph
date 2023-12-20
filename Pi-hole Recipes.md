# Flushing DNS Cache
Once a query has been made, Pi-hole caches the response so that future queries are faster.  Once the cached entry expires, another query is made - though depending on the DNS record's time-to-live (TTL) this may be a while.

Rather than waiting, restarting Pi-hole's DNS will flush its cache so that queries will be sent upstream again:
```shell
$ pihole resartdns
```

This [discussion thread](https://discourse.pi-hole.net/t/how-do-i-flush-my-pi-hole-cache/3020) has additional information.

# Additional Blocklists
The default block lists may not sufficient depending on needs.  Additional blocklists can be added through the web interface - either by logging into the Admin Console and clicking "Adlist" on the left, or by visiting `http://<pihole_ip>/admin/groups-adlists.php`.  Enter blocklist URLs along with their descriptions, one at a time, and click "Add".

A reasonable starting point for blocklists can be found at [The Firebog](https://firebog.net/).  Not every list needs to be added, though adding all of the green lists with a checkmark next to them works and provides protection against the following:
- Suspicious domains
- Advertising
- Tracking and telemetry
- Malicious hosts
- Cryptocurrency miners

Once additional blocklists are added, the Gravity database needs to be rebuilt:

```shell
$ pihole -g
```

