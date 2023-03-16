## Playbook

Playbook запускает установку clickhouse, vector и lighthouse на три ВМ в Yandex.Cloud, запускает службу `clickhouse-server` и `vector`, 
создает базу `logs` в `clickhouse`. В lighthouse-01 устанавливает веб-сервер nginx, копирует конфиги, и запускает nginx. Устанавливает git, клонирует репозиторий lighthouse. 

### Variables
В каталоге group_vars задаются необходимые версии дистрибутивов.
`lighthouse_vcs` ссылка на репозиторий lighthouse
`nginx_user_name` пользователь, под которым запускается веб-сервер nginx
`clickhouse_version, vector_version` версии clickhouse и vector

    
 ### Install Clickhouse
 Скачиваются rpm пакеты, устанавливается Clickhouse, создается база logs. 
 
### Install vector
Скачиваются пакеты, устанавливается vector. Запуск службы.

### Install lighthouse
Устанавливается веб-сервер nginx. Копируется конфиг веб-сервера из папки templates. Устанавливается git. 
Клонируется репозиторий lighthouse в папку /var/www.

### Tags
`clickhouse` производит полную конфигурацию сервера clickhouse-01

`vector` производит полную конфигурацию сервера vector-01

`lighthouse` производит полную конфигурацию сервера lighthouse-01
   