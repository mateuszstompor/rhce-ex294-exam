# 12. Periodic jobs

Create a playbook that meets following requirements:
* Is placed at `/home/automation/plays/periodic_jobs.yml`
* Is executed against `proxy` group
* Schedules a periodic job which runs every hour on workdays. It should be executed by the `root`. Every time the job is span it adds separator `-----` which is followed by date and list of currently pluged devices below that. Please look at provided example. Make note of date format. Save the log to `/var/log/devices.log`. Set group and owner to the root user
* Uses `at` to schedule a job that is going to be executed after 1 minute and dumps output from `vmstat` to `/var/log/vmstat.log`. The file should be owned by automation user and group. The file should be recreated each time the playbook is executed. If the playbook is executed a second time within a minute second job should not be scheduled


Example entry from two hours might look like it is presented below
```
----- 09/21/21 21:11 -----
sda      8:0    0   64G  0 disk 
├─sda1   8:1    0  2.1G  0 part [SWAP]
└─sda2   8:2    0 61.9G  0 part /

----- 09/21/21 22:11 -----
sda      8:0    0   64G  0 disk 
├─sda1   8:1    0  2.1G  0 part [SWAP]
└─sda2   8:2    0 61.9G  0 part /
sdb      8:16   0    5G  0 disk 
```