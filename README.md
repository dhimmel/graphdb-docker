This keeps the infrastructure that builds docker images for [GraphDB](http://graphdb.ontotext.com/)

Check [Docker Hub Images](https://hub.docker.com/r/ontotext/graphdb/) for information on how to use the images.

Note that to use GraphDB EE or SE docker images, you must get a license from us first.

Currently there are no public images for GraphDB Free and you will have to
build those if needed from the zip distribution that you get after registering
on our website.

# Building a docker image based on the free edition

You will need docker and make installed on your machine.

1. Checkout this repository
1. Register on the Ontotext website for the GraphDB Free edition. Download the zip file and place it in the *free-edition* subdirectory
1. Run
```
make free VERSION=<the-version-that-you-got>
```

for example the most recent version as of this writing is 9.4.0 so run
```
make free VERSION=9.4.0
```

this will build an image that you can use called ontotext/graphdb:9.4.0-free.
You can run the image now with
```
docker run --detach --publish 7200:7200 ontotext/graphdb:9.4.0-free
```

Consult the docker hub documentation for more information.

## Upload to GitHub Package Registry

This section is custom to this fork of [`Ontotext-AD/graphdb-docker`](https://github.com/Ontotext-AD/graphdb-docker).

```bash
# tag image for GitHub Package Registry
docker tag \
  ontotext/graphdb:9.4.0-free \
  docker.pkg.github.com/dhimmel/graphdb-docker/ontotext-graphdb:9.4.0-free

# push to docker
docker push docker.pkg.github.com/dhimmel/graphdb-docker/ontotext-graphdb:9.4.0-free
```

See all packages at <https://github.com/dhimmel/graphdb-docker/packages/>.

## Run container

```bash
# create container from Package Regsitry image (only run first time)
docker container create \
  --name=ontotext-graphdb \
  --publish 7200:7200 \
  docker.pkg.github.com/dhimmel/graphdb-docker/ontotext-graphdb:9.4.0-free

# start container
docker start ontotext-graphdb

# stop container
docker stop ontotext-graphdb
```

Now visit <http://localhost:7200/>

# Issues

You can report issues in the GitHub issue tracker or at graphdb-support at ontotext.com


# Contributing

You are invited to contribute new features, fixes, or updates, large or small;
we are always thrilled to receive pull requests, and do our best to process
them as fast as we can.

Before you start to code, we recommend discussing your plans through a GitHub
issue, especially for more ambitious contributions. This gives other
contributors a chance to point you in the right direction, give you feedback on
your design, and help you find out if someone else is working on the same
thing.

# Making changes to the images and building your own version

The following command should be able to build you a custom image that takes your local changes into account

```
make ee VERSION=<version-of-graphdb-you-want>
```
for the enterprise edition and

```
make se VERSION=<version-of-graphdb-you-want>
```

for the standard edition.
