Ansible role for Jira Software
==============================

A Role to install and manage JIRA Server configuration on rhel/CentOS servers atm.

Requirements
------------

There's no special requirement as long as you use variable `jira_java_install` to auto-install Java OpenJDK. Otherwise, you will need to install Java JRE before running this role.

Role Variables
--------------

Highlight variables (see defaults/main.yml for more details):

    jira_java_install

Defines wether role has to auto-install Java OpenJDK within the system

    jira_java_version
    jira_version

Define the versions to install from. Both are somewhat related as jira releases depend on specific JAVA version. Refer to [jira server's platform requirements](https://confluence.atlassian.com/jira/supported-platforms).

    jira_java_home

Defines java's home. Overwrite this variable if you manage your own java stack and disabled `jira_java_install`.

    jira_group
    jira_user
    jira_homedir
    jira_workdir

    jira_archive: 'atlassian-jira-software-{{ jira_version }}.tar.gz'
    jira_url: 'https://downloads.atlassian.com/software/jira/downloads/{{ jira_archive }}'

Define default download url. This variable can be overwrite if you manage your own package repository internally.

    jira_hostname
    jira_server_port
    jira_connector_port
    jira_connector_redirect_port
    jira_connection_timeout
    jira_context_path
    jira_proxy_name
    jira_scheme

Jira Server comes with a pre-configured servlet container (Apache Tomcat). Thoses variables allow you to update its configuration to match with your infrastructure requirements.

    jira_db_engine
    jira_db_hostname
    jira_db_port
    jira_db_name
    jira_db_user
    jira_db_passwd

Define database engine location and credentials.


Dependencies
------------

None.

Example Playbook
----------------

Here's an example playbook with few variables:

```yaml
- hosts: servers
  vars:
    jira_java_install: true
    jira_version: "7.12.0"
    jira_db_engine: postgresql
    jira_db_port: 5432
    jira_db_user: jira
    jira_db_passwd: "mysuperduperpassword"

  roles:
     - name: laxathom.jira
       tags:
        - jira
```

License
-------

MIT
