# Docker-mysql-backup-s3

container to backup and restore your mysql database's to using awscli.

# Container startup explained

* This container user cron to make backups
* Mysql will dump the database to this container and compress it using gzip
* Using s3cli the file will be uploaded to S3 Storage
* To restore a db just enter the container and run the 'restore' script with the file name to restore:

  ```bash
  ./restore example.sql.gz
  ```

* To run a manual backup just enter the container and run:

  ```bash
  ./backup
  ```

# Environment variables

- _`$MYSQL_PASSWORD`_ - The password to connect with Mysql.
- _`$MYSQL_USER`_ - The username to connect with Mysql.
- _`$DB_NAME`_ - Database name.
- _`$AWS_ACCESS_KEY_ID`_ - Aws acess key.
- _`$AWS_SECRET_ACCESS_KEY`_ -Aws secret key.
- _`$BUCKET`_ - Aws bucket name .
- _`$REGION`_ - Aws region where your bucket is.
- _`$MYSQL_PORT`_ - Port to connect with Mysql. default 3306.
- _`$MYSQL_HOST`_ - Host where mysql is running.
- _`$FILENAME`_ - Name to file in Azure Storage. Default name `default-date +"%Y-%m-%d_%H-%M"` output example `default-2015-08-03_17-58`
- _`$BACKUP_WINDOW`_ - What time should backup run. you should use crontab format, so see [documentation](http://www.freebsd.org/cgi/man.cgi?crontab(5). default value every day at 6 am.

# Example of running

```bash
docker run --rm --name mysql-backup \
  --env AWS_ACCESS_KEY_ID=AKIAIDHJDJCCC2KM4SSA \
  --env AWS_SECRET_ACCESS_KEY=HT1PWzBN5sjVPFHCuTX+VQs+8nQ00KteoI44iBfz \
  --env BUCKET=backups.example.com \
  --env REGION=eu-west-1  \
  --env FILENAME=backup \
  --env MYSQL_HOST=test.mysql.net \
  --env MYSQL_USER=root \
  --env MYSQL_PASSWORD=password \
  --env DB_NAME=mysql-db \
  --env BACKUP_WINDOW=' 0 6 * * * ' \
  fernandoneto/docker-mysql-backup-s3

```

This will upload to Aws S3 a file named `default-2015-08-04_09-47.sql.gz`.

### Building image

```bash
docker build -t fernandoneto/docker-mysql-backup-s3 .
```
