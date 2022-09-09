# Run Blockscout in development

This document describes how to run the blockscout service in development in both `dev` and `prod` modes.

## Prepare the network

Blockscout needs to access the database and the JSON-RPC provided by the service `zkevm-node-db` in the [zkevm-bridge-service](https://github.com/0xPolygonHermez/zkevm-bridge-service). To enable this access through docker you will need to add this `network` setting to the [docker-compose.yml](https://github.com/0xPolygonHermez/zkevm-bridge-service/blob/main/docker-compose.yml) of the `zkevm-bridge-service` and start the services:

```
networks:
  default:
    name: zkevm
```

## Select the desired environment

Blockscout has an env var `MIX_ENV` that is defined in the [docker-compose.yml](../../docker/docker-compose.yml). Set its value to either `dev` or `prod`:

* `dev` will instruct Blockscout to run in dev mode. This includes a file watch mechanism that will reload the browser whenever a file changes.
* `prod` will instruct Blockscout to run in prod mode.

## Build the app

Before you run the app you will have to build it. We have 2 build flavors according to the value of the `MIX_ENV` env var.

Access the `docker` folder and run `make build-dev` for `dev` or `make build-prod` for `prod`.

## Run the app

Once the build is ready you can start the container with `make start-compose`. After about a minute it should be available at `http://localhost:4010/`. Use `make stop-compose` to stop the container.
