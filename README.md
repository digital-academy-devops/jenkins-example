
## Jenkins в docker-compose

Запустите Jenkins:
```shell
docker-compose -p jenkins up -d master
```
Затем откройте страницу в браузере: [http://localhost:8080](http://localhost:8080)

Получение первичного пароля администратора:
```shell
docker-compose -p jenkins exec master cat /var/jenkins_home/secrets/initialAdminPassword
```

Или:

```shell
$ docker-compose logs master 2>&1 | grep -A2 "Please use the following password to proceed to installation"
```

Выполните первичную настройку.

### Добавление JNLP агента
После первичной настройки Jenkins, добавьте node c именем `jnlp-agent`.
Скопируйте секретный ключ в переменную `JNLP_KEY` в файле [.env](.env).
Запустите агента:
```shell
docker-compose -p jenkins up -d jnlp-agent
```

### Backup & restore
```shell
docker-compose -p jenkins run restore
```

```shell
docker-compose -p jenkins down
docker-compose -p jenkins run restore
docker-compose -p jenkins up -d
```

### Ссылки

- Плагин Docker: https://docs.cloudbees.com/docs/admin-resources/latest/plugins/docker-workflow 
- DIND agent: https://github.com/felipecrs/jenkins-agent-dind