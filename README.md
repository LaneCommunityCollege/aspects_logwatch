# UNMAINTAINED - aspects_logwatch
Configure Logwatch to send reports to whichever email addresses you want.

# Requirements
The server needs postfix or other email agent installed and configured.

# Role Variables
## aspects_cron_jobs
Create a cron job per email address.
### name
A unique name. I suggest ```Logwatch email to user@example.org```
### state
```absent``` only if you are removing a job.
```present``` all other times.
### backup
Set to ```no``` unless you want to use ansible's backup tool. See http://docs.ansible.com/cron_module.html
### minute
### hour
### day
### weekday
### month
How often you want to run the job. For a daily run, just set ```minute``` to something like ```0``` or ```5```, and ```hour``` to whichever hour you want to run it. A good choice might be ```0```. Then set the rest to ```*```. 

### user
Which user you want the job to run as. Remember, they have to be able to read the log files, and execute the logwatch program. ```root``` can do all that.

### job
    /usr/sbin/logwatch --output mail --mailto user@example.org --detail high

# Dependencies
* aspects_cron

Example Playbook
-------------------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }
      vars:
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

# License
MIT
