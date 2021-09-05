# postgres
```

PGDATA=/var/lib/postgresql/data/pgdata
POSTGRES_PASSWORD=mysecretpassword

container=postgres
cmd='-c shared_buffers=256MB -c max_connections=200'
image=library/postgres:latest
mount=/var/lib/postgresql/data
network=postgres
restart=always
run=/run/postgresql
volume=postgres

docker \
    volume \
    create \
    ${volume}
docker \
    network \
    create \
    ${network}
docker \
    container \
    run \
    --detach \
    --env PGDATA=${PGDATA} \
    --env POSTGRES_PASSWORD=${POSTGRES_PASSWORD} \
    --name ${container} \
    --network ${network} \
    --read-only \
    --restart ${restart} \
    --volume ${run}:${run} \
    --volume ${volume}:${mount} \
    ${image} \
    ${cmd}

```
