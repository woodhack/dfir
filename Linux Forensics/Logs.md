# Logs

The **/var/log** directory is where Linux stores most of its logging information. 

The **/var/log** directory contains log files for various services and applications. Common logs include:

- **/var/log/syslog** or **/var/log/messages**: Contains general system activity logs. These logs capture important system events such as startup messages, hardware changes, and kernel activity.
- **/var/log/auth.log**: Stores authentication-related messages, including login attempts, sudo usage, and other security events.
- **/var/log/dmesg**: Captures kernel ring buffer messages, which contain information about hardware and system boot processes.
- **/var/log/boot.log**: Logs boot-related messages, helping to diagnose any issues that occur during the system startup process.
- **/var/log/cron**: Contains messages related to the execution of cron jobs.
- **/var/log/apache2/** or **/var/log/nginx/**: Contains web server logs, which are useful for tracking requests, errors, and other web server activities.
- **/var/log/lastlog**: A record of the last login for each user.

Logs in the **/var/log** directory can grow over time and are often rotated (archived and replaced) by a process called **logrotate** to manage disk space.