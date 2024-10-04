---
description: >-
  Cryptlex On-premise will install and run on nearly any system supporting
  Docker.
---

# System Requirements

## Operating System

Cryptlex On-premise is deployed using Docker. Hence it can be deployed on any Linux, Mac, and Windows-based servers that can run current versions of Docker (at least version 20.10.22 or higher).&#x20;

## Storage and Memory

Cryptlex requires a minimum of 5GB to function for its database and docker images. Your exact storage size requirements will vary depending on the volume of licenses and the number of activations.

Cryptlex requires at least 1GB of memory to function. If the database is also installed on the same server then at least 4GB of memory is required.

## CPU

Cryptlex requires at least a dual-core CPU, and that will work for low volume installations. For anything more than that we recommend going with a quad-core CPU.

## Software

### Docker

Cryptlex requires at least version 18.06.0-ce of Docker.&#x20;

### Database <a href="#database" id="database"></a>

Cryptlex requires PostgreSQL 10.x (or higher) for storing all the data.

### Cache

Cryptlex uses Redis for storing the cache data. If no Redis database is provided it defaults to memory.

### Filestore

It uses [Minio](https://www.minio.io/), which is an Amazon S3 compatible object storage server, for storing release files. In case you don't want to use the Cryptlex [release management](https://docs.cryptlex.com/release-management) API, this is not required.

