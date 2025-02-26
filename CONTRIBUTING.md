# Contributing

First of all, **thank you**!

To run tests, you will need [Docker] installed on your machine. This repository
uses [docker-compose] to run multiple Cassandra instances in parallel on
different ports to test different features (such as authentication or SSL
encryption). To run normal tests, do this from the root of the project:

```bash
docker-compose up --daemon
mix test
```

The `--daemon` flag runs the instances as daemons in the background. Give it a
minute between starting the services and running `mix test` since Cassandra
takes a while to start. You can check whether the Docker containers are ready
with `docker-compose ps`. To stop the services, run `docker-compose stop`.

To run tests for Scylla, you'll need a different set of services and a different
test task:

```bash
docker-compose --file docker-compose.scylladb.yml up --daemon
mix test.scylladb
```

Use `docker-compose --file docker-compose.scylladb.yml stop` to stop Scylla when
done.

By default, tests run for native protocol *v5* except for a few specific tests
that run on other protocols. If you want to limit the test suite to a native
protocol, use:

```bash
CASSANDRA_NATIVE_PROTOCOL=v4 mix test
```

[Docker]: https://www.docker.com
[docker-compose]: https://docs.docker.com/compose/
