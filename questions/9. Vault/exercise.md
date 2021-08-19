# 9. Vault

* Create a file that meets following requirements:
    * Is placed at `/home/automation/plays/vars/regular_users.yml`
    * Is encrypted by Vault with id set to `users` and password to `eureka`
    * The file should contain a key `user_password`, its values should be set to `devops`

* Create a file that meets following requirements:
    * Is placed at `/home/automation/plays/vars/database_users.yml`
    * Is encrypted by Vault with password to `dbs-are-awesome`
    * The file should contain a key `db_password`, its values should be set to `devops`

* Create a file that meets following requirements:
    * Is placed at `/home/automation/plays/secrets/regular_users_password`
    * Contains `eureka` as the content

* Create a file that meets following requirements:
    * Is placed at `/home/automation/plays/secrets/database_users_password`
    * Contains `dbs-are-awesome` as the content
