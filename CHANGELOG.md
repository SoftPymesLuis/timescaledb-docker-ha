# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

These are changes that will probably be included in the next release.

### Added
### Changed
 * Allow restore from backup even when no master is running
### Removed
### Fixed
 * Backup parameters

## [v0.2.10] - 2020-04-20

### Added
 * Support PostgreSQL 12
 * Support for TimescaleDB 1.7 (PostgreSQL 11 & PostgreSQL 12)
 * Remove stale pidfile if it exists
 * Include `strace` for debugging
### Changed
 * Build 2 sets of Docker images in CI/CD (PostgreSQL 11 & PostgreSQL 12)
### Fixed
 * Fail build if a single item in a loop fails
### Removed
 * Some perl dependencies of `pgBackRest`, which are no longer needed
     as `pgBackRest` is now fully written in C


## [v0.2.9] - 2020-02-13

### Changed
 * PostgreSQL 11.7 was released
 * PostGIS is now included in all the Docker images

     This reduces the number of images that need to be built, maintained and supported

#### Build process
 * Add Labels to the Docker images, in line with the Open Container Initiative
 [Annotations Rules](https://github.com/opencontainers/image-spec/blob/master/annotations.md#rules) for their Image Format Specification.

     These labels can be used to identify exact version information of TimescaleDB, PostgreSQL and some
     other extensions, as well as the default labels for `created`, `revision` and `source`.

     This deprecates adding  the `scm-source.json` that was added to the Docker Images.
 * Improve build & release process


## [v0.2.8] - 2020-01-15

### Added
 * Create a additional Docker image including PostGIS
### Changed
 * TimescaleDB 1.6.0 was released

## [v0.2.7] - 2019-11-14

### Changed
 * PostgreSQL 11.6 was released
 * TimescaleDB 1.5.1 was released


## [v0.2.6] - 2019-11-06

### Changed
 * Reduce log output during installation of tsdbadmin scripts

## [v0.2.5] - 2019-10-31

### Added
 * Include pgextwlist to allow extension whitelisting
 * Possibility to build a Docker image for a given repository and/or tag
 * TimescaleDB 1.5.0 was released and is now included

## [v0.2.4] - 2019-10-29

### Added
 * pg_prometheus is now part of the Docker image
### Changed
 * Pass on all PostgreSQL parameters to Patroni
### Fixed
 * timescaledb-tune runs with the PG_MAJOR version

## [v0.2.3] - 2019-10-09
### Added
* Install [tsdbadmin](https://github.com/timescale/savannah-tsdbadmin/) scripts into postgres database

## [v0.2.2] - 2019-09-11

### Changed
* TimescaleDB 1.4.2 was released, rebuilding the Docker image to include that version

## [v0.2.1] - 2019-09-06

### Changed
* The default command for the Dockerfile is now "postgres". This ensures we have the same interface as other Docker images out there.

## [v0.2.0] - 2019-08-30

### Added
 * Allow PostgreSQL compile time customizations to be made.

  Some environments benefit from being able to change things like `NAMEDATALEN`.
 * Makefile to aid in building the Docker image
 * Gitlab CI/CD configuration to trigger automated builds
 * Entrypoint for `pgBackRest`
 * The TimescaleDB extension is added to the `template1` and `postgres` database
 * Git context is injected into the Docker image

### Changed
 * Default entrypoint is `docker_entrypoint.sh`.

  This enables the Docker image to also be used in a non-kubernetes environment, allowing
  developers to run the exact same software as production environments.

 * Default Docker repository names
 * Failure of first backup does not fail the database initialization

### Removed
 * Removed many packages to reduce Docker image size without breaking TimescaleDB

### Fixed
 * Only configure a Patroni namespace if a `POD_NAMESPACE`



## [v0.1.0] - 2019-08-30
This is the first stable release of the TimescaleDB HA Docker image.
It was built from the [TimescaleDB Operator](https://github.com/timescale/timescaledb-operator/tree/v0.1.0) before
this repository was split away from it.

### Added
 * A Docker image based on Debian buster

 The basic components of the Docker image are:
  * [TimescaleDB](https://github.com/timescale/timescaledb), all recent releases
  * [PostgreSQL](https://github.com/postgres/postgres)
  * [Patroni](https://github.com/zalando/patroni)
  * [pgBackRest](https://github.com/pgbackrest/pgbackrest)

This Docker image can be used in the same way as the (smaller) public
[TimescaleDB Docker](https://github.com/timescale/timescaledb-docker) image,
however this image has HA built in, which leverages Patroni to do
auto failover of PostgreSQL if needed.
