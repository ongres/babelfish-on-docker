# Babelfish on Docker

Docker environments for Babelfish test.


## Use current image

```bash
docker pull registry.gitlab.com/ongresinc/labs/babelfish-on-docker:latest
```

Or, use compose:

```bash
docker-compose build babelfishpg-ubuntu-focal
docker-compose up
```

See that you can add more distros in the same compose, and build by build argument as above.


Access:

```bash
docker-compose exec babelfishpg-ubuntu-focal bash -c 'sqlcmd -H localhost:1433 -P password -U bbf' 
```


## Build dev

```
docker tag babelfishpg:ubuntu.focal registry.gitlab.com/ongresinc/labs/babelfish-on-docker
docker tag babelfishpg:ubuntu.focal ghcr.io/ongres/babelfish-on-docker-compose
docker push registry.gitlab.com/ongresinc/labs/babelfish-on-docker
docker push ghcr.io/ongres/babelfish-on-docker-compose
```


## References

Other docker implementations found: 

- [from Toyonut](https://github.com/Toyonut/babelfish-testbed).
- [from rsubr](https://github.com/rsubr/postgres-babelfish)

