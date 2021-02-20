# vettadock/mysql-old Docker image

This Docker image contains obsolete MySQL versions, not supported anymore by the vendor.
We try to only include the last release form each version, because the need to run an obsolete release
from an obsolete version is extremely unlikely. However, including the latest release
is not always possible.
The MySQL daemon however runs on Ubuntu versions that are as modern as possible,
because there is probably no need to run it on obsolete environments.

MySQL is built from generic Linux binaries. These binaries are downloaded from [VettaArchive](https://archive.vettabase.com),
a project that makes old software versions available. Generic binaries can be used
on any Linux distribution. We don't want to make the repository bloat by adding distro-specific
packages.

You can pull the image from DockerHub. See [VettaDock](https://hub.docker.com/r/vettadock/mysql-old).

Support for images and containers created from this repository is available at
[Vettabase](https://vettabase.com).


## Motivation

Vettabase does not recommend to run obsolete versions of MySQL - or any other server technology.

However, some organisations simply do it. Keeping software upgraded means to invest resources in it,
and sometimes organisations simply don't think the benefits are worth the price. Hopefully
it is software for internal use, that does not contain sensitive or critical data. But,
whatever the reason, these organisations need packages for that software and
consulting in case of troubles. Vettabase is here to help.


## Supported versions

Supported versions:

- 5.5
- 5.1
- 5.0
- 4.1

Each supported version is an image tag.


## Building the image

To build the image from a Dockerfile, first move to the Dockerfile directory, then run:

```
docker build --no-cache --tag <image_name>:<tag> .
```


## Create and use a container

A container can be used in this way:

```
docker run --detach --name <container-name> mysql-old:5.0
docker start <container-name>
```

To connect MySQL using the mysql client inside the container:

```
docker exec -ti <container-name> mysql
```


## Security concerns

When a container is created, the root user has no password. At this point there is not data,
so creating a temporary password would bring no benefit. Creating proper users and
passwords is your responsibility.

We believe that official MySQL, Percona Server and MariaDB containers should do the same, even if
it sounds less cool.

MySQL runs as mysql:mysql. Any other command run via do `docker exec` will run as root.
However, to run such commands you need to be root in the host. This allows you to access
all containers data, destroy containers, and even replace them with a flavour you created.
For this reason, we don't see the root user as a security risk in this context.
However, if you believe there is a valid reason to avoid using root in a container,
please file a bug and explain your point of you. We love to be persuaded when we are wrong.


## TODO

- Add a configuarion file
- Add VOLUMEs in Dockerfile
- Add documentation on how to expose ports, specify volumes for containers, or using Docker networks
- Add documentation on how to perform backups


## Contributing

The best ways of contributing this project are:

- Report bugs.
- Let us know that you are using this image, see out mail below.
- Tell us why you need to run obsolete MySQL versions.
- Let us know about any old tool you need that is not included in this project (file a bug).


## Credits and contacts

This repository is maintained by Vettabase.

For questions or commercial support enquiries, please contact info@vettabase.com.

