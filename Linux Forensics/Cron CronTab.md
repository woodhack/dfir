# Cron/CronTab

A **crontab** is a special file that contains a list of tasks scheduled for periodic execution by the **cron** process. Each line in a crontab represents a cron job, which includes timing information and the command to be executed. Crontabs require six specific values to schedule tasks:

- **MIN**: The minute at which the task should execute (0-59).
- **HOUR**: The hour of the day (0-23) when the task should execute.
- **DOM**: The day of the month (1-31) when the task should execute.
- **MON**: The month (1-12) when the task should execute.
- **DOW**: The day of the week (0-7), with 0 and 7 both representing Sunday.
- **CMD**: The actual command or script to be executed.

Crontabs support the use of a wildcard symbol (`*`). If you don’t need to specify a particular value, you can use the `*` wildcard to represent "every value" for that field. For example, if you want the task to run every day, you can put `*` in the **DOW** field.

Example: Running a task every day at 2:30 AM would look like `30 2 * * *`, followed by the command you want to execute.

Common tasks that use cron include system backups, scheduled script execution, and automated maintenance.

To manage crontabs, users can view, edit, or delete cron jobs using commands like `crontab -l` to list tasks, `crontab -e` to edit the crontab, and `crontab -r` to remove it.

System-wide crontabs, typically found in `/etc/crontab`, allow administrators to set up cron jobs that affect the entire system.