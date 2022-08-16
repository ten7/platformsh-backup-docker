# Platform.sh backup for Docker

A docker container to run the Ansible ten7.platformsh_backup role.

## Configuration

Create a configuration file as described in the [ten7.platformsh_backup](https://github.com/ten7/platformsh-backup) Ansible role.

Once created, you have three ways to provide it to the container:
* As a base64-encoded value of the `PLATFORMSH_BACKUP_CONFIG` environment variable
* As a mounted file at the location specified by the `PLATFORMSH_BACKUP_CONFIG_FILE` environment variable
* As a mounted file at `/config/platformsh-backup/platformsh-backup.yml` inside the container.

## Use with base Docker

To run the Docker image as part of a script or in cron, use the following command:

```shell
docker run --rm -v /path/to/platformsh-backup.yml:/config/platformsh-backup/platformsh-backup.yml ten7/platformsh-backup
```

Note, that if your `platformsh-backup.yml` file depends on other files (such as SSH keys) you will need to add multiple `-v` switches to mount each one.

## Docker compose

Create the following Docker Compose file.

```yaml
version: '3'
services:
  backup:
    image: ten7/platformsh-backup
    volumes:
      - /path/to/platformsh-backup.yml:/config/platformsh-backup/platformsh-backup.yml
```

Again, if your `platformsh-backup.yml` depends on other files (such as SSH keys) you will need to add additional items under `volumes` to mount them.

Once the `docker-compose.yml` file is created, you can run backups using:

```shell
docker-compose run backup
```

## License

GPL v3

## Author Information

This Docker image was created by [TEN7](https://ten7.com/).

