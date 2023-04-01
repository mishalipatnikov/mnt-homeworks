# Домашнее задание к занятию "5. Тестирование roles"

## Подготовка к выполнению
1. Установите molecule: `pip3 install "molecule==3.5.2"`
2. Выполните `docker pull aragast/netology:latest` -  это образ с podman, tox и несколькими пайтонами (3.7 и 3.9) внутри

## Основная часть

Наша основная цель - настроить тестирование наших ролей. Задача: сделать сценарии тестирования для vector. Ожидаемый результат: все сценарии успешно проходят тестирование ролей.

### Molecule

1. Запустите  `molecule test -s centos7` внутри корневой директории clickhouse-role, посмотрите на вывод команды.
```commandline
[admin@fedora ansible-clickhouse]$ molecule --version
molecule 3.5.2 using python 3.11 
    ansible:2.14.3
    delegated:3.5.2 from molecule
    docker:2.1.0 from molecule_docker requiring collections: community.docker>=3.0.2 ansible.posix>=1.4.0
[admin@fedora ansible-clickhouse]$ molecule test -s centos_7
INFO     centos_7 scenario test matrix: dependency, lint, cleanup, destroy, syntax, create, prepare, converge, idempotence, side_effect, verify, cleanup, destroy
INFO     Performing prerun...
INFO     Set ANSIBLE_LIBRARY=/home/admin/.cache/ansible-compat/b9a93c/modules:/home/admin/.ansible/plugins/modules:/usr/share/ansible/plugins/modules
INFO     Set ANSIBLE_COLLECTIONS_PATH=/home/admin/.cache/ansible-compat/b9a93c/collections:/home/admin/.ansible/collections:/usr/share/ansible/collections
INFO     Set ANSIBLE_ROLES_PATH=/home/admin/.cache/ansible-compat/b9a93c/roles:/home/admin/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/hosts.yml linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/hosts
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/group_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/group_vars
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/host_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/host_vars
INFO     Running centos_7 > dependency
WARNING  Skipping, missing the requirements file.
WARNING  Skipping, missing the requirements file.
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/hosts.yml linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/hosts
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/group_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/group_vars
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/host_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/host_vars
INFO     Running centos_7 > lint
COMMAND: yamllint .
ansible-lint
flake8

Traceback (most recent call last):
  File "/usr/bin/ansible-lint", line 8, in <module>
    sys.exit(_run_cli_entrypoint())
             ^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3.11/site-packages/ansiblelint/__main__.py", line 344, in _run_cli_entrypoint
    sys.exit(main(sys.argv))
             ^^^^^^^^^^^^^^
  File "/usr/lib/python3.11/site-packages/ansiblelint/__main__.py", line 242, in main
    result = _get_matches(rules, options)
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3.11/site-packages/ansiblelint/runner.py", line 235, in _get_matches
    matches.extend(runner.run())
                   ^^^^^^^^^^^^
  File "/usr/lib/python3.11/site-packages/ansiblelint/runner.py", line 166, in run
    matches.extend(self._emit_matches(files))
  File "/usr/lib/python3.11/site-packages/ansiblelint/runner.py", line 204, in _emit_matches
    for child in ansiblelint.utils.find_children(lintable):
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3.11/site-packages/ansiblelint/utils.py", line 226, in find_children
    for child in play_children(basedir, item, lintable.kind, playbook_dir):
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3.11/site-packages/ansiblelint/utils.py", line 306, in play_children
    return delegate_map[k](basedir, k, v, parent_type)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3.11/site-packages/ansiblelint/utils.py", line 318, in _include_children
    if "{{" in v:  # pragma: no branch
       ^^^^^^^^^
TypeError: argument of type 'NoneType' is not iterable
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/hosts.yml linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/hosts
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/group_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/group_vars
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/host_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/host_vars
INFO     Running centos_7 > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/hosts.yml linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/hosts
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/group_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/group_vars
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/host_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/host_vars
INFO     Running centos_7 > destroy
INFO     Sanity checks: 'docker'

PLAY [Destroy] *****************************************************************

TASK [Set async_dir for HOME env] **********************************************
ok: [localhost]

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item=centos_7)

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).
ok: [localhost] => (item=centos_7)

TASK [Delete docker networks(s)] ***********************************************
skipping: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=3    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/hosts.yml linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/hosts
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/group_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/group_vars
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/host_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/host_vars
INFO     Running centos_7 > syntax

playbook: /home/admin/netology/ansible-clickhouse/molecule/resources/playbooks/converge.yml
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/hosts.yml linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/hosts
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/group_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/group_vars
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/host_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/host_vars
INFO     Running centos_7 > create

PLAY [Create] ******************************************************************

TASK [Set async_dir for HOME env] **********************************************
ok: [localhost]

TASK [Log into a Docker registry] **********************************************
skipping: [localhost] => (item=None) 
skipping: [localhost]

TASK [Check presence of custom Dockerfiles] ************************************
ok: [localhost] => (item={'capabilities': ['SYS_ADMIN'], 'command': '/usr/sbin/init', 'dockerfile': '../resources/Dockerfile.j2', 'env': {'ANSIBLE_USER': 'ansible', 'DEPLOY_GROUP': 'deployer', 'SUDO_GROUP': 'wheel', 'container': 'docker'}, 'image': 'centos:7', 'name': 'centos_7', 'privileged': True, 'tmpfs': ['/run', '/tmp'], 'volumes': ['/sys/fs/cgroup:/sys/fs/cgroup']})

TASK [Create Dockerfiles from image names] *************************************
changed: [localhost] => (item={'capabilities': ['SYS_ADMIN'], 'command': '/usr/sbin/init', 'dockerfile': '../resources/Dockerfile.j2', 'env': {'ANSIBLE_USER': 'ansible', 'DEPLOY_GROUP': 'deployer', 'SUDO_GROUP': 'wheel', 'container': 'docker'}, 'image': 'centos:7', 'name': 'centos_7', 'privileged': True, 'tmpfs': ['/run', '/tmp'], 'volumes': ['/sys/fs/cgroup:/sys/fs/cgroup']})

TASK [Synchronization the context] *********************************************
changed: [localhost] => (item={'capabilities': ['SYS_ADMIN'], 'command': '/usr/sbin/init', 'dockerfile': '../resources/Dockerfile.j2', 'env': {'ANSIBLE_USER': 'ansible', 'DEPLOY_GROUP': 'deployer', 'SUDO_GROUP': 'wheel', 'container': 'docker'}, 'image': 'centos:7', 'name': 'centos_7', 'privileged': True, 'tmpfs': ['/run', '/tmp'], 'volumes': ['/sys/fs/cgroup:/sys/fs/cgroup']})

TASK [Discover local Docker images] ********************************************
ok: [localhost] => (item=None)
ok: [localhost]

TASK [Build an Ansible compatible image (new)] *********************************
changed: [localhost] => (item=molecule_local/centos:7)

TASK [Create docker network(s)] ************************************************
skipping: [localhost]

TASK [Determine the CMD directives] ********************************************
ok: [localhost] => (item=None)
ok: [localhost]

TASK [Create molecule instance(s)] *********************************************
changed: [localhost] => (item=centos_7)

TASK [Wait for instance(s) creation to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (300 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (299 retries left).
changed: [localhost] => (item=None)
changed: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=9    changed=5    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0

INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/hosts.yml linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/hosts
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/group_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/group_vars
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/host_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/host_vars
INFO     Running centos_7 > prepare
WARNING  Skipping, prepare playbook not configured.
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/hosts.yml linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/hosts
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/group_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/group_vars
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/host_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/host_vars
INFO     Running centos_7 > converge

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [centos_7]

TASK [Apply Clickhouse Role] ***************************************************

TASK [ansible-clickhouse : Include OS Family Specific Variables] ***************
ok: [centos_7]

TASK [ansible-clickhouse : include_tasks] **************************************
included: /home/admin/netology/ansible-clickhouse/tasks/precheck.yml for centos_7

TASK [ansible-clickhouse : Requirements check | Checking sse4_2 support] *******
ok: [centos_7]

TASK [ansible-clickhouse : Requirements check | Not supported distribution && release] ***
skipping: [centos_7]

TASK [ansible-clickhouse : include_tasks] **************************************
included: /home/admin/netology/ansible-clickhouse/tasks/params.yml for centos_7

TASK [ansible-clickhouse : Set clickhouse_service_enable] **********************
ok: [centos_7]

TASK [ansible-clickhouse : Set clickhouse_service_ensure] **********************
ok: [centos_7]

TASK [ansible-clickhouse : include_tasks] **************************************
included: /home/admin/netology/ansible-clickhouse/tasks/install/yum.yml for centos_7

TASK [ansible-clickhouse : Install by YUM | Ensure clickhouse repo installed] ***
--- before: /etc/yum.repos.d/clickhouse.repo
+++ after: /etc/yum.repos.d/clickhouse.repo
@@ -0,0 +1,6 @@
+[clickhouse]
+baseurl = https://packages.clickhouse.com/rpm/stable/
+enabled = 1
+gpgcheck = 0
+name = Clickhouse repo
+

changed: [centos_7]

TASK [ansible-clickhouse : Install by YUM | Ensure clickhouse package installed (latest)] ***
changed: [centos_7]

TASK [ansible-clickhouse : Install by YUM | Ensure clickhouse package installed (version latest)] ***
skipping: [centos_7]

TASK [ansible-clickhouse : include_tasks] **************************************
included: /home/admin/netology/ansible-clickhouse/tasks/configure/sys.yml for centos_7

TASK [ansible-clickhouse : Check clickhouse config, data and logs] *************
ok: [centos_7] => (item=/var/log/clickhouse-server)
--- before
+++ after
@@ -1,4 +1,4 @@
 {
-    "mode": "0700",
+    "mode": "0770",
     "path": "/etc/clickhouse-server"
 }

changed: [centos_7] => (item=/etc/clickhouse-server)
--- before
+++ after
@@ -1,7 +1,7 @@
 {
-    "group": 0,
-    "mode": "0755",
-    "owner": 0,
+    "group": 996,
+    "mode": "0770",
+    "owner": 999,
     "path": "/var/lib/clickhouse/tmp/",
-    "state": "absent"
+    "state": "directory"
 }

changed: [centos_7] => (item=/var/lib/clickhouse/tmp/)
--- before
+++ after
@@ -1,4 +1,4 @@
 {
-    "mode": "0700",
+    "mode": "0770",
     "path": "/var/lib/clickhouse/"
 }

changed: [centos_7] => (item=/var/lib/clickhouse/)

TASK [ansible-clickhouse : Config | Create config.d folder] ********************
--- before
+++ after
@@ -1,4 +1,4 @@
 {
-    "mode": "0500",
+    "mode": "0770",
     "path": "/etc/clickhouse-server/config.d"
 }

changed: [centos_7]

TASK [ansible-clickhouse : Config | Create users.d folder] *********************
--- before
+++ after
@@ -1,4 +1,4 @@
 {
-    "mode": "0500",
+    "mode": "0770",
     "path": "/etc/clickhouse-server/users.d"
 }

changed: [centos_7]

TASK [ansible-clickhouse : Config | Generate system config] ********************
--- before
+++ after: /home/admin/.ansible/tmp/ansible-local-6913az_p11hn/tmpepz5dz0k/config.j2
@@ -0,0 +1,382 @@
+<?xml version="1.0"?>
+<!--
+ -
+ - Ansible managed: Do NOT edit this file manually!
+ -
+--> 
+<clickhouse>
+    <logger>
+        <!-- Possible levels: https://github.com/pocoproject/poco/blob/develop/Foundation/include/Poco/Logger.h#L105 -->
+        <level>trace</level>
+        <log>/var/log/clickhouse-server/clickhouse-server.log</log>
+        <errorlog>/var/log/clickhouse-server/clickhouse-server.err.log</errorlog>
+        <size>1000M</size>
+        <count>10</count>
+    </logger>
+
+    <http_port>8123</http_port>
+
+    <tcp_port>9000</tcp_port>
+
+    <!-- Used with https_port and tcp_port_secure. Full ssl options list: https://github.com/ClickHouse-Extras/poco/blob/master/NetSSL_OpenSSL/include/Poco/Net/SSLManager.h#L71 -->
+    <openSSL>
+        <server> <!-- Used for https server AND secure tcp port -->
+            <!-- openssl req -subj "/CN=localhost" -new -newkey rsa:2048 -days 365 -nodes -x509 -keyout /etc/clickhouse-server/server.key -out /etc/clickhouse-server/server.crt -->
+            <certificateFile>/etc/clickhouse-server/server.crt</certificateFile>
+            <privateKeyFile>/etc/clickhouse-server/server.key</privateKeyFile>
+            <!-- openssl dhparam -out /etc/clickhouse-server/dhparam.pem 4096 -->
+            <dhParamsFile>/etc/clickhouse-server/dhparam.pem</dhParamsFile>
+            <verificationMode>none</verificationMode>
+            <loadDefaultCAFile>true</loadDefaultCAFile>
+            <cacheSessions>true</cacheSessions>
+            <disableProtocols>sslv2,sslv3</disableProtocols>
+            <preferServerCiphers>true</preferServerCiphers>
+        </server>
+
+        <client> <!-- Used for connecting to https dictionary source -->
+            <loadDefaultCAFile>true</loadDefaultCAFile>
+            <cacheSessions>true</cacheSessions>
+            <disableProtocols>sslv2,sslv3</disableProtocols>
+            <preferServerCiphers>true</preferServerCiphers>
+            <!-- Use for self-signed: <verificationMode>none</verificationMode> -->
+            <invalidCertificateHandler>
+                <!-- Use for self-signed: <name>AcceptCertificateHandler</name> -->
+                <name>RejectCertificateHandler</name>
+            </invalidCertificateHandler>
+        </client>
+    </openSSL>
+
+    <!-- Default root page on http[s] server. For example load UI from https://tabix.io/ when opening http://localhost:8123 -->
+    <!--
+    <http_server_default_response><![CDATA[<html ng-app="SMI2"><head><base href="http://ui.tabix.io/"></head><body><div ui-view="" class="content-ui"></div><script src="http://loader.tabix.io/master.js"></script></body></html>]]></http_server_default_response>
+    -->
+
+    <!-- Port for communication between replicas. Used for data exchange. -->
+    <interserver_http_port>9009</interserver_http_port>
+
+
+
+    <!-- Hostname that is used by other replicas to request this server.
+         If not specified, than it is determined analoguous to 'hostname -f' command.
+         This setting could be used to switch replication to another network interface.
+      -->
+    <!--
+    <interserver_http_host>example.clickhouse.com</interserver_http_host>
+    -->
+
+    <!-- Listen specified host. use :: (wildcard IPv6 address), if you want to accept connections both with IPv4 and IPv6 from everywhere. -->
+    <!-- <listen_host>::</listen_host> -->
+    <!-- Same for hosts with disabled ipv6: -->
+    <!-- <listen_host>0.0.0.0</listen_host> -->
+    <listen_host>127.0.0.1</listen_host>
+
+    <max_connections>2048</max_connections>
+    <keep_alive_timeout>3</keep_alive_timeout>
+
+    <!-- Maximum number of concurrent queries. -->
+    <max_concurrent_queries>100</max_concurrent_queries>
+
+    <!-- Set limit on number of open files (default: maximum). This setting makes sense on Mac OS X because getrlimit() fails to retrieve
+         correct maximum value. -->
+    <!-- <max_open_files>262144</max_open_files> -->
+
+    <!-- Size of cache of uncompressed blocks of data, used in tables of MergeTree family.
+         In bytes. Cache is single for server. Memory is allocated only on demand.
+         Cache is used when 'use_uncompressed_cache' user setting turned on (off by default).
+         Uncompressed cache is advantageous only for very short queries and in rare cases.
+      -->
+    <uncompressed_cache_size>8589934592</uncompressed_cache_size>
+
+    <!-- Approximate size of mark cache, used in tables of MergeTree family.
+         In bytes. Cache is single for server. Memory is allocated only on demand.
+         You should not lower this value.
+      -->
+    <mark_cache_size>5368709120</mark_cache_size>
+
+
+    <!-- Path to data directory, with trailing slash. -->
+    <path>/var/lib/clickhouse/</path>
+
+    <!-- Path to temporary data for processing hard queries. -->
+    <tmp_path>/var/lib/clickhouse/tmp/</tmp_path>
+
+    <!-- Directory with user provided files that are accessible by 'file' table function. -->
+    <user_files_path>/var/lib/clickhouse/user_files/</user_files_path>
+
+    <!-- Path to configuration file with users, access rights, profiles of settings, quotas. -->
+    <users_config>users.xml</users_config>
+
+    <!-- Default profile of settings. -->
+    <default_profile>default</default_profile>
+
+    <!-- System profile of settings. This settings are used by internal processes (Buffer storage, Distibuted DDL worker and so on). -->
+    <!-- <system_profile>default</system_profile> -->
+
+    <!-- Default database. -->
+    <default_database>default</default_database>
+
+    <!-- Server time zone could be set here.
+
+         Time zone is used when converting between String and DateTime types,
+          when printing DateTime in text formats and parsing DateTime from text,
+          it is used in date and time related functions, if specific time zone was not passed as an argument.
+
+         Time zone is specified as identifier from IANA time zone database, like UTC or Africa/Abidjan.
+         If not specified, system time zone at server startup is used.
+
+         Please note, that server could display time zone alias instead of specified name.
+         Example: W-SU is an alias for Europe/Moscow and Zulu is an alias for UTC.
+    -->
+    <!-- <timezone>Europe/Moscow</timezone> -->
+
+    <!-- You can specify umask here (see "man umask"). Server will apply it on startup.
+         Number is always parsed as octal. Default umask is 027 (other users cannot read logs, data files, etc; group can only read).
+    -->
+    <!-- <umask>022</umask> -->
+
+    <!-- Perform mlockall after startup to lower first queries latency
+          and to prevent clickhouse executable from being paged out under high IO load.
+         Enabling this option is recommended but will lead to increased startup time for up to a few seconds.
+    -->
+    <mlock_executable>False</mlock_executable>
+
+    <!-- Configuration of clusters that could be used in Distributed tables.
+         https://clickhouse.com/docs/en/engines/table-engines/special/distributed/
+      -->
+    <remote_servers incl="clickhouse_remote_servers" />
+
+
+    <!-- If element has 'incl' attribute, then for it's value will be used corresponding substitution from another file.
+         By default, path to file with substitutions is /etc/metrika.xml. It could be changed in config in 'include_from' element.
+         Values for substitutions are specified in /clickhouse/name_of_substitution elements in that file.
+      -->
+
+    <!-- ZooKeeper is used to store metadata about replicas, when using Replicated tables.
+         Optional. If you don't use replicated tables, you could omit that.
+
+         See https://clickhouse.com/docs/en/engines/table-engines/mergetree-family/replication/
+      -->
+    <zookeeper incl="zookeeper-servers" optional="true" />
+
+    <!-- Substitutions for parameters of replicated tables.
+          Optional. If you don't use replicated tables, you could omit that.
+         See https://clickhouse.com/docs/en/engines/table-engines/mergetree-family/replication/#creating-replicated-tables
+      -->
+    <macros incl="macros" optional="true" />
+
+
+    <!-- Reloading interval for embedded dictionaries, in seconds. Default: 3600. -->
+    <builtin_dictionaries_reload_interval>3600</builtin_dictionaries_reload_interval>
+
+    <!-- If true, dictionaries are created lazily on first use. Otherwise they are initialised on server startup. Default: true -->
+    <!-- See also: https://clickhouse.com/docs/en/operations/server-configuration-parameters/settings/#server_configuration_parameters-dictionaries_lazy_load -->
+    <dictionaries_lazy_load>True</dictionaries_lazy_load>
+
+    <!-- Maximum session timeout, in seconds. Default: 3600. -->
+    <max_session_timeout>3600</max_session_timeout>
+
+    <!-- Default session timeout, in seconds. Default: 60. -->
+    <default_session_timeout>60</default_session_timeout>
+
+    <!-- Sending data to Graphite for monitoring. Several sections can be defined. -->
+    <!--
+        interval - send every X second
+        root_path - prefix for keys
+        hostname_in_path - append hostname to root_path (default = true)
+        metrics - send data from table system.metrics
+        events - send data from table system.events
+        asynchronous_metrics - send data from table system.asynchronous_metrics
+    -->
+    <!--
+    <graphite>
+        <host>localhost</host>
+        <port>42000</port>
+        <timeout>0.1</timeout>
+        <interval>60</interval>
+        <root_path>one_min</root_path>
+        <hostname_in_path>true</hostname_in_path>
+
+        <metrics>true</metrics>
+        <events>true</events>
+        <asynchronous_metrics>true</asynchronous_metrics>
+    </graphite>
+    <graphite>
+        <host>localhost</host>
+        <port>42000</port>
+        <timeout>0.1</timeout>
+        <interval>1</interval>
+        <root_path>one_sec</root_path>
+
+        <metrics>true</metrics>
+        <events>true</events>
+        <asynchronous_metrics>false</asynchronous_metrics>
+    </graphite>
+    -->
+
+
+    <!-- Query log. Used only for queries with setting log_queries = 1. -->
+    <query_log>
+        <!-- What table to insert data. If table is not exist, it will be created.
+             When query log structure is changed after system update,
+              then old table will be renamed and new table will be created automatically.
+        -->
+        <database>system</database>
+        <table>query_log</table>
+        <!--
+            PARTITION BY expr https://clickhouse.com/docs/en/table_engines/mergetree-family/custom_partitioning_key/
+            Example:
+                event_date
+                toMonday(event_date)
+                toYYYYMM(event_date)
+                toStartOfHour(event_time)
+        -->
+        <partition_by>toYYYYMM(event_date)</partition_by>
+        <!-- Interval of flushing data. -->
+        <flush_interval_milliseconds>7500</flush_interval_milliseconds>
+    </query_log>
+
+    <!-- Query thread log. Has information about all threads participated in query execution.
+         Used only for queries with setting log_query_threads = 1. -->
+    <query_thread_log>
+        <database>system</database>
+        <table>query_thread_log</table>
+        <partition_by>toYYYYMM(event_date)</partition_by>
+        
+        <flush_interval_milliseconds>7500</flush_interval_milliseconds>
+    </query_thread_log>
+
+    <!-- Uncomment if use part log.
+         Part log contains information about all actions with parts in MergeTree tables (creation, deletion, merges, downloads).
+    <part_log>
+        <database>system</database>
+        <table>part_log</table>
+        <flush_interval_milliseconds>7500</flush_interval_milliseconds>
+    </part_log>
+    -->
+
+
+    <!-- Parameters for embedded dictionaries, used in Yandex.Metrica.
+         See https://clickhouse.com/docs/en/dicts/internal_dicts/
+    -->
+
+    <!-- Path to file with region hierarchy. -->
+    <!-- <path_to_regions_hierarchy_file>/opt/geo/regions_hierarchy.txt</path_to_regions_hierarchy_file> -->
+
+    <!-- Path to directory with files containing names of regions -->
+    <!-- <path_to_regions_names_files>/opt/geo/</path_to_regions_names_files> -->
+
+
+    <!-- Configuration of external dictionaries. See:
+         https://clickhouse.com/docs/en/sql-reference/dictionaries/external-dictionaries/external-dicts
+    -->
+    <dictionaries_config>*_dictionary.xml</dictionaries_config>
+
+    <!-- Uncomment if you want data to be compressed 30-100% better.
+         Don't do that if you just started using ClickHouse.
+      -->
+    <compression incl="clickhouse_compression">
+    <!--
+        <!- - Set of variants. Checked in order. Last matching case wins. If nothing matches, lz4 will be used. - ->
+        <case>
+
+            <!- - Conditions. All must be satisfied. Some conditions may be omitted. - ->
+            <min_part_size>10000000000</min_part_size>        <!- - Min part size in bytes. - ->
+            <min_part_size_ratio>0.01</min_part_size_ratio>   <!- - Min size of part relative to whole table size. - ->
+
+            <!- - What compression method to use. - ->
+            <method>zstd</method>
+        </case>
+    -->
+    </compression>
+
+    <!-- Allow to execute distributed DDL queries (CREATE, DROP, ALTER, RENAME) on cluster.
+         Works only if ZooKeeper is enabled. Comment it if such functionality isn't required. -->
+    <distributed_ddl>
+        <!-- Path in ZooKeeper to queue with DDL queries -->
+        <path>/clickhouse/task_queue/ddl</path>
+
+        <!-- Settings from this profile will be used to execute DDL queries -->
+        <!-- <profile>default</profile> -->
+    </distributed_ddl>
+
+    <!-- Settings to fine tune MergeTree tables. See documentation in source code, in MergeTreeSettings.h -->
+        <merge_tree>
+        </merge_tree>
+
+    <!-- Protection from accidental DROP.
+         If size of a MergeTree table is greater than max_table_size_to_drop (in bytes) than table could not be dropped with any DROP query.
+         If you want do delete one table and don't want to restart clickhouse-server, you could create special file <clickhouse-path>/flags/force_drop_table and make DROP once.
+         By default max_table_size_to_drop is 50GB; max_table_size_to_drop=0 allows to DROP any tables.
+         The same for max_partition_size_to_drop.
+         Uncomment to disable protection.
+    -->
+    <!-- <max_table_size_to_drop>0</max_table_size_to_drop> -->
+    <!-- <max_partition_size_to_drop>0</max_partition_size_to_drop> -->
+
+    <!-- Example of parameters for GraphiteMergeTree table engine -->
+    <graphite_rollup_example>
+        <pattern>
+            <regexp>click_cost</regexp>
+            <function>any</function>
+            <retention>
+                <age>0</age>
+                <precision>3600</precision>
+            </retention>
+            <retention>
+                <age>86400</age>
+                <precision>60</precision>
+            </retention>
+        </pattern>
+        <default>
+            <function>max</function>
+            <retention>
+                <age>0</age>
+                <precision>60</precision>
+            </retention>
+            <retention>
+                <age>3600</age>
+                <precision>300</precision>
+            </retention>
+            <retention>
+                <age>86400</age>
+                <precision>3600</precision>
+            </retention>
+        </default>
+    </graphite_rollup_example>
+
+
+    <!-- Exposing metrics data for scraping from Prometheus. -->
+    <!--
+        endpoint – HTTP endpoint for scraping metrics by prometheus server. Start from ‘/’.
+        port – Port for endpoint.
+        metrics – Flag that sets to expose metrics from the system.metrics table.
+        events – Flag that sets to expose metrics from the system.events table.
+        asynchronous_metrics – Flag that sets to expose current metrics values from the system.asynchronous_metrics table.
+    -->
+    <!--
+    <prometheus>
+        <endpoint>/metrics</endpoint>
+        <port>8001</port>
+        <metrics>true</metrics>
+        <events>true</events>
+        <asynchronous_metrics>true</asynchronous_metrics>
+    </prometheus>
+    -->
+
+
+    <!-- Directory in <clickhouse-path> containing schema files for various input formats.
+         The directory will be created if it doesn't exist.
+      -->
+    <format_schema_path>/var/lib/clickhouse//format_schemas/</format_schema_path>
+
+    <!-- Uncomment to disable ClickHouse internal DNS caching. -->
+    <!-- <disable_internal_dns_cache>1</disable_internal_dns_cache> -->
+
+    <kafka>
+    </kafka>
+
+
+
+
+
+</clickhouse>

changed: [centos_7]

TASK [ansible-clickhouse : Config | Generate users config] *********************
--- before
+++ after: /home/admin/.ansible/tmp/ansible-local-6913az_p11hn/tmpr6n9koyv/users.j2
@@ -0,0 +1,106 @@
+<?xml version="1.0"?>
+<!--
+ -
+ - Ansible managed: Do NOT edit this file manually!
+ -
+--> 
+<clickhouse>
+   <profiles>
+    <!-- Profiles of settings. -->
+    <!-- Default profiles. -->
+        <default>
+            <max_memory_usage>10000000000</max_memory_usage>
+            <use_uncompressed_cache>0</use_uncompressed_cache>
+            <load_balancing>random</load_balancing>
+            <max_partitions_per_insert_block>100</max_partitions_per_insert_block>
+        </default>
+        <readonly>
+            <readonly>1</readonly>
+        </readonly>
+        <!-- Default profiles end. -->
+    <!-- Custom profiles. -->
+        <!-- Custom profiles end. -->
+    </profiles>
+
+    <!-- Users and ACL. -->
+    <users>
+    <!-- Default users. -->
+            <!-- Default user for login if user not defined -->
+        <default>
+                <password></password>
+                <networks incl="networks" replace="replace">
+                <ip>::1</ip>
+                <ip>127.0.0.1</ip>
+                </networks>
+        <profile>default</profile>
+        <quota>default</quota>
+            </default>
+            <!-- Example of user with readonly access -->
+        <readonly>
+                <password></password>
+                <networks incl="networks" replace="replace">
+                <ip>::1</ip>
+                <ip>127.0.0.1</ip>
+                </networks>
+        <profile>readonly</profile>
+        <quota>default</quota>
+            </readonly>
+        <!-- Custom users. -->
+            <!-- classic user with plain password -->
+        <testuser>
+                <password_sha256_hex>f2ca1bb6c7e907d06dafe4687e579fce76b37e4e93b7605022da52e6ccc26fd2</password_sha256_hex>
+                <networks incl="networks" replace="replace">
+                <ip>::1</ip>
+                <ip>127.0.0.1</ip>
+                </networks>
+        <profile>default</profile>
+        <quota>default</quota>
+                 <allow_databases>
+                    <database>testu1</database>
+                </allow_databases>
+                            </testuser>
+            <!-- classic user with hex password -->
+        <testuser2>
+                <password>testplpassword</password>
+                <networks incl="networks" replace="replace">
+                <ip>::1</ip>
+                <ip>127.0.0.1</ip>
+                </networks>
+        <profile>default</profile>
+        <quota>default</quota>
+                 <allow_databases>
+                    <database>testu2</database>
+                </allow_databases>
+                            </testuser2>
+            <!-- classic user with multi dbs and multi-custom network allow password -->
+        <testuser3>
+                <password>testplpassword</password>
+                <networks incl="networks" replace="replace">
+                <ip>192.168.0.0/24</ip>
+                <ip>10.0.0.0/8</ip>
+                </networks>
+        <profile>default</profile>
+        <quota>default</quota>
+                 <allow_databases>
+                    <database>testu1</database>
+                    <database>testu2</database>
+                    <database>testu3</database>
+                </allow_databases>
+                            </testuser3>
+        </users>
+
+    <!-- Quotas. -->
+    <quotas>
+        <!-- Default quotas. -->
+        <default>
+        <interval>
+        <duration>3600</duration>
+        <queries>0</queries>
+        <errors>0</errors>
+        <result_rows>0</result_rows>
+        <read_rows>0</read_rows>
+        <execution_time>0</execution_time>
+    </interval>
+        </default>
+            </quotas>
+</clickhouse>

changed: [centos_7]

TASK [ansible-clickhouse : Config | Generate remote_servers config] ************
skipping: [centos_7]

TASK [ansible-clickhouse : Config | Generate macros config] ********************
skipping: [centos_7]

TASK [ansible-clickhouse : Config | Generate zookeeper servers config] *********
skipping: [centos_7]

TASK [ansible-clickhouse : Config | Fix interserver_http_port and intersever_https_port collision] ***
skipping: [centos_7]

TASK [ansible-clickhouse : Notify Handlers Now] ********************************

RUNNING HANDLER [ansible-clickhouse : Restart Clickhouse Service] **************
ok: [centos_7]

TASK [ansible-clickhouse : include_tasks] **************************************
included: /home/admin/netology/ansible-clickhouse/tasks/service.yml for centos_7

TASK [ansible-clickhouse : Ensure clickhouse-server.service is enabled: True and state: restarted] ***
fatal: [centos_7]: FAILED! => {"changed": false, "msg": "Service is in unknown state", "status": {}}

PLAY RECAP *********************************************************************
centos_7                   : ok=18   changed=7    unreachable=0    failed=1    skipped=6    rescued=0    ignored=0

CRITICAL Ansible return code was 2, command was: ['ansible-playbook', '-D', '--inventory', '/home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory', '--skip-tags', 'molecule-notest,notest', '/home/admin/netology/ansible-clickhouse/molecule/resources/playbooks/converge.yml']
WARNING  An error occurred during the test sequence action: 'converge'. Cleaning up.
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/hosts.yml linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/hosts
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/group_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/group_vars
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/host_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/host_vars
INFO     Running centos_7 > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/hosts.yml linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/hosts
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/group_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/group_vars
INFO     Inventory /home/admin/netology/ansible-clickhouse/molecule/centos_7/../resources/inventory/host_vars/ linked to /home/admin/.cache/molecule/ansible-clickhouse/centos_7/inventory/host_vars
INFO     Running centos_7 > destroy

PLAY [Destroy] *****************************************************************

TASK [Set async_dir for HOME env] **********************************************
ok: [localhost]

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item=centos_7)

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).
changed: [localhost] => (item=centos_7)

TASK [Delete docker networks(s)] ***********************************************
skipping: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=3    changed=2    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Pruning extra files from scenario ephemeral directory


```
2. Перейдите в каталог с ролью vector-role и создайте сценарий тестирования по умолчанию при помощи `molecule init scenario --driver-name docker`.
3. Добавьте несколько разных дистрибутивов (centos:8, ubuntu:latest) для инстансов и протестируйте роль, исправьте найденные ошибки, если они есть.
4. Добавьте несколько assert'ов в verify.yml файл для  проверки работоспособности vector-role (проверка, что конфиг валидный, проверка успешности запуска, etc). Запустите тестирование роли повторно и проверьте, что оно прошло успешно.
```commandline
[admin@fedora vector-role]$ molecule test -s centos
INFO     centos scenario test matrix: dependency, lint, cleanup, destroy, syntax, create, prepare, converge, idempotence, side_effect, verify, cleanup, destroy
INFO     Performing prerun...
INFO     Set ANSIBLE_LIBRARY=/home/admin/.cache/ansible-compat/f5bcd7/modules:/home/admin/.ansible/plugins/modules:/usr/share/ansible/plugins/modules
INFO     Set ANSIBLE_COLLECTIONS_PATH=/home/admin/.cache/ansible-compat/f5bcd7/collections:/home/admin/.ansible/collections:/usr/share/ansible/collections
INFO     Set ANSIBLE_ROLES_PATH=/home/admin/.cache/ansible-compat/f5bcd7/roles:/home/admin/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles
INFO     Running centos > dependency
INFO     Running from /home/admin/mnt-homeworks/08-ansible-05-testing/vector-role : ansible-galaxy collection install -vvv community.docker:>=3.0.2
INFO     Running from /home/admin/mnt-homeworks/08-ansible-05-testing/vector-role : ansible-galaxy collection install -vvv ansible.posix:>=1.4.0
WARNING  Skipping, missing the requirements file.
WARNING  Skipping, missing the requirements file.
INFO     Running centos > lint
INFO     Lint is disabled.
INFO     Running centos > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running centos > destroy
INFO     Sanity checks: 'docker'

PLAY [Destroy] *****************************************************************

TASK [Set async_dir for HOME env] **********************************************
ok: [localhost]

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item=instance)

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).
ok: [localhost] => (item=instance)

TASK [Delete docker networks(s)] ***********************************************
skipping: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=3    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Running centos > syntax

playbook: /home/admin/mnt-homeworks/08-ansible-05-testing/vector-role/molecule/centos/converge.yml
INFO     Running centos > create

PLAY [Create] ******************************************************************

TASK [Set async_dir for HOME env] **********************************************
ok: [localhost]

TASK [Log into a Docker registry] **********************************************
skipping: [localhost] => (item=None) 
skipping: [localhost]

TASK [Check presence of custom Dockerfiles] ************************************
ok: [localhost] => (item={'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True})

TASK [Create Dockerfiles from image names] *************************************
skipping: [localhost] => (item={'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True}) 
skipping: [localhost]

TASK [Synchronization the context] *********************************************
skipping: [localhost] => (item={'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True}) 
skipping: [localhost]

TASK [Discover local Docker images] ********************************************
ok: [localhost] => (item={'changed': False, 'skipped': True, 'skip_reason': 'Conditional result was False', 'item': {'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item', 'i': 0, 'ansible_index_var': 'i'})

TASK [Build an Ansible compatible image (new)] *********************************
skipping: [localhost] => (item=molecule_local/docker.io/pycontribs/centos:8) 
skipping: [localhost]

TASK [Create docker network(s)] ************************************************
skipping: [localhost]

TASK [Determine the CMD directives] ********************************************
ok: [localhost] => (item={'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True})

TASK [Create molecule instance(s)] *********************************************
changed: [localhost] => (item=instance)

TASK [Wait for instance(s) creation to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (300 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (299 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (298 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (297 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (296 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (295 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (294 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (293 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (292 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (291 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (290 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (289 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (288 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (287 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (286 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (285 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (284 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (283 retries left).
FAILED - RETRYING: [localhost]: Wait for instance(s) creation to complete (282 retries left).
changed: [localhost] => (item={'failed': 0, 'started': 1, 'finished': 0, 'ansible_job_id': '237580252041.27591', 'results_file': '/home/admin/.ansible_async/237580252041.27591', 'changed': True, 'item': {'image': 'docker.io/pycontribs/centos:8', 'name': 'instance', 'pre_build_image': True}, 'ansible_loop_var': 'item'})

PLAY RECAP *********************************************************************
localhost                  : ok=6    changed=2    unreachable=0    failed=0    skipped=5    rescued=0    ignored=0

INFO     Running centos > prepare
WARNING  Skipping, prepare playbook not configured.
INFO     Running centos > converge

PLAY [Converge] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [instance]

TASK [Include vector-role] *****************************************************

TASK [vector-role : Get vector distrib] ****************************************
changed: [instance]

TASK [vector-role : Install vector packages] ***********************************
fatal: [instance]: FAILED! => {"changed": false, "msg": "Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: No URLs in mirrorlist", "rc": 1, "results": []}

PLAY RECAP *********************************************************************
instance                   : ok=2    changed=1    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0

CRITICAL Ansible return code was 2, command was: ['ansible-playbook', '--inventory', '/home/admin/.cache/molecule/vector-role/centos/inventory', '--skip-tags', 'molecule-notest,notest', '/home/admin/mnt-homeworks/08-ansible-05-testing/vector-role/molecule/centos/converge.yml']
WARNING  An error occurred during the test sequence action: 'converge'. Cleaning up.
INFO     Running centos > cleanup
WARNING  Skipping, cleanup playbook not configured.
INFO     Running centos > destroy

PLAY [Destroy] *****************************************************************

TASK [Set async_dir for HOME env] **********************************************
ok: [localhost]

TASK [Destroy molecule instance(s)] ********************************************
changed: [localhost] => (item=instance)

TASK [Wait for instance(s) deletion to complete] *******************************
FAILED - RETRYING: [localhost]: Wait for instance(s) deletion to complete (300 retries left).
changed: [localhost] => (item=instance)

TASK [Delete docker networks(s)] ***********************************************
skipping: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=3    changed=2    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

INFO     Pruning extra files from scenario ephemeral directory

```
5. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.
 [Vector-role 1.1](https://github.com/mishalipatnikov/vector-role)

### Tox

1. Добавьте в директорию с vector-role файлы из [директории](./example)
2. Запустите `docker run --privileged=True -v <path_to_repo>:/opt/vector-role -w /opt/vector-role -it aragast/netology:latest /bin/bash`, где path_to_repo - путь до корня репозитория с vector-role на вашей файловой системе.
```commandline
[admin@fedora vector-role]$ docker run --privileged=True -v /home/admin/vector-role/:/opt/vector-role -w /opt/vector-role -it aragast/netology:latest /bin/bash

```
3. Внутри контейнера выполните команду `tox`, посмотрите на вывод.
```commandline
tox
py39-ansible210 installed: ansible==2.10.7,ansible-base==2.10.17,ansible-compat==3.0.1,ansible-core==2.14.4,ansible-lint==5.1.3,arrow==1.2.3,attrs==22.2.0,bcrypt==4.0.1,binaryornot==0.4.4,bracex==2.3.post1,Cerberus==1.3.2,certifi==2022.12.7,cffi==1.15.1,chardet==5.1.0,charset-normalizer==3.1.0,click==8.1.3,click-help-colors==0.9.1,cookiecutter==2.1.1,cryptography==40.0.1,distro==1.8.0,docker==6.0.1,enrich==1.2.7,idna==3.4,Jinja2==3.1.2,jinja2-time==0.2.0,jmespath==1.0.1,jsonschema==4.17.3,lxml==4.9.2,markdown-it-py==2.2.0,MarkupSafe==2.1.2,mdurl==0.1.2,molecule==3.4.0,molecule-docker==1.1.0,packaging==23.0,paramiko==2.12.0,pathspec==0.11.1,pluggy==0.13.1,pycparser==2.21,Pygments==2.14.0,PyNaCl==1.5.0,pyrsistent==0.19.3,python-dateutil==2.8.2,python-slugify==8.0.1,PyYAML==5.4.1,requests==2.28.2,resolvelib==0.8.1,rich==13.3.3,ruamel.yaml==0.17.21,ruamel.yaml.clib==0.2.7,selinux==0.3.0,six==1.16.0,subprocess-tee==0.4.1,tenacity==8.2.2,text-unidecode==1.3,urllib3==1.26.15,wcmatch==8.4.1,websocket-client==1.5.1,yamllint==1.26.3
py39-ansible210 run-test-pre: PYTHONHASHSEED='746519202'
py39-ansible210 run-test: commands[0] | molecule test -s tox --destroy always
INFO     tox scenario test matrix: destroy, create, converge, destroy
INFO     Performing prerun...
WARNING  Failed to locate command: [Errno 2] No such file or directory: 'git'
INFO     Guessed /opt/vector-role as project root directory
WARNING  Computed fully qualified role name of vector-role does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

INFO     Using /root/.cache/ansible-lint/b984a4/roles/vector-role symlink to current repository in order to enable Ansible to find the role using its expected full name.
INFO     Added ANSIBLE_ROLES_PATH=~/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/root/.cache/ansible-lint/b984a4/roles
INFO     Running tox > destroy
INFO     Sanity checks: 'docker'
Traceback (most recent call last):
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/urllib3/connectionpool.py", line 703, in urlopen
    httplib_response = self._make_request(
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/urllib3/connectionpool.py", line 398, in _make_request
    conn.request(method, url, **httplib_request_kw)
  File "/usr/local/lib/python3.9/http/client.py", line 1255, in request
    self._send_request(method, url, body, headers, encode_chunked)
  File "/usr/local/lib/python3.9/http/client.py", line 1301, in _send_request
    self.endheaders(body, encode_chunked=encode_chunked)
  File "/usr/local/lib/python3.9/http/client.py", line 1250, in endheaders
    self._send_output(message_body, encode_chunked=encode_chunked)
  File "/usr/local/lib/python3.9/http/client.py", line 1010, in _send_output
    self.send(msg)
  File "/usr/local/lib/python3.9/http/client.py", line 950, in send
    self.connect()
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/docker/transport/unixconn.py", line 30, in connect
    sock.connect(self.unix_socket)
FileNotFoundError: [Errno 2] No such file or directory

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/requests/adapters.py", line 489, in send
    resp = conn.urlopen(
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/urllib3/connectionpool.py", line 787, in urlopen
    retries = retries.increment(
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/urllib3/util/retry.py", line 550, in increment
    raise six.reraise(type(error), error, _stacktrace)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/urllib3/packages/six.py", line 769, in reraise
    raise value.with_traceback(tb)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/urllib3/connectionpool.py", line 703, in urlopen
    httplib_response = self._make_request(
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/urllib3/connectionpool.py", line 398, in _make_request
    conn.request(method, url, **httplib_request_kw)
  File "/usr/local/lib/python3.9/http/client.py", line 1255, in request
    self._send_request(method, url, body, headers, encode_chunked)
  File "/usr/local/lib/python3.9/http/client.py", line 1301, in _send_request
    self.endheaders(body, encode_chunked=encode_chunked)
  File "/usr/local/lib/python3.9/http/client.py", line 1250, in endheaders
    self._send_output(message_body, encode_chunked=encode_chunked)
  File "/usr/local/lib/python3.9/http/client.py", line 1010, in _send_output
    self.send(msg)
  File "/usr/local/lib/python3.9/http/client.py", line 950, in send
    self.connect()
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/docker/transport/unixconn.py", line 30, in connect
    sock.connect(self.unix_socket)
urllib3.exceptions.ProtocolError: ('Connection aborted.', FileNotFoundError(2, 'No such file or directory'))

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/docker/api/client.py", line 214, in _retrieve_server_version
    return self.version(api_version=False)["ApiVersion"]
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/docker/api/daemon.py", line 181, in version
    return self._result(self._get(url), json=True)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/docker/utils/decorators.py", line 46, in inner
    return f(self, *args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/docker/api/client.py", line 237, in _get
    return self.get(url, **self._set_request_timeout(kwargs))
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/requests/sessions.py", line 600, in get
    return self.request("GET", url, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/requests/sessions.py", line 587, in request
    resp = self.send(prep, **send_kwargs)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/requests/sessions.py", line 701, in send
    r = adapter.send(request, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/requests/adapters.py", line 547, in send
    raise ConnectionError(err, request=request)
requests.exceptions.ConnectionError: ('Connection aborted.', FileNotFoundError(2, 'No such file or directory'))

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/opt/vector-role/.tox/py39-ansible210/bin/molecule", line 8, in <module>
    sys.exit(main())
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/click/core.py", line 1130, in __call__
    return self.main(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/click/core.py", line 1055, in main
    rv = self.invoke(ctx)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/click/core.py", line 1657, in invoke
    return _process_result(sub_ctx.command.invoke(sub_ctx))
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/click/core.py", line 1404, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/click/core.py", line 760, in invoke
    return __callback(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/click/decorators.py", line 26, in new_func
    return f(get_current_context(), *args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/molecule/command/test.py", line 159, in test
    base.execute_cmdline_scenarios(scenario_name, args, command_args, ansible_args)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/molecule/command/base.py", line 119, in execute_cmdline_scenarios
    execute_scenario(scenario)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/molecule/command/base.py", line 161, in execute_scenario
    execute_subcommand(scenario.config, action)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/molecule/command/base.py", line 150, in execute_subcommand
    return command(config).execute()
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/molecule/logger.py", line 187, in wrapper
    rt = func(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/molecule/command/destroy.py", line 107, in execute
    self._config.provisioner.destroy()
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/molecule/provisioner/ansible.py", line 705, in destroy
    pb.execute()
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/molecule/provisioner/ansible_playbook.py", line 106, in execute
    self._config.driver.sanity_checks()
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/molecule_docker/driver.py", line 236, in sanity_checks
    docker_client = docker.from_env()
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/docker/client.py", line 96, in from_env
    return cls(
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/docker/client.py", line 45, in __init__
    self.api = APIClient(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/docker/api/client.py", line 197, in __init__
    self._version = self._retrieve_server_version()
  File "/opt/vector-role/.tox/py39-ansible210/lib/python3.9/site-packages/docker/api/client.py", line 221, in _retrieve_server_version
    raise DockerException(
docker.errors.DockerException: Error while fetching server API version: ('Connection aborted.', FileNotFoundError(2, 'No such file or directory'))
ERROR: InvocationError for command /opt/vector-role/.tox/py39-ansible210/bin/molecule test -s tox --destroy always (exited with code 1)
py39-ansible30 installed: ansible==3.0.0,ansible-base==2.10.17,ansible-compat==3.0.1,ansible-core==2.14.4,ansible-lint==5.1.3,arrow==1.2.3,attrs==22.2.0,bcrypt==4.0.1,binaryornot==0.4.4,bracex==2.3.post1,Cerberus==1.3.2,certifi==2022.12.7,cffi==1.15.1,chardet==5.1.0,charset-normalizer==3.1.0,click==8.1.3,click-help-colors==0.9.1,cookiecutter==2.1.1,cryptography==40.0.1,distro==1.8.0,docker==6.0.1,enrich==1.2.7,idna==3.4,Jinja2==3.1.2,jinja2-time==0.2.0,jmespath==1.0.1,jsonschema==4.17.3,lxml==4.9.2,markdown-it-py==2.2.0,MarkupSafe==2.1.2,mdurl==0.1.2,molecule==3.4.0,molecule-docker==1.1.0,packaging==23.0,paramiko==2.12.0,pathspec==0.11.1,pluggy==0.13.1,pycparser==2.21,Pygments==2.14.0,PyNaCl==1.5.0,pyrsistent==0.19.3,python-dateutil==2.8.2,python-slugify==8.0.1,PyYAML==5.4.1,requests==2.28.2,resolvelib==0.8.1,rich==13.3.3,ruamel.yaml==0.17.21,ruamel.yaml.clib==0.2.7,selinux==0.3.0,six==1.16.0,subprocess-tee==0.4.1,tenacity==8.2.2,text-unidecode==1.3,urllib3==1.26.15,wcmatch==8.4.1,websocket-client==1.5.1,yamllint==1.26.3
py39-ansible30 run-test-pre: PYTHONHASHSEED='746519202'
py39-ansible30 run-test: commands[0] | molecule test -s tox --destroy always
INFO     tox scenario test matrix: destroy, create, converge, destroy
INFO     Performing prerun...
WARNING  Failed to locate command: [Errno 2] No such file or directory: 'git'
INFO     Guessed /opt/vector-role as project root directory
WARNING  Computed fully qualified role name of vector-role does not follow current galaxy requirements.
Please edit meta/main.yml and assure we can correctly determine full role name:

galaxy_info:
role_name: my_name  # if absent directory name hosting role is used instead
namespace: my_galaxy_namespace  # if absent, author is used instead

Namespace: https://galaxy.ansible.com/docs/contributing/namespaces.html#galaxy-namespace-limitations
Role: https://galaxy.ansible.com/docs/contributing/creating_role.html#role-names

As an alternative, you can add 'role-name' to either skip_list or warn_list.

INFO     Using /root/.cache/ansible-lint/b984a4/roles/vector-role symlink to current repository in order to enable Ansible to find the role using its expected full name.
INFO     Added ANSIBLE_ROLES_PATH=~/.ansible/roles:/usr/share/ansible/roles:/etc/ansible/roles:/root/.cache/ansible-lint/b984a4/roles
INFO     Running tox > destroy
INFO     Sanity checks: 'docker'
Traceback (most recent call last):
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/urllib3/connectionpool.py", line 703, in urlopen
    httplib_response = self._make_request(
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/urllib3/connectionpool.py", line 398, in _make_request
    conn.request(method, url, **httplib_request_kw)
  File "/usr/local/lib/python3.9/http/client.py", line 1255, in request
    self._send_request(method, url, body, headers, encode_chunked)
  File "/usr/local/lib/python3.9/http/client.py", line 1301, in _send_request
    self.endheaders(body, encode_chunked=encode_chunked)
  File "/usr/local/lib/python3.9/http/client.py", line 1250, in endheaders
    self._send_output(message_body, encode_chunked=encode_chunked)
  File "/usr/local/lib/python3.9/http/client.py", line 1010, in _send_output
    self.send(msg)
  File "/usr/local/lib/python3.9/http/client.py", line 950, in send
    self.connect()
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/docker/transport/unixconn.py", line 30, in connect
    sock.connect(self.unix_socket)
FileNotFoundError: [Errno 2] No such file or directory

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/requests/adapters.py", line 489, in send
    resp = conn.urlopen(
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/urllib3/connectionpool.py", line 787, in urlopen
    retries = retries.increment(
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/urllib3/util/retry.py", line 550, in increment
    raise six.reraise(type(error), error, _stacktrace)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/urllib3/packages/six.py", line 769, in reraise
    raise value.with_traceback(tb)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/urllib3/connectionpool.py", line 703, in urlopen
    httplib_response = self._make_request(
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/urllib3/connectionpool.py", line 398, in _make_request
    conn.request(method, url, **httplib_request_kw)
  File "/usr/local/lib/python3.9/http/client.py", line 1255, in request
    self._send_request(method, url, body, headers, encode_chunked)
  File "/usr/local/lib/python3.9/http/client.py", line 1301, in _send_request
    self.endheaders(body, encode_chunked=encode_chunked)
  File "/usr/local/lib/python3.9/http/client.py", line 1250, in endheaders
    self._send_output(message_body, encode_chunked=encode_chunked)
  File "/usr/local/lib/python3.9/http/client.py", line 1010, in _send_output
    self.send(msg)
  File "/usr/local/lib/python3.9/http/client.py", line 950, in send
    self.connect()
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/docker/transport/unixconn.py", line 30, in connect
    sock.connect(self.unix_socket)
urllib3.exceptions.ProtocolError: ('Connection aborted.', FileNotFoundError(2, 'No such file or directory'))

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/docker/api/client.py", line 214, in _retrieve_server_version
    return self.version(api_version=False)["ApiVersion"]
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/docker/api/daemon.py", line 181, in version
    return self._result(self._get(url), json=True)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/docker/utils/decorators.py", line 46, in inner
    return f(self, *args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/docker/api/client.py", line 237, in _get
    return self.get(url, **self._set_request_timeout(kwargs))
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/requests/sessions.py", line 600, in get
    return self.request("GET", url, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/requests/sessions.py", line 587, in request
    resp = self.send(prep, **send_kwargs)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/requests/sessions.py", line 701, in send
    r = adapter.send(request, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/requests/adapters.py", line 547, in send
    raise ConnectionError(err, request=request)
requests.exceptions.ConnectionError: ('Connection aborted.', FileNotFoundError(2, 'No such file or directory'))

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/opt/vector-role/.tox/py39-ansible30/bin/molecule", line 8, in <module>
    sys.exit(main())
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/click/core.py", line 1130, in __call__
    return self.main(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/click/core.py", line 1055, in main
    rv = self.invoke(ctx)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/click/core.py", line 1657, in invoke
    return _process_result(sub_ctx.command.invoke(sub_ctx))
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/click/core.py", line 1404, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/click/core.py", line 760, in invoke
    return __callback(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/click/decorators.py", line 26, in new_func
    return f(get_current_context(), *args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/molecule/command/test.py", line 159, in test
    base.execute_cmdline_scenarios(scenario_name, args, command_args, ansible_args)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/molecule/command/base.py", line 119, in execute_cmdline_scenarios
    execute_scenario(scenario)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/molecule/command/base.py", line 161, in execute_scenario
    execute_subcommand(scenario.config, action)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/molecule/command/base.py", line 150, in execute_subcommand
    return command(config).execute()
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/molecule/logger.py", line 187, in wrapper
    rt = func(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/molecule/command/destroy.py", line 107, in execute
    self._config.provisioner.destroy()
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/molecule/provisioner/ansible.py", line 705, in destroy
    pb.execute()
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/molecule/provisioner/ansible_playbook.py", line 106, in execute
    self._config.driver.sanity_checks()
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/molecule_docker/driver.py", line 236, in sanity_checks
    docker_client = docker.from_env()
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/docker/client.py", line 96, in from_env
    return cls(
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/docker/client.py", line 45, in __init__
    self.api = APIClient(*args, **kwargs)
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/docker/api/client.py", line 197, in __init__
    self._version = self._retrieve_server_version()
  File "/opt/vector-role/.tox/py39-ansible30/lib/python3.9/site-packages/docker/api/client.py", line 221, in _retrieve_server_version
    raise DockerException(
docker.errors.DockerException: Error while fetching server API version: ('Connection aborted.', FileNotFoundError(2, 'No such file or directory'))
ERROR: InvocationError for command /opt/vector-role/.tox/py39-ansible30/bin/molecule test -s tox --destroy always (exited with code 1)
_______________________________________________________________________________________________________________ summary ________________________________________________________________________________________________________________
ERROR:   py39-ansible210: commands failed
ERROR:   py39-ansible30: commands failed

```
5. Создайте облегчённый сценарий для `molecule` с драйвером `molecule_podman`. Проверьте его на исполнимость.
6. Пропишите правильную команду в `tox.ini` для того чтобы запускался облегчённый сценарий.
```commandline
[tox]
minversion = 1.8
basepython = python3.6
envlist = py{39}-ansible{210,30}
skipsdist = true

[testenv]
passenv = *
deps =
    -r tox-requirements.txt
    ansible210: ansible<3.0
    ansible30: ansible<3.1
commands =
    {posargs:molecule test -s tox --destroy always}
```
8. Запустите команду `tox`. Убедитесь, что всё отработало успешно.
```commandline
[root@0d20d2095815 vector-role]# tox
py39-ansible210 installed: ansible==2.10.7,ansible-base==2.10.17,ansible-compat==3.0.1,ansible-core==2.14.4,ansible-lint==5.1.3,arrow==1.2.3,attrs==22.2.0,bcrypt==4.0.1,binaryornot==0.4.4,bracex==2.3.post1,Cerberus==1.3.2,certifi==2022.12.7,cffi==1.15.1,chardet==5.1.0,charset-normalizer==3.1.0,click==8.1.3,click-help-colors==0.9.1,cookiecutter==2.1.1,cryptography==40.0.1,distro==1.8.0,docker==6.0.1,enrich==1.2.7,idna==3.4,Jinja2==3.1.2,jinja2-time==0.2.0,jmespath==1.0.1,jsonschema==4.17.3,lxml==4.9.2,markdown-it-py==2.2.0,MarkupSafe==2.1.2,mdurl==0.1.2,molecule==3.4.0,molecule-docker==1.1.0,packaging==23.0,paramiko==2.12.0,pathspec==0.11.1,pluggy==0.13.1,pycparser==2.21,Pygments==2.14.0,PyNaCl==1.5.0,pyrsistent==0.19.3,python-dateutil==2.8.2,python-slugify==8.0.1,PyYAML==5.4.1,requests==2.28.2,resolvelib==0.8.1,rich==13.3.3,ruamel.yaml==0.17.21,ruamel.yaml.clib==0.2.7,selinux==0.3.0,six==1.16.0,subprocess-tee==0.4.1,tenacity==8.2.2,text-unidecode==1.3,urllib3==1.26.15,wcmatch==8.4.1,websocket-client==1.5.1,yamllint==1.26.3
py39-ansible210 run-test-pre: PYTHONHASHSEED='2865250999'
py39-ansible210 run-test: commands[0] | molecule test -s tox --destroy always
---
dependency:
  name: galaxy
driver:
  name: podman
platforms:
  - image: docker.io/pycontribs/centos:7
    name: centos7
    pre_build_image: true
provisioner:
  name: ansible
scenario:
  test_sequence:
    - destroy
    - create
    - converge
    - destroy
verifier:
  name: ansible

CRITICAL Failed to pre-validate.

{'driver': [{'name': ['unallowed value podman']}]}
ERROR: InvocationError for command /opt/vector-role/.tox/py39-ansible210/bin/molecule test -s tox --destroy always (exited with code 1)
py39-ansible30 installed: ansible==3.0.0,ansible-base==2.10.17,ansible-compat==3.0.1,ansible-core==2.14.4,ansible-lint==5.1.3,arrow==1.2.3,attrs==22.2.0,bcrypt==4.0.1,binaryornot==0.4.4,bracex==2.3.post1,Cerberus==1.3.2,certifi==2022.12.7,cffi==1.15.1,chardet==5.1.0,charset-normalizer==3.1.0,click==8.1.3,click-help-colors==0.9.1,cookiecutter==2.1.1,cryptography==40.0.1,distro==1.8.0,docker==6.0.1,enrich==1.2.7,idna==3.4,Jinja2==3.1.2,jinja2-time==0.2.0,jmespath==1.0.1,jsonschema==4.17.3,lxml==4.9.2,markdown-it-py==2.2.0,MarkupSafe==2.1.2,mdurl==0.1.2,molecule==3.4.0,molecule-docker==1.1.0,packaging==23.0,paramiko==2.12.0,pathspec==0.11.1,pluggy==0.13.1,pycparser==2.21,Pygments==2.14.0,PyNaCl==1.5.0,pyrsistent==0.19.3,python-dateutil==2.8.2,python-slugify==8.0.1,PyYAML==5.4.1,requests==2.28.2,resolvelib==0.8.1,rich==13.3.3,ruamel.yaml==0.17.21,ruamel.yaml.clib==0.2.7,selinux==0.3.0,six==1.16.0,subprocess-tee==0.4.1,tenacity==8.2.2,text-unidecode==1.3,urllib3==1.26.15,wcmatch==8.4.1,websocket-client==1.5.1,yamllint==1.26.3
py39-ansible30 run-test-pre: PYTHONHASHSEED='2865250999'
py39-ansible30 run-test: commands[0] | molecule test -s tox --destroy always
---
dependency:
  name: galaxy
driver:
  name: podman
platforms:
  - image: docker.io/pycontribs/centos:7
    name: centos7
    pre_build_image: true
provisioner:
  name: ansible
scenario:
  test_sequence:
    - destroy
    - create
    - converge
    - destroy
verifier:
  name: ansible

CRITICAL Failed to pre-validate.

{'driver': [{'name': ['unallowed value podman']}]}
ERROR: InvocationError for command /opt/vector-role/.tox/py39-ansible30/bin/molecule test -s tox --destroy always (exited with code 1)
_______________________________________________________________________________________________________________ summary ________________________________________________________________________________________________________________
ERROR:   py39-ansible210: commands failed
ERROR:   py39-ansible30: commands failed

```
9. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.
[tox](https://github.com/mishalipatnikov/vector-role/tree/1.3)
[molecule](https://github.com/mishalipatnikov/vector-role/tree/1.1)

После выполнения у вас должно получится два сценария molecule и один tox.ini файл в репозитории. Не забудьте указать в ответе теги решений Tox и Molecule заданий. В качестве решения пришлите ссылку на  ваш репозиторий и скриншоты этапов выполнения задания. 

## Необязательная часть

1. Проделайте схожие манипуляции для создания роли lighthouse.
2. Создайте сценарий внутри любой из своих ролей, который умеет поднимать весь стек при помощи всех ролей.
3. Убедитесь в работоспособности своего стека. Создайте отдельный verify.yml, который будет проверять работоспособность интеграции всех инструментов между ними.
4. Выложите свои roles в репозитории.

В качестве решения пришлите ссылки и скриншоты этапов выполнения задания.

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
