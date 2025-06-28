# About

GitHub Action to run [`buildcharts summary`](https://github.com/eddietisma/buildcharts) inside a Docker container.

This action uses the BuildCharts CLI to generate a summary.

- Reads `docker buildx history`.
- Parses logs.
- Generates a summary.

## Usage

```yaml
name: ci

on:
  push:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up BuildCharts
        uses: buildcharts/setup-action@v1

      - name: Generate BuildCharts pipeline
        uses: buildcharts/generate-action@v1
        
      - name: Docker build and test
        uses: docker/bake-action@v6
        with:
          source: .
          files: buildcharts.hcl
        env:
          VERSION: v1.0.0
          COMMIT: aaaaaaaa

      - name: Generate BuildCharts Summary
        uses: buildcharts/summary-action@v1
```


# Links
- https://docs.docker.com/reference/cli/docker/buildx/history/inspect/
- https://docs.docker.com/reference/cli/docker/buildx/history/logs/

```
docker buildx history ls --format json
docker buildx history inspect o6kz6yonn0e864qti1s7680hl
docker buildx history logs o6kz6yonn0e864qti1s7680hl

```