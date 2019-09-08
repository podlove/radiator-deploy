# radiator-deploy
Documentation and Sources on how to deploy [Radiator]

## Status
Radiator deployment is still in the bootstrap phase. Ideally we'd like to gather multiple different deployment scenarios with easy and quick entry points to get you up and running quickly.

## Components

To run [Radiator] you need these components:

1. A PostgreSQL database
2. An Amazon S3 compatible object storage service (e.g. [MinIO])
3. The main [Radiator] phoenix instance

Optionally:

* A frontend using the Backend API Radiator is providing (we default you to our own [radiator-cms])

## Docker

There are multiple stages to your Docker strategy.

1. The main [Radiator] repo does have a Dockerfile to form the basis for any docker deployment. 
2. A [docker-compose] file in the main repo to get you going locally just for quick turnaround testing/working - which includes database, minio and phoenix running on port `4000`.
3. This Repo with further variants
   1. macOS `.local` deployment, so you can run a full install locally. This includes [radiator-cms] and a configured [nginx] that is bundled in a way that it only listens to your `.local` address so you can show it around, test and work with it in your local network from multiple devices. Be aware that this setup doesn't use TLS so only use temporary passwords there. This can be found in `docker/radloc`
   2. Basic manual deployment on a single server that already has an [nginx] setup going. Further instructions can be found in `docker/radsingle`


### `docker/radloc` - macOS `.local` Setup

Basic compose file combination to work for your local mac. `./configure` is getting your `.local` name.

| Service     | URL                                     |
| ----------- | --------------------------------------- |
| Radiator    | http://[yourmachine].local:4000         |
| Minio data  | http://[yourmachine].local/media        |
| MailHog     | http://localhost:8025                   |
| GraphiQL    | http://[yourmachine].local/api/graphiql |
| RestAPI     | http://[yourmachine].local/api/rest/v1  |
| GraphQL API | http://[yourmachine].local/api/graphql  |

#### Run

```bash
cd docker/radloc
./configure
docker-compose build
docker-compose up
```

#### Remove

Data is persisted using docker volumes, so this way you can get a clean start:

```bash
cd docker/radloc
docker-compose down
docker volume rm radloc_minio_config radloc_minio_data radloc_psql_db
```



[Radiator]: https://github.com/podlove/radiator
[docker-compose]: https://docs.docker.com/compose/
[Dockerfile]: https://docs.docker.com/engine/reference/builder/
[MinIO]: https://min.io
[radiator-cms]: https://github.com/podlove/radiator-cms
[nginx]: https://www.nginx.com
