# aspects_logwatch
Install logwatch and remove the cron jobs from cron.daily so you can manage them yourself. Also helps manage logwatch service configuration in /etc/logwatch/conf/services.

[aspects_cron](https://github.com/LaneCommunityCollege/aspects_cron) is a good tool to use for this.

# Requirements
The server needs postfix or other email agent installed and configured.

# Role Variables
## aspects_logwatch_enabled
Boolean. False to skip role tasks. True to run role tasks.

## aspects_logwatch_conf_services
A dictionary/hash of logwatch service configuration files to copy.

Use this form:
```yaml
    aspects_logwatch_conf_services:
      sudo:
        src: < path/relative/to/inventory_dir/to/conf/file >
        dest: < /path/to/where/logwatch/will/read/the/file/from >
```

If you are overwriting a file that comes with Logwatch, make sure you copy everything from that version into the new version.

# Dependencies
* aspects_packages
* aspects_cron

# Example Playbook

```yaml
    - hosts: servers
      roles:
         - aspects_logwatch
      vars:
          aspects_cron_enabled: True
          aspects_logwatch_enabled: True
          aspects_cron_jobs:
            logwatchemail1:
              name: "Logwatch email to user@example.org"
              state: "present"
              backup: "no"
              minute: "0"
              hour: "0"
              day: "*"
              weekday: "*"
              month: "*"
              user: "root"
              job: "/usr/sbin/logwatch --output mail --mailto user@example.org --detail high"
            logwatchemail2:
              name: "Logwatch email to user2@example.org"
              state: "present"
              backup: "no"
              minute: "0"
              hour: "0"
              day: "*"
              weekday: "*"
              month: "*"
              user: "root"
              job: "/usr/sbin/logwatch --output mail --mailto user2@example.org --detail high"
```

# License
MIT
