Role Name
=========

Role install lighthouse
lighthouse_vcs: https://github.com/VKCOM/lighthouse.git
nginx_user_name: nginx

Role Variables
--------------

| vars             | variables                     |
|------------------|:------------------------------|
| lighthouse_vcs   | Link to repository lighthouse |
| nginx_user_name  | Name of user to start nginx   |

Dependencies
----------------

This role needs to work 
https://github.com/mishalipatnikov/clickhouse

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         -  role: vector

License
-------

MIT

Author Information
------------------

Mikhail Lipatnikov