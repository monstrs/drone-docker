# drone-docker

[![Build Status](http://beta.drone.io/api/badges/drone-plugins/drone-docker/status.svg)](http://beta.drone.io/drone-plugins/drone-docker)
[![Go Doc](https://godoc.org/github.com/drone-plugins/drone-docker?status.svg)](http://godoc.org/github.com/drone-plugins/drone-docker)
[![Go Report](https://goreportcard.com/badge/github.com/drone-plugins/drone-docker)](https://goreportcard.com/report/github.com/drone-plugins/drone-docker)
[![Join the chat at https://gitter.im/drone/drone](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/drone/drone)

Drone plugin can be used to build and publish Docker images to a container
registry. For the usage information and a listing of the available options
please take a look at [the docs](DOCS.md).

## Build

Build the binary with the following commands:

```
GO15VENDOREXPERIMENT=1 CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -tags netgo
GO15VENDOREXPERIMENT=1 go test
```

## Docker

Build the docker image with the following commands:

```
docker build --rm=true -t plugins/docker .
```

Please note incorrectly building the image for the correct x64 linux and with
GCO disabled will result in an error when running the Docker image:

```
docker: Error response from daemon: Container command
'/bin/drone-docker' not found or does not exist..
```

## Usage

Execute from the working directory:

```
docker run --rm \
  -e PLUGIN_TAG=latest \
  -e PLUGIN_REPO=octocat/hello-world \
  -e DRONE_COMMIT_SHA=d8dbe4d94f15fe89232e0402c6e8a0ddf21af3ab \
  -v $(pwd):$(pwd) \
  -w $(pwd) \
  --privileged \
  plugins/docker --dry-run
```
