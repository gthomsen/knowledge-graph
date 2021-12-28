Tags: #squid #service 

[Hacker News article](https://news.ycombinator.com/item?id=15434943) with links for chaining proxies together.  Talks about Privoxy -> Squid -> Internet, transparent MITM proxying with MITM, and mitmproxy.

[Blog post](https://jpetazzo.github.io/2014/06/17/transparent-squid-proxy-docker/) Jerome Petazzoni about transparently routing HTTP traffic from a container to Squid.  Back from the days where there was still quite a bit of HTTP traffic.  Cannot transparently cache HTTPS traffic.  This [Github gist](https://gist.github.com/int128/aecad331dc66b2272bf0) has more details.