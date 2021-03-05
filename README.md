# common

Common services for `docker-compose.yml`.

## Services

### Mastodon

The use of [docker-compose.mastodon.yml](docker-compose.mastodon.yml) is kinda special.

Clone this repository as submodule and create `docker-compose.common.yml` in the same directory.
Write common settings to the service named mastodon inside `docker-compose.common.yml`.

```docker-compose.common.yml
services:
  mastodon:
    # image name
    image: tootsuite/mastodon:latest
    # env file or environment valiables
    env_file: .env.production
    # hostnames
    extra_hosts:
      - 'db-host:ip-addr'
```

Finally use [common/docker-compose.mastodon.yml](docker-compose.mastodon.yml) in `docker-compose.yml`.

```docker-compose.yml
services:
  web:
    extends:
      file: common/docker-compose.mastodon.yml
      service: web
  streaming:
    extends:
      file: common/docker-compose.mastodon.yml
      service: streaming
  sidekiq:
    extends:
      file: common/docker-compose.mastodon.yml
      service: sidekiq
    environment:
      DB_POOL: 60
```
