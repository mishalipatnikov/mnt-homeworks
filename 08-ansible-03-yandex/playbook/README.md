## Playbook

Playbook запускает установку clickhouse, vector и lighthouse на три ВМ в Yandex.Cloud, запускает службу `clickhouse-server` и `vector`, 
создает базу `logs` в `clickhouse`. В lighthouse-01 устанавливает веб-сервер nginx, копирует конфиги, и запускает nginx. Устанавливает git. 

### Variables
В каталоге group_vars задаются необходимые версии дистрибутивов.

|clickhouse_version|версия clickhouse| 
|-|--------|
|vector_version|версия vector|
|lighthouse_vcs|ссылка на репозиторий git lighthouse|
|nginx_user_name|от какого пользователя запускать веб-сервер nginx|
    
 ### Install Clickhouse
 Скачиваются rpm пакеты, устанавливается Clickhouse, создается база logs. 
 
### Install vector
Скачиваются пакеты, устанавливается vector. Запуск службы.

### Install lighthouse
Устанавливается веб-сервер nginx. Настраивается конфиги веб-сервера. Устанавливается git. Создается директория /var/www/lighthouse
Клонируется репозиторий lighthouse.

### Tags
|clickhouse|производит полную конфигурацию сервера clickhouse-01| 
|-|--------|
|vector|производит полную конфигурацию сервера vector-01|
|vector|производит полную конфигурацию сервера lighthouse-01|
   