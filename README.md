# postgres-plv8

Docker images for running [plv8](https://github.com/plv8/plv8) 1.4, 1.5 and 2.x on Postgres 9.4, 9.5, 9.6, 10, 11, 12 and 15. Based on the [official Postgres image](http://registry.hub.docker.com/_/postgres/).

[![neio/postgresql_plv8_ip4r][docker-pulls-image]][docker-hub-url] [![neio/postgresql_plv8_ip4r][docker-stars-image]][docker-hub-url] [![neio/postgresql_plv8_ip4r][docker-size-image]][docker-hub-url] [![neio/postgresql_plv8_ip4r][docker-layers-image]][docker-hub-url]




## Usage

### How to use this image

This image behaves exactly like the official Postgres image with the only difference being the inclusion of the plv8 extension.

```sh
$ docker run -d --name postgres neio/postgresql_plv8_ip4r
$ docker exec -it postgres bash -c "psql -U postgres -c \"CREATE EXTENSION plv8; SELECT extversion FROM pg_extension WHERE extname = 'plv8';\""
```

You should see the version of the plv8 extension installed.

You can optionally create a service using `docker-compose`:

```yml
postgres:
  image: neio/postgresql_plv8_ip4r
```

## Image variants

The `neio/postgresql_plv8_ip4r` image comes in multiple flavors:

### `neio/postgresql_plv8_ip4r:latest`

Points to the latest release available of Postgres stable with compatible plv8 installed. Occasionally pre-release versions will be included.

### `neio/postgresql_plv8_ip4r:<majorPostgresVersion>`

Points to the latest release available of Postgres `<majorPostgresVersion>` with the latest release available of plv8 `<plv8Version>` installed.

## Supported Docker versions

This image is officially supported on Docker version 19.03, with support for older versions provided on a best-effort basis.

## License

MIT

[docker-hub-url]: https://hub.docker.com/r/neio/postgresql_plv8_ip4r
[docker-pulls-image]: https://img.shields.io/docker/pulls/neio/postgresql_plv8_ip4r.svg?style=flat-square
[docker-stars-image]: https://img.shields.io/docker/stars/neio/postgresql_plv8_ip4r.svg?style=flat-square
[docker-layers-image]: https://img.shields.io/microbadger/layers/neio/postgresql_plv8_ip4r.svg?style=flat-square
[docker-size-image]: https://img.shields.io/microbadger/image-size/neio/postgresql_plv8_ip4r.svg?style=flat-square
