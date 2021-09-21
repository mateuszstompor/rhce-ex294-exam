# 8. YUM repositories

* Create a playbook that meets following requirements:
    * Is placed at `/home/automation/plays/yum.yml`
    * Runs against `database` hosts 
    * Adds a definition of new yum repository
    * Enables this repository in yum
    * Enables GPG check for this repo, key can be found here `https://repo.mysql.com/RPM-GPG-KEY-mysql`
    * Sets description of the repo to `MySQL 5.7 Community Server`
    * Sets repo id to `mysql57-community`
    * Sets url of the repo to `http://repo.mysql.com/yum/mysql-5.7-community/el/6/$basearch/`
