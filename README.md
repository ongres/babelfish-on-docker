# Babelfish on Docker

Docker environments for Babelfish test.


## Use current image

```bash
docker pull registry.gitlab.com/ongresinc/labs/babelfish-on-docker:latest
```

```
docker-compose -f docker-compose-remote.yml up 
```

Access through local:

```bash
docker-compose exec babelfishpg-ubuntu-focal bash -c 'sqlcmd -H localhost:1433 -P password -U bbf' 
```

To access through host mode in the same machine, it can be issued a similar command to the below (you may need to change the network name entry):

```bash
DOCKER_BBF_IP=$(docker inspect -f "{{with index .NetworkSettings.Networks \"babelfish-on-docker_babelfish\"}}{{.IPAddress}}{{end}}" babelfishpg-ubuntu-focal)
```

Then, you can either use your psql or your MSSQL Server client of preference ([FreeTDS](https://www.freetds.org/) in the following example):

```bash
/opt/babelfish/bin/psql -h ${DOCKER_BBF_IP} -p 5432 -U bbf bbf 
tsql -S ${DOCKER_BBF_IP} -p 1433 -U bbf bbf
```

> BABELFISH_DB is the Postgres database that has the Babelfish extensions, and it is called `master` in SQL Server. So, certain clients like DBeaver will need to specify the master instead of the Postgres name.

## Multi-DB / Single-DB

The current image uses multi-db as the default migration mode. It means that all the databases you create in the Babelfish database (through TDS), will be reflected as Postgres _schemas_ in the selected Babelfish database.

The mapped schemas will had the `*-dbo` suffix. This mode is useful if you rely on multi schema login against your SQL Server.

Single-DB will allow only one user database, and it might be the most recommended mode for beginners.


## Building

```bash
docker-compose build babelfishpg-ubuntu-focal
docker-compose up

docker tag babelfishpg:ubuntu.focal registry.gitlab.com/ongresinc/labs/babelfish-on-docker
docker tag babelfishpg:ubuntu.focal ghcr.io/ongres/babelfish-on-docker-compose
docker push registry.gitlab.com/ongresinc/labs/babelfish-on-docker
docker push ghcr.io/ongres/babelfish-on-docker-compose
```

See that you can add more distros in the same compose, and build by build argument as above.



## References

Other docker implementations found: 

- [from Toyonut](https://github.com/Toyonut/babelfish-testbed).
- [from rsubr](https://github.com/rsubr/postgres-babelfish)

