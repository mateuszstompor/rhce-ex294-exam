# 5. Ansible Facts

* Create a playbook that meets following requirements:
    * Is placed at `/home/automation/plays/ansible_facts.yml` 
    * Runs against `database` group
    * Results in possiblity to retrieve a pair `role=mysql` from ansible facts path `ansible_local.custom.sample_exam` after calling setup module
