# Housekeeping

The [housekeeping](https://github.com/SpecterOps/Nemesis/tree/main/projects/housekeeping/) service handles the automated cleanup of expired files and database entries.

This service periodically checks for files and database entries that have passed their expiration date and removes them from both the Minio storage and the database tables. This helps maintain system performance and ensures compliance with data retention policies.

When the serivce runs, entries in the database with an "expiration" datetime value past the current time will be removed, along with their associated files in the Minio datalake.

## Features

- Scheduled daily cleanup of expired data (configurable)
- Handles deletion of files from Minio storage
- Cleans up related database entries
- Supports manual triggering of cleanup jobs
- Maintains proper logging of cleanup activities

## Configuration

The service can be configured using environment variables:

- `CLEANUP_SCHEDULE`: Cron expression for the cleanup schedule (default: `0 0 * * *` - midnight every day)
- `LOG_LEVEL`: Set the logging level (default: `INFO`)

These ENV variables can be adjusted in the [docker-compose.yml](https://github.com/SpecterOps/Nemesis/tree/main/docker-compose.yml) file.

## Endpoints

- `GET /healthz`: Health check endpoint for Docker healthcheck
- `GET /`: Service information
- `POST /trigger-cleanup`: Manually trigger a cleanup job
