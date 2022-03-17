Tags: #containers #singularity 

Singularity apparently does not track the `WORKDIR` when converting Docker images, which causes problems when the `ENTRYPOINT` command is a relative path like so:

```docker
WORKDIR /installed
ENTRYPOINT ["entrypoint.sh"]
```

Instead, one has to restructure things so that a full path is constructed for the `ENTRYPOINT` like so:

```docker
ENTRYPOINT ["/installed/entrypoint.sh"]
```

This was a known issue in June of 2019 and appears to remain a difference from Docker/Podman as of Singularity 3.8.

Unfortunately this makes it difficult to provide entry point commands that depend on build variables as `ENTRYPOINT` cannot use variables (neither `ARG` nor `ENV`).

Derived from this [University of Buffalo page](https://ubccr.freshdesk.com/support/solutions/articles/13000065627-error-when-using-docker-entrypoint-script-with-singularity).
