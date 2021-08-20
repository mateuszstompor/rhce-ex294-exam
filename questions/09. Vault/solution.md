# 9. Vault - Solution

Navigate to `/home/automation/plays` as `automation` user and create directories for the files
```bash
mkdir secrets vars
```
Create yml that is going to contain password for encrypted file containing db-related data
```bash
echo dbs-are-awesome > /home/automation/plays/secrets/database_users_password
```
Create yml that is going to contain password for encrypted file containing users-related data
```bash
echo eureka > /home/automation/plays/secrets/regular_users_password
```
Create yml that is going to hold users-related vars
```bash
echo "user_password: devops" > /home/automation/plays/vars/regular_users.yml
```
Create yml that is going to hold db-related vars
```bash
echo "db_password: devops" > /home/automation/plays/vars/database_users.yml
```
Encrypt db-related vars file
```bash
ansible-vault encrypt /home/automation/plays/vars/database_users.yml --vault-id @./secrets/database_users_password
```

Encrypt users-related vars file
```bash
ansible-vault encrypt /home/automation/plays/vars/regular_users.yml --vault-id users@./secrets/regular_users_password
```