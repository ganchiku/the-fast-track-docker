# the-fast-track-docker

This is a docker image for Symfony 5: The Fast Track.
The original book is based on local environment for PHP development, but I find it is a bit difficult to set up environment. It requires some packages clients to be installed such as PostgreSQL, RabbitMQ, Redis, and some beginners try to start learning Symfony5 have hard time to go through the book.

That's a reason why I built this docker image. This docker image bundles dependent libraries such ash PostgreSQL, RabbitMQ, and Redis, and you do not need to install such library to your local environment. However, currently, there's no TLS support.


## symfony guestbook new without git
Because symfony application is in docker subdirectory, you need to ignore git init for creating new applicatoin. You can achieve it with `--no-git` option as follows:
```sh
docker-compose exec php symfony new guestbook --version=5.2 --no-git
```

## symfony command replacement
Because all symfony command runs in docker container, replace all command using `symfony` to `docker-compose exec php symfony` as folllows:
```sh
docker-compose exec php symfony composer req profiler --dev
```

## Run local server without TLS.
To run the local server without TLS support, run as follows:
```sh
docker-compose exec php symfony server:start --no-tls
```
Remember? we have added `docker-compose exec php` to the original command.



