AKIAIDHJDJCCC2KM4SSA
Secret Access Key:
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

docker run --rm --name mysql-teste \
  --env AWS_ACCESS_KEY_ID=AKIAIDHJDJCCC2KM4SSA \
  --env AWS_SECRET_ACCESS_KEY=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 \
  --env BUCKET=backups.googs.com \
  --env REGION=eu-west-1  \
  --env FILENAME=acer \
  --env MYSQL_HOST=172.17.0.2 \
  --env MYSQL_PORT=3306 \
  --env MYSQL_USER=root \
  --env MYSQL_PASSWORD=findhit \
  --env DB_NAME=findhit \
  --env BACKUP_WINDOW=' * * * * * ' \
  --env DEBUG="true" \
  fneto:teste
