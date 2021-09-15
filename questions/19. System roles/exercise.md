# 19. System roles

Use NTP system role to configure all hosts time synchronization.
To achieve that create a playbook named `time.yml` that meets following requirements:
* Is placed at `/home/automation/plays`
* Uses `1.pl.pool.ntp.org` and `2.pl.pool.ntp.org` server pool to synchronize time
* Enables `iburst`
* Configure timezone as `UTC`