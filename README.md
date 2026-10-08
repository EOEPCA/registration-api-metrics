[![flake8](https://github.com/EOEPCA/registration-api-metrics/workflows/flake8/badge.svg)](https://github.com/EOEPCA/registration-api-metrics/actions)

# registration-api-metrics

EOEPCA Registration API metrics service.


## Workflow

- runs on a schedule (per `registration-api-metrics-management/docker/registration-api-metrics-management.cron`) to analyze a registration API instance (as defined in `$REGISTRATION_API_METRICS_API_URL`)
- queries registration API to derive metrics
- publishes to broker service (MQTT)
- sends metrics to a Prometheus collector
- collect real-time and offline Registration API metrics and makes them available as [OpenMetrics](https://openmetrics.io)
- provides analytics and visualization via [Prometheus](https://prometheus.io) and [Grafana](https://grafana.com)

## Installation

### Requirements
- Docker

### Dependencies
Dependencies are embedded in service definitions and orchestrated by Docker.

## Running

### Docker

The Docker setup uses Docker and Docker Compose to manage the following services:

- **registration-api-metrics-monitoring**: monitoring
  - **registration-api-metrics-metrics-collector**: metrics collector
  - **registration-api-metrics-prometheus**: metrics scraper
  - **registration-api-metrics-grafana**: analytics and visualization
- **registration-api-metrics-broker**: MQTT broker
- **registration-api-metrics-management**: management service to publich metrics from a Registration API instance (as defined in `$REGISTRATION_API_METRICS_API_URL`)

See [`registration-api-metrics.env`](registration-api-metrics.env) for default environment variable settings.

To adjust service ports, edit [`docker-compose.override.yml`](docker-compose.override.yml) accordingly.

The [`Makefile`](Makefile) in the root directory provides options to manage the Docker Compose setup.

```bash
# build all images
make build

# build all images (no cache)
make force-build

# start all containers
make up

# reinitialize backend
make reinit-backend

# start all containers in dev mode
make dev

# view all container logs in realtime
make logs

# login to the registration-api-metrics-management container
make login

# restart all containers
make restart

# shutdown all containers
make down

# remove all volumes
make rm
```

## Development

### Code Conventions

* [PEP8](https://www.python.org/dev/peps/pep-0008)

### Bugs and Issues

All bugs, enhancements and issues are managed on [GitHub](https://github.com/EOEPCA/registration-api-metrics/issues).

## Contact

* [Angelos Tzotsos](https://github.com/kalxas)
