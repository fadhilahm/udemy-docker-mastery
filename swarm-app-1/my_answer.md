# My Answer

1. Create the overlay network.

`docker network create --driver overlay backend`

`docker network create --driver overlay frontend`

1. Create the `vote` service.

`docker service create --name vote -p 80:80 --network frontend --replicas 2 bretfisher/examplevotingapp_vote`

1. Create the `redis` service.

`docker service create --name redis --network frontend redis:3.2`

1, Create the `worker` service.

`docker service create --name worker --network frontend --network backend bretfisher/examplevotingapp_worker`

1. Create the `db` service.

`docker service create --name db --network backend --mount type=volume,source=db-data,target=/var/lib/postgresql/data -e POSTGRES_HOST_AUTH_METHOD=trust postgres:9.4`

1. Create the `result` service.

`docker service create --name result -p 5001:80 --network backend bretfisher/examplevotingapp_result`
