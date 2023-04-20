# `home-monitoring`

Configuration and tools to manage my home monitoring systems.

It will monitor a number of things for us:

- Internet connection: looking at upload and download speeds, but
  also the quality of the connection
- Unifi network infrastructure: (hopefully) filling some gaps in the
  capabilities of the Unifi management software
- Solar power generation: how much is our solar array generating, how
  much are we using/exporting, and so on

## Getting started

Everything is put together using [Docker
Compose](https://docs.docker.com/compose/), so you should just be able
to run:

```
docker compose up
```

Then open:

- [Grafana](http://localhost:3000/)
- [Prometheus](http://localhost:9090)
