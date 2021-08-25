# 12. Periodic jobs

Create a playbook that meets following requirements:
* Is placed at `/home/automation/plays/periodic_jobs.yml`
* Is executed aginst `proxy` group
* Schedules a periodic job executed by the `root` user which runs every hour on weekdays and appends output from `date` command to `/var/log/time.log`
* Uses `at` to schedule a job that is going to be executed after 15 minutes and dump `Greatings from <hostname>` to `/var/log/greetings` where `<hostname>` is replaced with fqdn of the server. The file should be owned by devops user and group